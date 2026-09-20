# KaamNow — Web Launch & Production Readiness Checklist

**Product:** KaamNow — Immediate Local Work  
**Document:** Web Launch, Security, SEO, Performance, Accessibility, Reliability & Production Checklist  
**Version:** 1.0  
**Status:** Detailed launch source of truth

---

# 1. Purpose

This document defines the complete checklist required before exposing KaamNow's public website, Creator/Admin portal, backend APIs, and production infrastructure to real users.

It expands the standard website launch checklist into KaamNow-specific requirements covering:

- Legal pages
- Privacy
- Security
- Authentication
- Secrets
- HTTPS
- Cookies
- SEO
- Social previews
- Accessibility
- Responsive design
- Performance
- Forms
- Spam protection
- Analytics
- Monitoring
- API security
- Database security
- Backups
- Notifications
- Chat
- Location privacy
- Identity verification
- SOS safety
- Subscription
- Payment boundary
- Admin security
- Deployment
- Incident response

---

# 2. Launch Scope

The production system is based on the final KaamNow architecture:

```text
Flutter Mobile App (Android / iOS)
          │
          │ HTTPS / WebSocket
          ▼
Cloudflare Edge
(DNS • CDN • WAF • DDoS • Rate Controls)
          │
          ▼
GCP Cloud Run
          │
          ▼
FastAPI Modular Monolith
 ├─ Auth / Users / Workers
 ├─ Jobs / Assignments
 ├─ Matching / PostGIS
 ├─ Chat / Realtime
 ├─ Ratings / Reputation
 ├─ Subscriptions
 ├─ Notifications
 ├─ Disputes / Reports
 ├─ SOS / Safety
 ├─ Admin APIs
 └─ AI Orchestration
      │
      ├───────────────┐
      ▼               ▼
Cloud SQL          Redis
PostgreSQL         Memorystore
+ PostGIS              │
      │                │
      └───────┬────────┘
              ▼
        Pub/Sub Workers
              │
              ├── Matching / Notifications
              ├── Reminders / Subscriptions
              └── Maintenance / Analytics

Object Storage: Cloudflare R2
Push: Firebase Cloud Messaging
Maps: Google Maps Platform
Admin: Next.js + TypeScript
Observability: OpenTelemetry + Sentry/Grafana
CI/CD: GitHub Actions
IaC: Terraform/OpenTofu
```

The mobile application must consume production APIs securely and must not contain private backend credentials.
Business logic, authorization, payment-boundary rules, matching rules and safety rules must be enforced server-side.

---

# 3. Privacy Policy

A production Privacy Policy must be published before launch.

It should explain, as applicable:

- Account information.
- Mobile number.
- OTP authentication.
- Name/profile information.
- Profile photo.
- Worker profile.
- Skills and availability.
- Job information.
- Approximate and exact location.
- Chat messages.
- Ratings and reviews.
- Reports and disputes.
- Identity verification.
- Subscription information.
- Notification data.
- Device/app information.
- Analytics.
- Cookies.
- Third-party services.
- SOS information.
- SOS location information.
- SOS audio behavior.
- Data retention.
- Data deletion.
- Account deactivation.
- User rights.
- Support/contact information.

### SOS privacy disclosure

The Privacy Policy must clearly explain:

- Normal app use does not secretly record audio.
- SOS audio begins only after SOS activation.
- Recording is subject to Android/device capabilities and permissions.
- Audio is stored locally in encrypted form according to the implemented design.
- The app should not claim that recording works universally when OS/device restrictions prevent it.

---

# 4. Terms & Conditions

Publish Terms & Conditions covering:

- User eligibility.
- Worker responsibilities.
- Job creation.
- Legitimate work requirements.
- Prohibited jobs.
- Accurate job information.
- Worker conduct.
- User conduct.
- Cancellation.
- No-show.
- Reopening jobs.
- Completion approval.
- Rating/review behavior.
- Reports.
- Disputes.
- Safety incidents.
- Chat rules.
- Identity verification.
- Worker verification.
- Subscription.
- Offers/deals.
- Account restrictions.
- Suspension.
- Termination.
- Platform limitations.

### Payment boundary

Clearly state:

- KaamNow is a job coordination platform.
- Payment is directly between User and Worker.
- KaamNow does not hold user funds.
- KaamNow does not operate escrow.
- KaamNow does not transfer funds between users.
- KaamNow does not store UPI PINs.
- KaamNow does not guarantee refunds.
- KaamNow does not automatically recover disputed money.
- External payment method is authoritative for the actual financial transaction.

---

# 5. Secrets & Environment Variables

No secret may be committed to GitHub.

Never expose:

- Database credentials.
- JWT signing secrets.
- Refresh-token secrets.
- Admin credentials.
- Firebase server credentials.
- FCM server credentials.
- Google Maps server API keys.
- AI provider keys.
- SMTP credentials.
- Cloud storage credentials.
- Redis credentials.
- Monitoring credentials.
- Third-party private keys.

Use:

```text
.env.example
```

for placeholders only.

Production secrets must be stored in a secure environment/secret manager.

### Repository checks

Before launch:

- Search Git history for leaked secrets.
- Rotate any secret that was previously committed.
- Verify `.gitignore`.
- Verify CI/CD does not print secrets.
- Verify build logs do not expose credentials.

---

# 6. HTTPS

Production must use HTTPS.

Check:

- Valid TLS certificate.
- HTTP redirects to HTTPS.
- No mixed content.
- Secure API endpoints.
- Secure WebSocket connections.
- Secure cookies.
- HSTS where appropriate.
- Certificate renewal process.

Production WebSocket:

```text
wss://
```

not:

```text
ws://
```

---

# 7. Cookie & Consent

If non-essential cookies or tracking are used:

- Show appropriate consent.
- Explain cookie categories.
- Provide required controls.
- Do not treat optional analytics/marketing cookies as strictly necessary.
- Respect user preferences.
- Document cookies in the Privacy Policy.

If the application does not use optional cookies, do not add an unnecessary cookie banner merely for appearance.

---

# 8. Authentication & Session Security

Authentication:

```text
Mobile Number
      ↓
OTP
      ↓
Access Token
      ↓
Authenticated Session
```

Check:

- OTP expiry.
- OTP attempt limits.
- Resend limits.
- Brute-force protection.
- Session expiration.
- Refresh-token rotation where implemented.
- Logout invalidation.
- Device/session management if supported.
- Secure token storage.
- No tokens in URLs.
- No tokens in logs.

Admin authentication must have stronger controls than ordinary user authentication.

---

# 9. Role-Based Access Control

Roles:

```text
USER
WORKER
ADMIN
SUPER_ADMIN
```

Verify that:

- User cannot access worker-only admin APIs.
- Worker cannot access admin APIs.
- Admin permissions are scoped.
- Sensitive verification data is restricted.
- Super-admin actions are protected.
- Frontend hiding alone is never treated as authorization.

Every sensitive backend endpoint must independently enforce authorization.

---

# 10. API Security

For FastAPI production APIs:

- HTTPS only.
- Authentication on protected routes.
- Authorization on every protected resource.
- Input validation with Pydantic.
- Request size limits.
- Rate limiting.
- Pagination.
- Query limits.
- CORS allowlist.
- Secure error responses.
- No stack traces in production responses.
- No internal database errors exposed to clients.
- API versioning where appropriate.
- Audit logging for sensitive actions.

Never trust:

- Client-supplied user ID.
- Client-supplied worker ID.
- Client-supplied role.
- Client-supplied completion state.
- Client-supplied subscription status.
- Client-supplied verification status.

---

# 11. CORS

Production CORS must use an allowlist.

Do not use unrestricted:

```text
Access-Control-Allow-Origin: *
```

for authenticated private APIs unless there is a deliberate, reviewed reason.

Allow only known production domains.

Example conceptual setup:

```text
https://kaamnow.example
https://admin.kaamnow.example
```

Use actual production domains during deployment.

---

# 12. Security Headers

Review appropriate headers such as:

- Content-Security-Policy.
- Strict-Transport-Security.
- X-Content-Type-Options.
- Referrer-Policy.
- Permissions-Policy.
- Frame-ancestors / clickjacking protection.
- Secure cookie attributes.

Headers must be tested against actual application behavior before enforcement.

---

# 13. Input Validation

Validate every external input.

Examples:

- Mobile number.
- OTP.
- Job description.
- Budget.
- Worker count.
- Search radius.
- Date/time.
- Chat message.
- Portfolio URL.
- Report description.
- Review.
- Admin configuration.

Prevent:

- SQL injection.
- XSS.
- HTML injection.
- Command injection.
- Malformed URLs.
- Oversized payloads.
- Invalid numeric ranges.

---

# 14. Output Encoding

User-generated content may appear in:

- Job titles.
- Job descriptions.
- Chat.
- Reviews.
- Worker profiles.
- Admin notes.

Render user content safely.

Do not inject raw HTML unless it is explicitly sanitized.

---

# 15. Rate Limiting

Rate-limit sensitive operations:

- OTP requests.
- OTP verification.
- Login.
- Password/credential operations if introduced.
- Job creation.
- Worker alerts.
- Chat message bursts.
- Reports.
- Reviews.
- Portfolio submissions.
- Admin login.
- Admin actions.
- Public API endpoints.

Use Redis where appropriate.

---

# 16. Spam / Bot Protection

Protect:

- Public forms.
- Contact forms.
- Signup/OTP endpoints.
- Job creation.
- Reports.
- Reviews.
- Public API endpoints.

Possible controls:

- Rate limits.
- Device/IP heuristics.
- CAPTCHA or challenge where justified.
- Abuse scoring.
- Temporary restrictions.

Do not create excessive friction for normal users.

---

# 17. Form Validation

Every form needs:

- Required/optional indication.
- Inline validation.
- Clear error messages.
- Correct input types.
- Maximum lengths.
- Minimum lengths where relevant.
- Loading state.
- Submit-disabled state when appropriate.
- Success state.
- Retry state.

Examples:

```text
Mobile number → valid format
Budget → valid numeric range
Worker count → positive integer
Radius → allowed values only
Portfolio URL → valid URL
Review → allowed length
```

---

# 18. Error Handling

Production errors must be user-friendly.

Never show:

- Stack traces.
- SQL errors.
- Internal service names.
- Secret values.
- Debug logs.
- File paths.

Example:

Instead of:

```text
500 psycopg2 connection exception...
```

show:

> Something went wrong. Please try again.

Provide a retry action when appropriate.

---

# 19. Custom 404 Page

Create a branded 404 page.

Include:

- KaamNow branding.
- Short explanation.
- Home button.
- Search/navigation where useful.

Example:

**This page isn't available.**

**Go to Home**

Do not leave users on a generic server error page.

---

# 20. 500 / Server Error Page

Create a production-safe server error page.

Include:

- Friendly message.
- Retry.
- Home.
- Support/contact if appropriate.

Do not expose internal diagnostics.

---

# 21. Broken Links

Before launch, test:

- Navigation.
- Footer links.
- Legal pages.
- Privacy.
- Terms.
- Contact.
- Admin navigation.
- Documentation links.
- External portfolio links.
- App download links if present.

Run automated broken-link checks where practical.

---

# 22. SEO Metadata

Public website pages should have:

- Unique title.
- Meta description.
- Canonical URL.
- Correct language metadata.
- Open Graph metadata.
- Twitter/X card metadata where applicable.
- Structured data where appropriate.

Do not index private Admin pages.

---

# 23. Social Preview Image

Create a branded social preview image.

It should contain:

**KaamNow**

Short value proposition:

**Find Local Help. Get Work Done.**

Use the final KaamNow palette:

- #141204
- #262A10
- #54442B
- #A9714B
- #E8985E

Keep text inside safe preview areas.

---

# 24. Favicon & App Icons

Provide:

- Favicon.
- Apple touch icon if web usage requires it.
- Android/app icon.
- Maskable icon where applicable.
- Correct sizes.
- Light/dark considerations where supported.

Use the final KaamNow logo and palette.

---

# 25. Sitemap

Generate:

```text
sitemap.xml
```

Include only indexable public pages.

Do not include:

- Private jobs.
- User profiles containing private data.
- Worker private dashboards.
- Admin routes.
- Chat.
- Dispute cases.
- Verification pages.
- Private account pages.

Update sitemap automatically if the public site is dynamic.

---

# 26. robots.txt

Create:

```text
robots.txt
```

Allow crawling of public marketing pages.

Disallow private application areas.

Do not rely on `robots.txt` as a security mechanism. Authentication/authorization must still protect private routes.

---

# 27. Canonical URLs

Every public SEO page should have a canonical URL.

Avoid duplicate content through:

- Query parameters.
- Alternate routes.
- Trailing slash inconsistencies.
- Multiple domain variants.

---

# 28. Mobile Responsiveness

Test:

- Small Android phones.
- Standard Android phones.
- Large Android phones.
- Tablets where relevant.
- Desktop browsers.
- Different browser zoom levels.

Check:

- No horizontal overflow.
- CTA remains accessible.
- Text does not clip.
- Cards do not overlap.
- Navigation remains usable.
- Forms remain readable.

---

# 29. Accessibility

Minimum requirements:

- Strong text/background contrast.
- Keyboard navigation on web.
- Screen-reader labels.
- Logical heading hierarchy.
- Focus indicators.
- Accessible form errors.
- Touch targets.
- No color-only status communication.
- Reduced-motion support.
- Text scaling.
- Accessible dialogs.

SOS actions must remain easy to identify.

---

# 30. Color Contrast

Verify all combinations involving:

- Pitch Black.
- Dark Khaki.
- Dark Khaki 2.
- Cinnamon Wood.
- Toasted Almond.
- Light neutral backgrounds.

Do not assume that two brand colors are automatically accessible together.

Use accessible text colors when the raw palette creates insufficient contrast.

---

# 31. Image Optimization

Before production:

- Compress images.
- Use modern formats such as WebP/AVIF where supported.
- Provide responsive sizes.
- Use lazy loading for below-the-fold images.
- Avoid oversized source images.
- Define dimensions to reduce layout shift.

Worker portfolio media should remain externally hosted where designed.

---

# 32. Alt Text

Meaningful images require descriptive alt text.

Examples:

Good:

```text
Verified plumber profile photo
```

Bad:

```text
image123.jpg
```

Decorative images should use appropriate empty alt semantics.

Do not put important UI text only inside images.

---

# 33. Page Load Performance

Measure:

- Initial load.
- Largest Contentful Paint.
- Cumulative Layout Shift.
- Interaction responsiveness.
- JavaScript bundle size.
- CSS size.
- Image weight.
- API latency.

Optimize:

- Code splitting.
- Lazy loading.
- Image optimization.
- Caching.
- CDN.
- Server rendering where appropriate.
- Database queries.
- API payload sizes.

---

# 34. Frontend Performance

For Next.js:

- Avoid unnecessary client components.
- Use server rendering where appropriate.
- Lazy-load heavy components.
- Optimize images.
- Minimize third-party scripts.
- Avoid unnecessary re-renders.
- Monitor bundle size.

For Flutter:

- Avoid unnecessary rebuilds.
- Optimize lists.
- Use image caching.
- Avoid heavy animations.
- Test on lower-end Android devices.

---

# 35. API Performance

Check:

- Response time.
- Database query time.
- N+1 queries.
- Pagination.
- Payload size.
- Cache opportunities.
- Timeout behavior.
- Retry behavior.

Never allow an API to return unbounded lists.

---

# 36. Database Performance

PostgreSQL checks:

- Required indexes.
- Foreign keys.
- Unique constraints.
- Query plans for important endpoints.
- Connection pooling.
- Slow query logging.
- Migration testing.

Important indexed fields may include:

- user_id
- worker_id
- job_id
- status
- skill
- location-related lookup fields
- created_at
- subscription status

Use actual query patterns to determine final indexes.

---

# 37. Redis / Queue Reliability

If Redis/Celery is used:

- Queue failures must be detectable.
- Jobs must not silently disappear.
- Retry policy must exist.
- Dead-letter/error handling should exist where required.
- Duplicate job processing must be considered.
- Worker alert retry must be idempotent.

---

# 38. Notification Reliability

FCM notification flows should be tested for:

- New job.
- Worker assignment.
- Job status.
- Completion request.
- Rating.
- Cancellation.
- Reopen.
- Subscription expiry.
- Admin announcement.

Notifications should deep-link to the relevant screen.

---

# 39. WebSocket / Chat Reliability

Test:

- Connect.
- Disconnect.
- Reconnect.
- Offline.
- Message retry.
- Duplicate messages.
- Message ordering.
- Authentication expiry.
- User blocked/restricted.
- Job closed.
- Reported chat.

Persist important messages server-side.

Do not rely solely on a live WebSocket connection for permanent records.

---

# 40. Authentication Security Testing

Test:

- Wrong OTP.
- Expired OTP.
- Too many attempts.
- Repeated resend.
- Session expiry.
- Logout.
- Multiple devices.
- Revoked session.
- Unauthorized API access.
- Role escalation attempt.

---

# 41. Admin Security

Creator/Admin portal requires special protection.

Check:

- Admin-only authentication.
- Role permissions.
- Session timeout.
- Sensitive action confirmation.
- Audit logs.
- Identity data restrictions.
- Admin action history.
- No direct browser access to database.
- No secrets in frontend JavaScript.

Sensitive actions should be auditable.

---

# 42. Identity Verification Security

Government IDs are highly sensitive.

Production checks:

- Restricted access.
- Encryption where stored.
- Minimum necessary retention.
- Verification audit trail.
- No public display.
- No exposure in normal API responses.
- Secure deletion/retention process.
- Admin access limited by role.

Public profile must show only:

**Identity Verified**

---

# 43. Location Privacy

Before assignment:

- Show approximate area.
- Show approximate distance.
- Do not expose exact address.

After appropriate assignment stage:

- Share exact address only where required by the product flow.

Check API responses to ensure exact location is not accidentally included in public worker discovery payloads.

---

# 44. SOS Production Checklist

Before release:

- SOS entry point works.
- Emergency flow is clearly visible.
- Location permission behavior is tested.
- Emergency call flow is tested.
- Emergency contact flow is tested.
- Android background restrictions are tested.
- Microphone permission behavior is tested.
- Audio starts only after SOS activation.
- Recording indicator is visible.
- Recording stops correctly.
- Local encrypted storage works.
- SOS session can end safely.
- SOS metadata is protected.
- Failure states are designed.

Do not claim unsupported automatic emergency/police integration.

---

# 45. Payment Boundary Checks

The UI and backend must agree that KaamNow does not act as a payment intermediary.

Verify:

- No wallet.
- No escrow.
- No platform payment balance.
- No fake transaction success state.
- No payment PIN collection.
- No UPI PIN storage.
- No payment OTP collection.
- Agreed amount can be recorded.
- Direct payment reminder can be shown.
- Financial disputes are not presented as guaranteed refunds.

---

# 46. Subscription Production Checks

Worker subscription:

**30-day free trial → ₹100/month**

Test:

- Trial activation.
- Trial countdown.
- Trial expiry.
- Active subscription.
- Renewal.
- Expired subscription.
- Existing job continuation.
- New job restriction.
- Open Jobs restriction.
- Admin price change.
- Admin trial change.
- Offers/discounts.

Do not hardcode pricing in the frontend.

---

# 47. Admin Configuration

Admin-configurable values should come from backend/API configuration where appropriate:

- Subscription price.
- Trial duration.
- Search radius.
- Radius expansion.
- Matching weights.
- Job expiry.
- Achievement thresholds.
- Notification rules.
- Promotions.
- Offers.

Changes should be validated and audited.

---

# 48. Analytics

Set up analytics only according to the documented privacy approach.

Useful product events:

- App/site visit.
- Signup started/completed.
- Job created.
- Matching started.
- Worker found.
- Worker accepted.
- Job assigned.
- Job started.
- Job done requested.
- Completion approved.
- Rating submitted.
- Job reopened.
- Dispute created.
- Subscription started.
- Subscription renewed/expired.

Do not collect unnecessary sensitive information in analytics.

Never send:

- Government ID.
- OTP.
- UPI PIN.
- Private chat content.
- Raw SOS audio.

---

# 49. Error Monitoring

Production monitoring should capture:

- Frontend exceptions.
- Backend exceptions.
- API failures.
- Background job failures.
- WebSocket failures.
- Notification failures.
- Database errors.
- Queue failures.

Error reports must not contain secrets or unnecessary personal data.

---

# 50. Logging

Logs should include useful operational information:

- Timestamp.
- Service.
- Request/correlation ID.
- Endpoint.
- Response status.
- Performance.
- Error category.

Avoid logging:

- OTP.
- Tokens.
- Passwords.
- UPI PIN.
- Government ID numbers.
- Full private chat content.
- SOS audio.

---

# 51. Audit Logs

Audit sensitive actions:

- Admin login.
- Verification decision.
- User restriction.
- Worker restriction.
- Job reassignment.
- Dispute resolution.
- Subscription configuration.
- Matching configuration.
- Promotion changes.
- Platform setting changes.
- Account deletion/deactivation.

Audit records should be protected from ordinary users.

---

# 52. Backups

PostgreSQL production backup plan:

- Automated backups.
- Defined retention.
- Restore testing.
- Off-site/independent backup where appropriate.
- Encryption.
- Access restriction.

A backup that has never been restored/tested should not be treated as verified recovery capability.

---

# 53. Disaster Recovery

Define:

- Recovery Point Objective (RPO).
- Recovery Time Objective (RTO).
- Database restore procedure.
- Service restart procedure.
- Redis recovery behavior.
- Notification retry behavior.
- Incident owner.
- Communication procedure.

Document the recovery process.

---

# 54. Deployment Environment

Separate:

```text
Development
Staging
Production
```

Never use production credentials in development.

Staging should test:

- Authentication.
- APIs.
- Database migrations.
- Notifications.
- Chat.
- Matching.
- Subscription.
- Admin actions.
- SOS flows.

---

# 55. Database Migration Safety

Before every production migration:

1. Test migration in staging.
2. Verify backup.
3. Verify rollback/recovery strategy.
4. Check data compatibility.
5. Run migration.
6. Verify application health.
7. Verify critical queries.

Never run an untested destructive migration directly on production.

---

# 56. CI/CD

Pipeline should include:

- Linting.
- Formatting.
- Unit tests.
- Integration tests.
- Build.
- Dependency checks.
- Security checks.
- Environment validation.
- Deployment.
- Post-deployment health check.

Do not automatically deploy to production from unreviewed code.

---

# 57. Dependency Security

Regularly review:

- Flutter packages.
- Dart packages.
- Python packages.
- Node packages.
- Next.js dependencies.
- System packages.

Remove unused dependencies.

Pin or constrain versions appropriately.

Review security advisories.

---

# 58. Domain & DNS

Before launch:

- Production domain configured.
- DNS verified.
- HTTPS certificate active.
- `www` behavior decided.
- Canonical domain decided.
- API domain configured.
- Admin domain configured.
- Email domain configured if required.

Avoid multiple unplanned production domains.

---

# 59. Email / Transactional Messaging

If email is used:

- Verified sending domain.
- SPF.
- DKIM.
- DMARC.
- From address.
- Reply-to address.
- Bounce handling.
- Abuse monitoring.

Do not expose internal email credentials.

---

# 60. Search Engine Indexing

Before launch:

Public:
- Marketing pages.
- Public informational pages.

Private:
- User dashboard.
- Worker dashboard.
- Admin.
- Jobs.
- Chat.
- Disputes.
- Verification.

Private routes must not be indexable and must also require authentication.

---

# 61. Social Sharing

Test:

- Open Graph title.
- Description.
- Image.
- URL.
- Mobile preview.
- Messaging-app preview.

No private user/job information should appear in public social previews.

---

# 62. Legal Footer

Public website footer should provide access to:

- Privacy Policy.
- Terms & Conditions.
- Contact/Support.
- Safety information where applicable.
- Cookie policy where applicable.

---

# 63. Support & Contact

Provide a support path.

Possible:

- Help.
- Contact.
- Report problem.
- Safety assistance information.

Support forms must have:

- Validation.
- Rate limiting.
- Confirmation.
- Reference/case ID where appropriate.

---

# 64. Content QA

Check all public copy for:

- Spelling.
- Grammar.
- Hindi/English consistency.
- Broken links.
- Incorrect prices.
- Incorrect feature claims.
- Unsupported safety claims.
- Outdated screenshots.
- Placeholder text.

Remove:

```text
Lorem ipsum
TODO
Coming soon
Test user
Example secret
```

from production-facing pages.

---

# 65. Mobile Browser QA

Even though KaamNow has a native Android app, public web pages must be tested on:

- Chrome Android.
- Safari iOS where relevant.
- Common desktop browsers.

Check:

- Navigation.
- Forms.
- Links.
- Images.
- Typography.
- Cookie/consent UI.
- Legal pages.
- Social preview.

---

# 66. Browser Compatibility

Test relevant current versions of:

- Chrome.
- Edge.
- Firefox.
- Safari.

Admin portal should be tested separately from the public marketing website.

---

# 67. Security Testing

Before launch perform:

- Dependency scan.
- Secret scan.
- Authentication testing.
- Authorization testing.
- Input validation testing.
- Rate-limit testing.
- CORS testing.
- Security-header testing.
- XSS testing.
- SQL injection testing.
- CSRF review where applicable.
- File/URL validation.
- Access-control testing.

For a public production system, perform an appropriate security review before launch.

---

# 68. File Upload Security

Where uploads exist:

- Validate file type.
- Validate file size.
- Do not trust file extension alone.
- Scan where appropriate.
- Generate safe filenames.
- Prevent executable uploads.
- Restrict access.
- Apply retention rules.

This is especially relevant to identity verification.

---

# 69. Portfolio Link Security

Google Drive portfolio links:

- Validate URL format.
- Store metadata only.
- Do not automatically download arbitrary files.
- Open external content safely.
- Treat external content as untrusted.

---

# 70. Content Moderation

Moderate:

- Job descriptions.
- Chat where platform rules require.
- Reviews.
- Reports.
- User/worker profile content.
- Promotional content.

Do not imply continuous human monitoring of ordinary chat.

---

# 71. Fake Job Protection

Provide controls against:

- Spam jobs.
- Misleading jobs.
- Duplicate jobs.
- Impossible requirements.
- Prohibited work.

Use:
- Rate limits.
- Report flow.
- Admin review.
- Reliability actions where justified.

---

# 72. No-Show Reliability

When a worker no-shows:

- User can report.
- Case can be reviewed.
- Verified reliability incidents can affect reputation.
- Repeated cases can trigger admin review.

Do not automatically penalize a user/worker based solely on an unverified accusation.

---

# 73. Completion Integrity

Backend must enforce:

```text
Worker → Job Done Request
          ↓
User Approval
          ↓
Completed
```

A frontend button must never be the only protection.

---

# 74. Duplicate Job / Assignment Protection

Backend must prevent:

- Duplicate assignments.
- Two workers simultaneously receiving the same exclusive assignment.
- Repeated completion requests.
- Duplicate ratings.
- Duplicate subscription activation.

Use transactions/idempotency where appropriate.

---

# 75. Time & Date

Production must consistently handle:

- Server time.
- User local time.
- Worker local time.
- Job scheduling.
- Notification scheduling.
- Subscription expiry.
- Trial expiry.

Store timestamps consistently and render them in the appropriate user context.

---

# 76. Location Accuracy & Privacy

Do not present approximate location as exact.

UI should distinguish:

**Approximate area**

from:

**Exact job address**

Avoid exposing coordinates in public URLs, logs, analytics, or client payloads unless necessary.

---

# 77. Accessibility of SOS

SOS must remain usable with:

- Large text.
- Screen readers.
- Reduced motion.
- Low-light/dark UI.
- One-handed interaction where practical.

Emergency action should not be hidden behind several menus.

---

# 78. Performance Budget

Define production budgets for:

- JavaScript bundle.
- CSS.
- Images.
- API response time.
- Page load.
- Core Web Vitals.
- Mobile data usage.

The exact thresholds should be finalized based on measured staging performance and target devices.

---

# 79. Production Health Checks

Create health endpoints/checks for:

- API.
- Database.
- Redis.
- Background worker.
- Notification service.
- Critical external dependencies.

Health checks must not expose secrets or internal credentials.

---

# 80. Monitoring & Alerts

Alert on:

- API error spikes.
- Authentication failures.
- Database failures.
- Queue backlog.
- Redis failures.
- Notification failures.
- High latency.
- Crash rate.
- Disk/storage issues.
- Certificate expiry.
- Backup failures.

Do not create noisy alerts for harmless events.

---

# 81. Launch-Day Checklist

Before opening production:

- [ ] Privacy Policy published.
- [ ] Terms published.
- [ ] Contact/support available.
- [ ] HTTPS verified.
- [ ] Secrets verified.
- [ ] CORS verified.
- [ ] Security headers verified.
- [ ] Authentication tested.
- [ ] RBAC tested.
- [ ] Rate limits active.
- [ ] API errors safe.
- [ ] 404 page active.
- [ ] 500 handling active.
- [ ] SEO metadata checked.
- [ ] Sitemap generated.
- [ ] robots.txt checked.
- [ ] Favicon installed.
- [ ] Social preview tested.
- [ ] Mobile responsiveness tested.
- [ ] Accessibility checked.
- [ ] Images optimized.
- [ ] Analytics verified.
- [ ] Error monitoring active.
- [ ] Database backup verified.
- [ ] Restore process tested.
- [ ] Notification flow tested.
- [ ] Chat flow tested.
- [ ] Matching flow tested.
- [ ] Subscription flow tested.
- [ ] SOS flow tested.
- [ ] Privacy/location flow tested.
- [ ] Admin permissions tested.
- [ ] Audit logging tested.
- [ ] Production environment variables verified.
- [ ] Staging-to-production deployment tested.

---

# 82. Post-Launch First 24 Hours

Monitor:

- Signup success.
- OTP delivery.
- API error rate.
- Job creation.
- Matching success.
- Worker acceptance.
- Notifications.
- Chat connection.
- Completion approval.
- Ratings.
- Subscription events.
- Server CPU/memory.
- Database load.
- Queue backlog.
- Crash/error rate.

Do not immediately make risky production changes based on a single user report without investigation.

---

# 83. Post-Launch First 7 Days

Review:

- Broken links.
- Search indexing.
- Analytics events.
- User drop-off.
- Matching failures.
- Notification failures.
- Subscription conversion.
- Admin workflow.
- Dispute handling.
- Safety reports.
- Performance.
- Device compatibility.
- Error trends.

Create fixes from observed evidence.

---

# 84. Rollback Plan

Every production release should have a rollback/recovery procedure.

Document:

- Previous stable version.
- Deployment rollback.
- Database migration recovery.
- Feature flag rollback where available.
- Cache invalidation.
- Queue handling.
- User communication if necessary.

Do not rely on “we can deploy the old version” if database changes are incompatible.

---

# 85. Incident Response

Define:

1. Detect.
2. Classify.
3. Contain.
4. Investigate.
5. Fix.
6. Verify.
7. Communicate.
8. Document.
9. Prevent recurrence.

Security incidents and safety incidents require separate escalation procedures.

---

# 86. Final Security Principle

Security must be enforced on the backend.

Never rely on:

- Hidden frontend buttons.
- Hidden routes.
- Disabled UI.
- Obfuscated IDs.
- Client-side role checks.

The server must independently validate every sensitive action.

---

# 87. Final Privacy Principle

Collect the minimum information necessary for the feature.

Especially protect:

- Government IDs.
- Exact addresses.
- Location.
- Phone numbers.
- Chat.
- SOS metadata.
- SOS audio.

Never collect or store secrets such as UPI PINs.

---

# 88. Final UX Principle

Every launch requirement should support a simple experience:

**Fast → Clear → Private → Safe → Recoverable**

The user should always know:
- What is happening.
- What the app needs.
- What will happen next.
- What information is visible.
- What action is required.

---

# 89. Definition of Production Ready

KaamNow is considered launch-ready only when:

1. Legal pages are published.
2. Production security controls are active.
3. Authentication and authorization are tested.
4. Sensitive data is protected.
5. HTTPS is enforced.
6. API and database security is reviewed.
7. Mobile and web UI are responsive.
8. Accessibility is checked.
9. SEO basics are configured.
10. Performance is measured.
11. Error monitoring is active.
12. Database backup and recovery are tested.
13. Matching and notification flows are tested.
14. Chat is reliable.
15. Subscription rules are verified.
16. Payment boundaries are accurately represented.
17. SOS behavior is tested within actual Android capabilities.
18. Admin actions are auditable.
19. No critical launch checklist item remains unresolved.

---

# 90. Final Repository Location

Recommended repository structure:

```text
kaamNow/
├── docs/
│   ├── PRD.md
│   ├── UI_UX_DESIGN.md
│   ├── TECH_STACK.md
│   └── WEB_LAUNCH_CHECKLIST.md
├── mobile/
├── backend/
├── admin/
└── README.md
```

This document should be maintained as the production-readiness checklist. Items should be checked off only after they are actually implemented and verified.

---

# 91. FINAL ARCHITECTURE ALIGNMENT — REQUIRED

This section overrides any older generic infrastructure assumptions elsewhere in this checklist.

## 91.1 Compute

- [ ] Production API runs as a containerized FastAPI application on **Google Cloud Run**.
- [ ] Cloud Run services have minimum/maximum instance settings reviewed.
- [ ] CPU/memory/concurrency settings are load-tested.
- [ ] Startup/readiness behavior is tested.
- [ ] Graceful shutdown is implemented.
- [ ] Container images are immutable and versioned by commit/release.
- [ ] Production images are vulnerability-scanned.
- [ ] No production secret is baked into the image.
- [ ] Rollback to a known-good image is tested.

## 91.2 Edge / Cloudflare

- [ ] Production DNS is managed through Cloudflare.
- [ ] TLS/HTTPS is enforced.
- [ ] WAF rules are enabled and reviewed.
- [ ] DDoS protection is enabled.
- [ ] Rate limiting exists at both edge and application levels for sensitive endpoints.
- [ ] Bot/abuse protection is configured without blocking legitimate mobile traffic.
- [ ] Origin access is restricted so the backend cannot be bypassed unintentionally.
- [ ] Cache rules never expose authenticated/private API responses.
- [ ] Admin routes receive stricter protection than public content.

## 91.3 Database — Cloud SQL PostgreSQL + PostGIS

- [ ] Production database is PostgreSQL.
- [ ] PostGIS is enabled.
- [ ] Spatial indexes exist for worker/location search.
- [ ] Database migrations are version controlled.
- [ ] No frontend connects directly to PostgreSQL.
- [ ] Application DB credentials use least privilege.
- [ ] Connection pooling is configured.
- [ ] Slow queries are monitored.
- [ ] Automated backups are enabled.
- [ ] Point-in-time recovery/appropriate recovery capability is configured where supported.
- [ ] A real restore test has been completed.
- [ ] Production database is not publicly exposed unless explicitly required and secured.
- [ ] Sensitive fields have appropriate encryption/protection and access controls.

## 91.4 Redis / Memorystore

- [ ] Redis is used for cache, ephemeral state, realtime coordination and suitable queues—not as the authoritative database.
- [ ] Redis network access is private/restricted.
- [ ] Authentication/access controls are configured.
- [ ] TTLs are defined for temporary keys.
- [ ] Cache invalidation behavior is tested.
- [ ] Application remains safe when Redis is temporarily unavailable where business correctness permits.
- [ ] No irreplaceable business record exists only in Redis.

## 91.5 Pub/Sub and Background Workers

- [ ] Pub/Sub topics and subscriptions are defined per event/workload boundary.
- [ ] Consumers are idempotent.
- [ ] Retry policies are configured.
- [ ] Dead-letter handling exists for repeatedly failing messages.
- [ ] Duplicate event delivery is expected and safely handled.
- [ ] Queue/backlog monitoring is enabled.
- [ ] Matching, notification, reminder and maintenance jobs do not unnecessarily block API requests.
- [ ] Background workers use least-privilege service credentials.

## 91.6 Object Storage — Cloudflare R2

- [ ] Binary files are not stored in PostgreSQL.
- [ ] R2 buckets are private by default.
- [ ] Signed URLs are short-lived.
- [ ] Upload authorization checks account/job ownership.
- [ ] File size and MIME/type restrictions are enforced.
- [ ] Object keys do not expose sensitive information.
- [ ] Public assets and private user files use separate access policies.
- [ ] Verification/safety-sensitive files have restricted retention and access.
- [ ] R2 credentials are stored as secrets.
- [ ] Worker portfolio uses Google Drive links where specified rather than defaulting to platform media storage.

## 91.7 FastAPI Modular Monolith

- [ ] Modules have explicit boundaries.
- [ ] API routes do not contain large amounts of business logic.
- [ ] Business logic is testable independently of HTTP.
- [ ] Database access is isolated through repositories/data-access services where appropriate.
- [ ] External integrations use adapters.
- [ ] AI calls are isolated behind the AI Orchestrator.
- [ ] Payment-provider integrations, if ever enabled, are isolated behind an adapter.
- [ ] Authorization is enforced server-side.
- [ ] All important state transitions validate the current state.

## 91.8 Authentication / Authorization

- [ ] Mobile OTP request endpoint has aggressive rate limits.
- [ ] OTP verification is protected against brute force and replay.
- [ ] Sessions can be revoked.
- [ ] Device/session metadata is controlled.
- [ ] JWT/access tokens have appropriate lifetime and rotation/revocation strategy.
- [ ] Admin authentication is stronger than ordinary user authentication.
- [ ] RBAC is enforced in backend code.
- [ ] User/worker/admin data cannot be accessed through IDOR-style requests.
- [ ] Sensitive admin actions require explicit authorization.

## 91.9 Job and Assignment Integrity

- [ ] Job state machine is enforced server-side.
- [ ] Valid transitions are explicitly defined.
- [ ] Assignment acceptance is atomic/idempotent.
- [ ] Two workers cannot both win a single-worker assignment.
- [ ] Duplicate API requests do not duplicate assignments.
- [ ] Worker cannot directly mark a job COMPLETED.
- [ ] Completion requires user approval.
- [ ] Reopen flow is protected and auditable.
- [ ] No-show/cancellation flows update appropriate reputation/reliability signals.
- [ ] Job status history is retained for audit/debugging.

## 91.10 Matching and PostGIS

- [ ] Required skill is determined/validated before matching.
- [ ] Worker eligibility is checked before ranking.
- [ ] Availability is checked.
- [ ] Subscription eligibility is checked before accepting new work.
- [ ] Distance is calculated using PostGIS.
- [ ] Radius options are limited to configured values: 5/10/15/20 km.
- [ ] Radius expansion has explicit limits and audit events.
- [ ] Approximate location is exposed before assignment.
- [ ] Exact address is protected until the permitted workflow stage.
- [ ] Matching does not rely on an opaque AI-only decision.
- [ ] Match explanations can be reproduced from stored eligibility/ranking inputs.

## 91.11 Chat / WebSocket

- [ ] Chat is private to the correct job participants.
- [ ] WebSocket authentication is enforced.
- [ ] WebSocket authorization checks job membership.
- [ ] PostgreSQL remains the authoritative message store.
- [ ] Redis is used only for realtime coordination/presence as designed.
- [ ] Reconnect behavior is tested.
- [ ] Duplicate messages/events are handled safely.
- [ ] Message rate limits are implemented.
- [ ] Abuse/report controls exist.
- [ ] Attachments use signed object-storage access.

## 91.12 Notifications / FCM

- [ ] Firebase Cloud Messaging production credentials are protected.
- [ ] Device tokens are stored securely.
- [ ] Invalid/expired tokens are removed or disabled.
- [ ] Notification jobs are idempotent.
- [ ] Critical in-app events remain available even if push delivery fails.
- [ ] Notification preferences are respected.
- [ ] Sensitive information is not unnecessarily exposed in notification previews.
- [ ] Notification retries and failures are observable.

## 91.13 Maps / Location

- [ ] Google Maps API keys are restricted by application/platform where applicable.
- [ ] Server-side map/geocoding credentials are never shipped in the mobile binary.
- [ ] Geospatial data access follows least privilege.
- [ ] Approximate location is used before assignment.
- [ ] Exact address is not included in worker discovery responses.
- [ ] Location retention/deletion policy is implemented.
- [ ] Permission denial is handled gracefully.
- [ ] Mock/spoofed or stale location behavior has appropriate safeguards for the product's risk level.

## 91.14 AI Orchestration

- [ ] AI is called through the backend, not directly from the mobile client.
- [ ] Provider/model credentials are server-side secrets.
- [ ] AI output is schema validated.
- [ ] Unsupported categories/skills are rejected or mapped safely.
- [ ] AI failures have deterministic/manual fallback.
- [ ] AI does not bypass authorization or payment rules.
- [ ] Government IDs, OTPs, payment secrets, raw SOS audio and unnecessary exact location are not sent to external models.
- [ ] Prompt/model version is traceable for debugging where appropriate.
- [ ] AI latency/timeouts do not block the entire job-creation experience indefinitely.

## 91.15 Payment Boundary

- [ ] Product UI does not imply KaamNow holds customer money.
- [ ] No internal wallet/escrow balance exists unless the architecture is explicitly changed and legally reviewed.
- [ ] User-worker payment is direct through UPI/QR or another mutually agreed method.
- [ ] Platform does not store UPI PIN/OTP.
- [ ] Platform does not guarantee refunds or financial recovery.
- [ ] Agreed amount can be recorded/displayed.
- [ ] Inspection-based pricing is represented as proposal → user approval → agreed amount.
- [ ] Additional work requires approval before becoming the agreed amount.
- [ ] Financial dispute UI clearly states the platform's coordination/review boundary.
- [ ] If an actual payment gateway is later introduced for subscription billing, it must be isolated from job-payment custody and implemented as a separate audited integration.

## 91.16 Worker Subscription

- [ ] Worker price is server-configured.
- [ ] Current product value is ₹100/month.
- [ ] Current free trial is 30 days.
- [ ] Pricing/trial values are not hard-coded into the client.
- [ ] Expired workers cannot accept new jobs/Open Jobs.
- [ ] Existing/ongoing jobs remain manageable according to product rules.
- [ ] Renewal updates entitlement server-side.
- [ ] Subscription state is cached only as a derived value, never as the sole source of truth.
- [ ] Admin changes to pricing/plans are audited.

## 91.17 Identity Verification

- [ ] Supported government IDs are processed only through restricted verification workflows.
- [ ] Public profile exposes only verification status.
- [ ] ID numbers are never returned by public profile APIs.
- [ ] Admin access to identity data is role restricted.
- [ ] Verification access is audited.
- [ ] Retention/deletion rules are documented.
- [ ] Verification files are stored privately with signed access if storage is required.

## 91.18 SOS / Safety

- [ ] SOS is available to both users and workers.
- [ ] Emergency trigger behavior is tested on supported Android versions/devices.
- [ ] The app does not secretly record during normal operation.
- [ ] Audio recording starts only after SOS activation.
- [ ] Android microphone/background restrictions are respected.
- [ ] Audio is encrypted and stored locally by default.
- [ ] Backend stores protected SOS metadata rather than normal cloud audio by default.
- [ ] Emergency contact/call flow is tested.
- [ ] The product does not claim guaranteed automatic police dispatch without an actual integration.
- [ ] SOS location access is time-bounded and purpose-limited.
- [ ] SOS cancellation/end flow is tested.
- [ ] Safety incident reports are auditable.
- [ ] SOS failures degrade safely and provide the user with available emergency-call/contact options.

## 91.19 Admin / Creator Portal

- [ ] Admin portal is a separate Next.js + TypeScript application.
- [ ] Admin API is protected by strict RBAC.
- [ ] No direct browser-to-database access.
- [ ] Admin sessions are protected.
- [ ] High-risk actions require appropriate confirmation.
- [ ] User/worker suspension actions are audited.
- [ ] Verification decisions are audited.
- [ ] Dispute resolutions are audited.
- [ ] Subscription configuration changes are audited.
- [ ] Promotion/ad changes are audited.
- [ ] Matching configuration changes are audited.
- [ ] Audit records cannot be silently modified by ordinary admins.

## 91.20 Observability

- [ ] OpenTelemetry traces are enabled for API/background workloads.
- [ ] Structured logs include correlation/request IDs.
- [ ] Sentry is configured for production errors.
- [ ] Metrics exist for API latency/error rate.
- [ ] Database saturation/slow queries are monitored.
- [ ] Redis health is monitored.
- [ ] Pub/Sub backlog and failed messages are monitored.
- [ ] Matching success/failure and time-to-assignment are measurable.
- [ ] Notification delivery failures are measurable.
- [ ] WebSocket connection health is measurable.
- [ ] Critical SOS processing errors generate alerts.
- [ ] Secrets, OTPs, tokens and raw SOS audio are never logged.

## 91.21 CI/CD

- [ ] GitHub Actions runs linting.
- [ ] Unit tests run on every protected branch.
- [ ] Integration tests run before production deployment.
- [ ] Dependency vulnerability scanning is enabled.
- [ ] Container image scanning is enabled.
- [ ] Infrastructure plan is reviewed before production changes.
- [ ] Production deployment requires protected environment approval where appropriate.
- [ ] Database migrations are handled as a controlled deployment step.
- [ ] Smoke tests run after deployment.
- [ ] Rollback procedure is documented and tested.

## 91.22 Terraform / Infrastructure as Code

- [ ] Cloud Run resources are defined as code.
- [ ] Cloud SQL resources/configuration are defined as code where appropriate.
- [ ] Redis/Memorystore configuration is defined as code.
- [ ] Pub/Sub topics/subscriptions are defined as code.
- [ ] Service accounts/IAM are defined as code.
- [ ] Cloudflare DNS/WAF configuration is tracked where supported.
- [ ] Environment separation exists for staging and production.
- [ ] Terraform state is protected and not committed to the repository.
- [ ] State access is restricted.
- [ ] Infrastructure drift is periodically reviewed.

## 91.23 Secrets

Never commit:

- [ ] JWT secrets.
- [ ] OTP provider credentials.
- [ ] FCM credentials.
- [ ] Google Maps server credentials.
- [ ] AI API keys.
- [ ] R2 access keys.
- [ ] Redis credentials.
- [ ] PostgreSQL passwords.
- [ ] Cloud service account private keys.
- [ ] Admin credentials.
- [ ] Any payment-provider secret.
- [ ] Any signing/encryption key.

## 91.24 Production Smoke Test

Before public launch, execute a complete end-to-end test:

```text
User OTP Login
      ↓
Create Job
      ↓
AI Requirement Understanding
      ↓
Dynamic Questions
      ↓
Post Job
      ↓
PostGIS Matching
      ↓
Worker Notification
      ↓
Worker Accepts
      ↓
Assignment
      ↓
Private Chat
      ↓
Worker Starts
      ↓
Job Done Request
      ↓
User Approves
      ↓
Completed
      ↓
Two-way Rating
      ↓
History / Reputation Update
```

Also test:

```text
Cancellation
Rejection
No Worker
Radius Expansion
Worker No-show
User Reopen
Additional Work Proposal
Completion Dispute
Chat Report
Subscription Expiry
SOS Activation
Network Failure
Duplicate Requests
Notification Failure
Database Restore
Rollback
```

---

# 92. FINAL ARCHITECTURE CONSISTENCY RULE

The following architecture is the source of truth for this launch checklist:

```text
Flutter Mobile
      │
Cloudflare Edge
      │
GCP Cloud Run
      │
FastAPI Modular Monolith
      │
 ┌────┼───────────────┐
 ▼    ▼               ▼
SQL   Redis          Pub/Sub
+GIS
 │                     │
 ▼                     ▼
R2                Background Workers

External:
FCM • Google Maps • OTP/SMS • Optional AI

Admin:
Next.js + TypeScript

DevOps:
GitHub Actions • Terraform/OpenTofu • OpenTelemetry • Sentry/Grafana
```

Any older checklist item that assumes AWS-specific services, a self-managed Kubernetes cluster, Kafka, MongoDB as the primary database, direct frontend-to-database access, platform-held job payments, or cloud-stored SOS audio should be treated as obsolete unless the architecture is explicitly changed and this document is updated.

---

# 93. FINAL GO-LIVE GATE

KaamNow should not be considered production-ready merely because the website loads.

All of the following must be green:

- [ ] Application security
- [ ] Authentication/authorization
- [ ] Database security
- [ ] PostGIS matching
- [ ] Assignment concurrency
- [ ] Chat/realtime
- [ ] Notifications
- [ ] Subscription entitlement
- [ ] Payment boundary
- [ ] Identity verification
- [ ] Location privacy
- [ ] SOS safety behavior
- [ ] AI fallback
- [ ] Admin RBAC
- [ ] Audit logs
- [ ] Backups and restore
- [ ] Monitoring and alerting
- [ ] CI/CD and rollback
- [ ] Legal pages
- [ ] Accessibility
- [ ] Mobile responsiveness
- [ ] SEO/public web requirements
- [ ] Load/performance testing
- [ ] Incident response
- [ ] End-to-end smoke testing

**Final rule:** do not launch on a “works on my device” basis. Launch only after the production environment, security controls, recovery procedures and critical user/safety workflows have been tested.
