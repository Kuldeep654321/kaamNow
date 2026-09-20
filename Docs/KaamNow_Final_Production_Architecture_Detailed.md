# KaamNow — Detailed Production Architecture

**Production-ready technical architecture • Modular monolith • Future scalable**

> This document is the technical source of truth for the KaamNow production backend/infrastructure direction.

## 1. Architecture Goals

- Production-first design: KaamNow is designed as a real service with security, observability, backups, auditability and controlled deployment.
- Modular monolith first: one FastAPI backend with strict domain boundaries. Extract services only when measured load or ownership boundaries justify it.
- Geospatial matching: PostgreSQL + PostGIS is the authoritative source for radius and distance queries.
- Async processing: Pub/Sub is used for notifications, retries, matching jobs, reminders and other non-blocking workloads.
- Realtime coordination: WebSocket + Redis supports private job chat and cross-instance presence/event coordination.
- Provider separation: business logic should not directly depend on a cloud-specific SDK wherever an adapter can be used.
- Safety by design: exact address, identity documents and SOS data have separate access controls and retention rules.
- Payment boundary: the platform records agreed amounts but does not custody, transfer, escrow or recover user-worker money.

## 2. Final Technology Stack

- Mobile application: Flutter + Dart.
- Android native integration: Kotlin through Flutter platform channels for supported emergency/device capabilities.
- Backend API: Python + FastAPI.
- Primary database: PostgreSQL with PostGIS.
- Cache/realtime coordination: Redis / managed Redis.
- Async messaging: Google Cloud Pub/Sub.
- Compute: Google Cloud Run containers.
- Edge: Cloudflare DNS, CDN, WAF and DDoS protection.
- Object storage: Cloudflare R2 with S3-compatible access.
- Push notifications: Firebase Cloud Messaging.
- Admin portal: Next.js + TypeScript.
- AI orchestration: Python module with provider/model adapters, structured output validation and deterministic fallback.
- Observability: OpenTelemetry + Sentry/Grafana Cloud.
- CI/CD: GitHub Actions.
- Infrastructure as Code: Terraform/OpenTofu.
- Secrets: managed secret storage and runtime-injected secrets; no secrets committed to Git.

## 3. High-Level System Architecture

```text
Client layer
Flutter Mobile App
  ├── User Mode
  └── Worker Mode

Admin layer
Next.js Admin Portal

Edge layer
Cloudflare
  ├── DNS
  ├── CDN
  ├── WAF
  └── DDoS protection

Application layer
GCP Cloud Run
  └── FastAPI Modular Monolith

Data and infrastructure
  ├── PostgreSQL + PostGIS
  ├── Redis
  ├── Pub/Sub
  └── Cloudflare R2

External platform integrations
  ├── Firebase Cloud Messaging
  ├── Maps/geocoding provider
  ├── OTP/SMS provider
  └── AI model provider(s), where enabled
```


## 4. Request Flow

- Mobile app sends an authenticated HTTPS request to the public API endpoint.
- Cloudflare terminates edge traffic and applies WAF/rate controls before forwarding allowed traffic.
- Cloud Run routes the request to FastAPI.
- FastAPI validates authentication, authorization, schema and business rules.
- Domain service performs the operation and uses PostgreSQL as the source of truth.
- Redis is used only for cache, ephemeral coordination, presence and suitable realtime state.
- Long-running or retryable work is published to Pub/Sub instead of blocking the API request.
- Workers consume Pub/Sub messages, execute idempotent jobs and record outcomes.
- FCM delivers mobile push notifications where required.
- Every sensitive administrative action and important state transition is auditable.

## 5. Backend Domain Architecture

- auth: OTP authentication, access/refresh sessions, device sessions, logout/revocation, RBAC.
- users: user profile, preferences, saved locations and account lifecycle.
- workers: worker profile, skills, availability, verification state, reputation and portfolio links.
- jobs: job creation, dynamic requirements, deadlines, radius, budget, status and history.
- matching: eligibility filters, PostGIS search, deterministic ranking, alert/retry strategy.
- assignments: worker acceptance, assignment locking, rejection, reassignment, multi-worker jobs.
- chat: private job chat, messages, system events, attachment references and moderation/report hooks.
- ratings: user-worker ratings, reviews, reputation events and achievement triggers.
- subscriptions: worker plan, 30-day free trial, renewal, expiry and configurable pricing.
- notifications: push, in-app notifications, reminders and preference handling.
- disputes: reports, issue categories, evidence references, admin review and resolution actions.
- sos: SOS lifecycle, location events, emergency contact/call flow metadata and local-audio references.
- admin: user/worker/job moderation, verification, disputes, subscriptions, promotions, settings and audit.
- ai: requirement interpretation, clarification, structured extraction and model/provider fallback.

## 6. User and Worker Account Model

- One mobile number maps to one account.
- The same account can operate in User Mode and Worker Mode.
- OTP authenticates the account; session tokens are separately managed and revocable.
- Worker profile is a role/profile attached to the account rather than a separate login identity.
- Identity verification is restricted; public profiles show only an Identity Verified state.
- Role checks are enforced in the backend, not only by hiding frontend screens.

## 7. Job Creation Pipeline

- Step 1: user enters a natural-language need.
- Step 2: AI Orchestrator extracts a candidate category, required skill, work type and missing information.
- Step 3: backend validates the AI output against allowed categories/skills.
- Step 4: only relevant dynamic questions are presented.
- Step 5: user selects radius: 5/10/15/20 km, optional deadline, worker count and budget where applicable.
- Step 6: inspection-based work can start without a fixed final price.
- Step 7: job is persisted as POSTED and matching begins.
- Step 8: matching events are queued where asynchronous processing is appropriate.
- Step 9: eligible workers receive alerts according to retry and notification rules.

## 8. Dynamic Requirement Examples

- Cleaning: area/size, basic or deep cleaning, rooms/sections, preferred date/time, special constraints.
- Electrician: problem description, appliance/fixture type, visible symptoms, urgency, access constraints.
- Plumber: leak/blockage/installation, fixture type, urgency, approximate location and access.
- AC repair: AC type, issue, cooling behavior, installation context and preferred time.
- Painting: rooms/area, surface type, paint scope, number of coats and preferred schedule.
- Cooking: meal type, servings, cuisine, dietary constraints, date/time.
- Pet care: pet type, service needed, duration, date/time and relevant instructions.
- The requirement schema remains extensible so new categories do not require redesigning the whole job system.

## 9. Matching Engine

- Hard eligibility filters: required skill, worker active state, availability, subscription eligibility and relevant restrictions.
- Geospatial filter: PostGIS ST_DWithin/radius-based queries using protected location data.
- Ranking inputs: distance, rating, relevant experience, similar completed jobs, reliability and availability.
- AI does not make an opaque final worker-selection decision; deterministic backend rules remain authoritative.
- Each candidate can have an internal match explanation for audit/debugging, such as skill match + distance + availability.
- Workers can receive a matching alert/buzzer.
- Acceptance must use an atomic/idempotent operation so two workers cannot both obtain the same single-worker assignment.
- Rejected/unavailable workers are skipped and the next eligible candidate can be alerted.
- If no suitable worker is found, configured radius expansion and Open Jobs can be used.

## 10. Geospatial Design

- Store coordinates in PostGIS using a suitable geographic coordinate type/index strategy.
- Use spatial indexes for radius queries.
- Before assignment, expose approximate area/distance rather than exact address.
- Exact address is released only when the job workflow reaches the permitted stage.
- Location permissions are optional where the product can operate without precise location; the backend must handle denied permissions.
- Location history should not be retained indefinitely; retain only what is required for the job, safety or audit purpose.
- Geospatial queries must be bounded by the user's selected/configured radius and system limits.

## 11. Job State Machine

- DRAFT → POSTED → MATCHING → ALERT_SENT → ACCEPTED → ASSIGNED → CHAT/COORDINATION → ON_THE_WAY → ARRIVED → IN_PROGRESS → DONE_REQUESTED → APPROVED → COMPLETED → RATING.
- Additional transitions: POSTED → CANCELLED; POSTED → EXPIRED; ACCEPTED → NO_SHOW; DONE_REQUESTED → DISPUTED → ADMIN_REVIEW → RESOLUTION.
- UI deliberately simplifies operational status to Assigned → In Progress → Done Requested → Approved → Completed → Rating.
- Worker cannot directly mark a job Completed.
- Worker selects Job Done; the user approves completion or reports an issue.
- Only user approval changes the authoritative job to COMPLETED.
- Completion triggers reputation, history and achievement updates.

## 12. Assignment Concurrency and Idempotency

- Use database transactions/locking or an equivalent atomic conditional update for single-worker assignment.
- Every accept, reject, cancel, reopen and completion request carries an idempotency key or unique operation reference.
- Duplicate API requests must return the existing operation result rather than create duplicate records.
- Background Pub/Sub messages must be safe to retry.
- State transitions must validate the current state before changing it.
- An immutable JobStatusHistory record should capture who/what caused important transitions.

## 13. Chat Architecture

- One private conversation is associated with the relevant job/assignment.
- PostgreSQL persists messages and authoritative message metadata.
- WebSocket delivers low-latency messages/events.
- Redis handles presence and cross-instance coordination where required.
- System messages can record assignment, amount approval, additional-work proposal, cancellation and completion events.
- Phone numbers are not automatically exposed.
- Report/block/safety actions must be available from the appropriate conversation context.
- Attachment support should use object storage references and signed URLs rather than database blobs.

## 14. Pricing and Payment Boundary

- Budget-oriented jobs may have a user-entered budget.
- Inspection-based jobs allow the worker to propose a price after inspection.
- Additional work requires a proposal and user approval before it becomes the agreed amount.
- The platform can display and record the agreed amount.
- User pays worker directly via UPI, QR or another mutually agreed external method.
- KaamNow does not hold money, run an escrow wallet, transfer funds, take transaction commission, store UPI PIN/OTP, guarantee refunds or recover disputed money.
- Financial disagreements may be reviewed as a platform case using agreed amount, relevant chat and job evidence, but the platform does not guarantee a financial outcome.
- Admin actions are platform-level: warning, restriction, suspension, reassignment, case closure or reputation/reliability action.

## 15. Worker Verification and Reputation

- Worker can submit Aadhaar, PAN or supported government-issued ID and a profile photo.
- Public profile shows Identity Verified rather than exposing ID details.
- Worker becomes Verified Worker after 3 user-approved completed jobs.
- Ratings are two-way: user rates worker and worker rates user.
- Reputation can use completed jobs, ratings, reliability, no-show history and relevant experience.
- Achievements include Verified Worker, Highly Rated, Quick Response and 50 Jobs Completed.
- High-performing/reliable workers can receive stronger matching priority while new workers retain access through Open Jobs.
- Unverified accusations must not automatically destroy reputation; reports require appropriate review.

## 16. Subscription Architecture

- Worker subscription: ₹100/month under the current product specification.
- First 30 days are completely free with worker features enabled.
- After trial expiry, profile remains visible and existing/ongoing jobs can continue, but new jobs/Open Jobs cannot be accepted until renewal.
- Subscription price, trial duration, plans, offers and discounts are configuration/API driven.
- Do not hard-code pricing in the Flutter or admin UI.
- Subscription state must be evaluated server-side before accepting a new job.
- Renewal/payment processing, if later integrated, should be isolated behind a payment-provider adapter.

## 17. Notifications and Event Architecture

- User events: job posted, matching started, worker found, assignment, work started, completion request, completion, rating, cancellation, reopen, dispute and reminders.
- Worker events: new matching job, assignment, timing changes, cancellation, reopened job, rating, subscription expiry and announcements.
- Use Pub/Sub for asynchronous notification jobs and retryable work.
- Notification delivery should be idempotent using event IDs.
- FCM tokens are device-specific and can expire; invalid tokens must be removed or disabled.
- Important notifications should also be represented in an in-app notification store so the user can recover missed push notifications.

## 18. SOS and Safety Architecture

- SOS is available to both users and workers for misbehavior, harassment, threats, physical confrontation, home-visit danger or medical emergencies.
- Supported emergency trigger mechanisms depend on Android/device capabilities; the product must not claim universal interception of every power-button pattern.
- SOS flow: Emergency Trigger → SOS Activated → Location Captured → Emergency Alert → Emergency Contact/Call Flow → SOS Safety Session.
- Audio recording begins only after SOS activation; normal app usage never secretly records.
- Android-approved microphone/background mechanisms and applicable privacy/recording requirements must be respected.
- Audio is encrypted and stored locally on the device by default; backend stores protected metadata and a local audio reference.
- SOS metadata can include session ID, account ID, timestamp, trigger type, location event, emergency status, local audio reference and incident/report status.
- Emergency contact/police calling is an assisted flow unless a real integration is implemented; do not promise automatic nearest-police dispatch.

## 19. Identity and Sensitive Data

- Separate identity-verification data from ordinary profile data.
- Use strict RBAC and least-privilege access.
- Never return government ID numbers in normal public profile APIs.
- Use field-level protection/encryption where appropriate.
- Maintain explicit retention and deletion/deactivation workflows.
- Log sensitive administrative access without logging secrets or unnecessary personal content.

## 20. Object Storage

- Store binary files in R2, not PostgreSQL.
- PostgreSQL stores object key, type, size, ownership and metadata.
- Worker portfolio uses Google Drive links by default rather than storing portfolio media directly.
- Before/after proof can use controlled external links where the product allows it.
- Private objects use short-lived signed access.
- Validate MIME type, size, extension and upload authorization.
- Malware scanning can be added to an asynchronous upload-processing pipeline when required.

## 21. AI Architecture

- AI Orchestrator is a backend module, not a direct client-side integration.
- Input is normalized and minimized before model calls.
- Model output uses a strict structured schema.
- Schema validation rejects malformed or unsupported category/skill output.
- AI failure falls back to deterministic category selection/manual clarification.
- Prompt/model providers are accessed through adapters so the product is not tied to one model vendor.
- AI should not receive unnecessary government ID, payment secrets, exact location or SOS audio.
- AI is an assistant for requirement understanding and clarification; authorization, payment boundary, safety and assignment rules remain deterministic.

## 22. Admin / Creator Portal

- Dashboard: users, workers, jobs, active matching, subscriptions, reports, disputes and operational health.
- Worker management: verification review, status, reputation actions and restrictions.
- Job management: search, status history, reassignment, cancellation and moderation.
- Disputes/reports: case queues, evidence references, notes, actions and audit trail.
- Subscriptions: price, trial duration, plans, offers and renewal configuration.
- Promotions: banners, ads, offers and announcements.
- Matching settings: radius policy, notification/retry configuration and safe thresholds.
- Platform settings: feature flags, categories, supported skills and operational configuration.
- Every privileged action is recorded in AdminAction/audit logs.

## 23. Security Architecture

- HTTPS everywhere; secure cookies/tokens according to client architecture.
- Short-lived access tokens with refresh/session rotation strategy.
- OTP rate limits, abuse controls and device/session management.
- RBAC enforced server-side on every privileged endpoint.
- Request validation using typed schemas.
- Rate limits by IP, account, device and sensitive endpoint where appropriate.
- WAF and application-level abuse protection.
- CORS restricted to approved origins.
- Security headers and safe content policies for the admin web app.
- Secrets injected through managed secret configuration.
- Dependency and container vulnerability scanning in CI.
- Database credentials use least privilege and are rotated according to operational policy.
- Audit logs are append-only from the application perspective.

## 24. Reliability and Failure Handling

- API timeouts and bounded retries.
- Pub/Sub retry with dead-letter handling for repeatedly failing jobs.
- Idempotency for notification, assignment, payment-metadata and state-transition operations.
- Graceful handling of Redis unavailability: authoritative requests should continue where safe without treating Redis as source of truth.
- Database connection pooling and controlled concurrency.
- Health/readiness endpoints for deployment orchestration.
- Feature flags for risky new functionality.
- Rollback-capable deployments.
- Backups with periodic restore tests rather than relying only on backup existence.

## 25. Observability

- Structured JSON logs with request ID/correlation ID.
- OpenTelemetry traces across API and background workers.
- Metrics for API latency, error rates, queue age, matching success, notification delivery, WebSocket connections and database health.
- Sentry for application exceptions and release tracking.
- Alerts for high error rate, database saturation, queue backlog, failed deployments and critical SOS pipeline failures.
- Do not log OTPs, access tokens, passwords, UPI PINs, government ID values or raw SOS audio.

## 26. Deployment Architecture

- Environments: development, staging and production.
- GitHub pull request → lint/test/security checks → container build → image scan → registry → staged deployment → smoke tests → production rollout.
- Use immutable container images tagged by commit/version.
- Terraform/OpenTofu defines cloud infrastructure.
- Runtime configuration is environment-specific and secret values are injected at deployment/runtime.
- Use gradual rollout where supported and maintain a rollback procedure.

## 27. Database Design Principles

- Use migrations with version control.
- Every table has explicit ownership/lifecycle rules.
- Use foreign keys and appropriate unique constraints.
- Use indexes based on actual query patterns.
- Use PostGIS spatial indexes for worker search.
- Partition only when measured data volume requires it.
- Keep audit/history records append-oriented.
- Do not put transient cache state in PostgreSQL unless it is required for business correctness.

## 28. Suggested Core API Groups

- POST /auth/otp/request
- POST /auth/otp/verify
- GET/PATCH /me
- GET/PATCH /worker/profile
- POST /jobs
- GET /jobs/{job_id}
- POST /jobs/{job_id}/match
- POST /jobs/{job_id}/accept
- POST /jobs/{job_id}/cancel
- POST /jobs/{job_id}/done-request
- POST /jobs/{job_id}/approve
- POST /jobs/{job_id}/reopen
- POST /jobs/{job_id}/report
- GET /jobs/{job_id}/chat
- POST /jobs/{job_id}/chat/messages
- POST /jobs/{job_id}/price-proposals
- POST /jobs/{job_id}/price-proposals/{id}/approve
- POST /sos
- POST /sos/{sos_id}/location
- POST /sos/{sos_id}/end
- GET /notifications
- GET /open-jobs
- GET /subscriptions/me
- Admin APIs under /admin/* with strict RBAC.

## 29. Repository Structure

```text
kaamnow/
├── apps/
│   ├── mobile/
│   │   ├── lib/
│   │   ├── android/
│   │   └── test/
│   └── admin/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── db/
│   │   ├── integrations/
│   │   ├── modules/
│   │   │   ├── auth/
│   │   │   ├── users/
│   │   │   ├── workers/
│   │   │   ├── jobs/
│   │   │   ├── matching/
│   │   │   ├── assignments/
│   │   │   ├── chat/
│   │   │   ├── ratings/
│   │   │   ├── subscriptions/
│   │   │   ├── notifications/
│   │   │   ├── disputes/
│   │   │   ├── sos/
│   │   │   ├── admin/
│   │   │   └── ai/
│   │   └── workers/
│   ├── migrations/
│   └── tests/
├── infrastructure/
│   ├── terraform/
│   ├── docker/
│   └── environments/
├── docs/
├── scripts/
└── .github/workflows/
```


## 30. Scaling Strategy

- Phase 1: single modular FastAPI application, horizontally scaled Cloud Run instances, managed PostgreSQL/PostGIS, Redis and Pub/Sub.
- Phase 2: independently scale background workers, notification workers and matching workers.
- Phase 3: extract only measured bottlenecks such as Matching or Chat/Realtime into separate services.
- Phase 4: introduce stronger event-driven boundaries if volume, team size or reliability requirements justify them.
- Kubernetes is not a launch requirement. Kafka is not a launch requirement. Multiple databases are not a launch requirement.
- Database scaling should begin with query/index optimization, connection pooling and vertical scaling before introducing distributed complexity.

## 31. Disaster Recovery

- Automated database backups with a defined retention policy.
- Periodic restore drills to validate that backups are usable.
- Object storage versioning/retention where appropriate.
- Infrastructure reproducible from Terraform/OpenTofu.
- Container images retained for rollback.
- Documented incident response and rollback runbooks.
- Define recovery objectives (RPO/RTO) before production launch and test them.

## 32. Production Checklist

- Custom domain and TLS configured.
- Cloudflare WAF/rules reviewed.
- Production database private connectivity and restricted credentials.
- PostGIS enabled and spatial indexes verified.
- Redis authentication/network restrictions configured.
- Pub/Sub retry/dead-letter policy configured.
- FCM production credentials protected.
- OTP provider configured with rate limits.
- Secrets removed from source code and repository history.
- CI/CD protected with branch/environment controls.
- Admin RBAC and audit logs tested.
- Identity data access tested.
- Exact-address privacy tested.
- SOS permissions and recording behavior tested on supported Android devices.
- Payment UI explicitly communicates direct user-worker payment.
- Privacy Policy, Terms and safety/reporting flows published.
- Monitoring alerts tested.
- Backup restore tested.
- Rollback tested.
- Load/performance testing completed for matching, chat and job creation.

## 33. Final Architecture Decision

- Recommended production foundation: Flutter + Kotlin Android integration, Cloudflare edge, GCP Cloud Run, FastAPI modular monolith, PostgreSQL + PostGIS, managed Redis, Pub/Sub, Cloudflare R2, FCM, Next.js Admin, Python AI Orchestrator, OpenTelemetry/Sentry/Grafana, GitHub Actions and Terraform/OpenTofu.
- The architecture deliberately avoids premature microservices and Kubernetes while preserving clean extraction boundaries for future growth.

