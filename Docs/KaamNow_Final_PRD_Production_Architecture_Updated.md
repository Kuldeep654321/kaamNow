# KaamNow — Final Product Requirements Document (Production Architecture Aligned)

**Version:** 2.0

**Status:** Final / Production Architecture Aligned

Immediate Local Work

Final Product Requirements Document (PRD)

Version: 2.0

Status: Final / Production Architecture Aligned

Product Type: Agentic Local Work Discovery, Matching & Coordination Platform

Interfaces: Mobile Application + Creator/Admin Web Portal

## 1. Product Overview

## 1.1 Product Vision

Immediate Local Work is an agentic local-work coordination platform that allows users to describe a legitimate local task instead of manually searching through worker listings.

The system understands the user's requirement, identifies the required skill, dynamically collects relevant details, finds suitable nearby workers, alerts them, manages assignment, enables communication, coordinates the work, verifies completion and builds reputation.

“Don't search for a worker. Just tell us what needs to be done.”

## 2. Problem Statement

Finding reliable local workers is often fragmented and time-consuming.

- Search for workers manually.

- Decide which category to select.

- Call multiple workers.

- Explain the same problem repeatedly.

- Check worker availability.

- Negotiate prices.

- Share location.

- Deal with cancellations and no-shows.

- Determine worker reliability.

Workers commonly face difficulty finding nearby jobs, dependence on personal contacts, irregular job opportunities, difficulty building reputation, limited digital visibility and difficulty managing multiple skills.

Immediate Local Work creates an intelligent coordination layer between users and local workers.

## 3. Product Objectives

Allow users to describe any legitimate local work requirement.

Understand the requirement automatically.

Identify required skills.

Dynamically collect relevant work information.

Find suitable nearby workers.

Prioritize workers using multiple matching signals.

Give new workers opportunities through Open Jobs.

Protect user and worker privacy.

Provide a complete structured job lifecycle.

Enable direct user-to-worker payment.

Build reputation from verified completed work.

Provide emergency safety assistance.

Provide a creator/admin control system.

Monetize through worker subscriptions instead of transaction commission.

## 4. Product Scope

Mobile Application
        +
Agentic Backend
        +
Creator/Admin Web Portal

The mobile application supports both User Mode and Worker Mode through the same account.

## 5. User Types

## 5.1 User

A person who needs local work completed.

- Cleaning

- Electrical work

- Plumbing

- Painting

- Cooking

- Pet care

- Vehicle washing

- Appliance repair

- Moving assistance

- Other legitimate local work

## 5.2 Worker

A local service provider who can offer one or multiple skills. A worker is not restricted to a single profession.

## 5.3 Creator/Admin

- Users

- Workers

- Verification

- Jobs

- Reports

- Disputes

- Subscriptions

- Offers

- Promotions

- Matching configuration

- Analytics

- Platform settings

## 6. Account Architecture

ONE ACCOUNT
                        |
             +----------+----------+
             |                     |
         USER MODE             WORKER MODE
             |                     |
       Create Jobs           Accept Jobs
       Hire Workers          Manage Skills
       Track Jobs            Availability
       Rate Workers           Complete Jobs

A user does not need another account to become a worker.

## 7. Authentication

- Mobile number login

- OTP verification

- Secure session management

- Login/logout

- Account recovery

- One mobile number → one account

The mobile number is not automatically exposed to another user or worker.

## 8. Profile System

## User Profile

- Name

- Profile picture

- Mobile number

- General location/area

- Identity verification status

- Ratings/reputation

- Relevant completed jobs

- Reliability information where applicable

## Worker Profile

- Name

- Profile picture

- Skills

- Service areas

- Availability

- Rating

- Completed jobs

- Achievements

- Identity verification status

- Verified Worker status

- Portfolio links

- Subscription status

## 9. Identity Verification

Users and workers can provide Aadhaar, PAN or another supported government-issued identity document.

## Privacy

- Government ID is never publicly displayed.

- Government ID is not visible to other users/workers.

- Access is restricted.

- Sensitive information is securely stored.

- Retention follows minimum-necessary principles.

- Public profiles display only verification status.

Identity badge: Identity Verified. This is separate from worker service verification.

## 10. Worker Verification

A worker receives the Verified Worker status after achieving 3 or more user-approved completed jobs.

Government identity verification does not automatically create the Verified Worker badge.

## 11. Requirement Entry

The user describes the requirement using text.

Example: “Mere ghar ki deep cleaning karwani hai.”

User Requirement
       ↓
Need Understanding
       ↓
Work Category
       ↓
Required Skill
       ↓
Dynamic Questions
       ↓
Structured Job
       ↓
User Confirmation

The user does not need to know the correct service category.

## 12. Need Understanding

- Work category

- Required skill

- Sub-skill

- Work type

- Number of workers required

- Deadline

- Budget relevance

- Inspection requirement

- Other necessary attributes

## 13. Dynamic Work Specification

Questions are generated according to the detected work.

## Example: Cleaning

User: “Ghar saaf karwana hai.”

System asks: What needs cleaning?

- Room

- Bathroom

- Kitchen

- Full House

- Windows

- Other

Then: Cleaning type?

- Basic

- Deep Cleaning

- Dusting

- Floor Cleaning

- Complete Cleaning

- Other

The same principle applies to electrician, plumber, painting, cooking, pet care, AC repair, appliance repair and other services.

## 14. Job Confirmation

Work: Deep House Cleaning
Area: Vijay Nagar
Date: 22 September
Time: 10:00 AM
Budget: ₹800
Workers Required: 1
Search Radius: 10 KM

User selects Confirm Job. Matching begins after confirmation.

## 15. Deadline

Deadline is optional. User can select a date/time or no deadline.

- Worker availability

- Matching

- Notifications

- Reminders

- Expiry

## 16. Budget System

## Budget-Based Work

- Cleaning

- Car washing

- Bike washing

- Painting

- Cooking

- Pet care

- Art/drawing

- Small assistance

## Inspection-Based Work

- Electrician

- Plumber

- AC repair

- Appliance repair

Job Posted
    ↓
Worker Assigned
    ↓
Inspection
    ↓
Worker Proposes Price
    ↓
User Approves
    ↓
Work Begins

## 17. Search Radius

- 5 km

- 10 km

- 15 km

- 20 km

5 KM
 ↓
10 KM
 ↓
15 KM
 ↓
20 KM
 ↓
25 KM...

Expansion follows configurable platform limits.

## 18. Location Privacy

## Before Assignment

- Approximate area

- Approximate distance

- Exact address hidden

## After Assignment

Exact location can be shared after appropriate user approval.

## 19. Smart Matching Engine

Required skill

Active status

Availability

Distance

Rating

Relevant experience

Similar completed jobs

JOB
              |
      +-------+--------+
      ↓       ↓        ↓
    Skill Availability Distance
      |       |        |
      +-------+--------+
              ↓
            Rating
              ↓
          Experience
              ↓
      MATCHING ENGINE
              ↓
       Ranked Workers

Matching weights are configurable.

## 20. Worker Eligibility

- Required skill is available.

- Worker is active.

- Worker is available during the required time.

- Worker is inside the current radius.

- Subscription permits new-job acceptance.

- Worker is not restricted.

- Worker does not have a conflicting assignment.

## 21. Smart Matching Explanation

Why this job matches you: Required cleaning skill; 3.2 km away; available tomorrow; similar jobs completed.

## 22. Worker Job Alert

NEW JOB

Deep House Cleaning
Distance: 3.4 KM
Date: Tomorrow
Time: 10:00 AM
Budget: ₹800
Workers Required: 1

[ ACCEPT ]   [ REJECT ]

## 23. Smart Retry

Worker Group 1
      ↓
   REJECT
      ↓
Worker Group 2
      ↓
   REJECT
      ↓
Worker Group 3

The system continues with the next eligible workers.

## 24. Open Job Posting

User can select Open Job Posting. The job becomes available to relevant workers.

- Increase worker discovery

- Improve job fulfillment

- Give new workers opportunities

- Reduce dependence on existing reputation

## 25. Open Job Filters

- Distance

- Work type

- Required skill

- Budget

- Date

- Time

## 26. Multiple Worker Jobs

A job can require multiple workers.

Required Workers: 3

Worker A → Assigned
Worker B → Assigned
Worker C → Assigned

Matching continues until the required count is fulfilled.

## 27. Job Assignment

- Assignment is created.

- Position is reserved.

- Other workers cannot take that position.

- Notifications are sent.

- Matching stops for that position.

For multiple-worker jobs, matching continues for remaining positions.

## 28. In-App Chat

- Work details

- Timing

- Price discussion

- Additional requirements

- Coordination

## Privacy

- Phone number is not automatically exposed.

- Chat is protected.

- Automated safety/moderation checks may apply.

- Authorized review may occur during reports/disputes.

Normal chats are not continuously human-monitored.

## 29. Price Negotiation

The platform does not enforce a universal price. User and worker can discuss and agree on pricing. The final agreed amount is recorded against the job.

## 30. Additional Work

Worker proposes additional amount
             ↓
        User reviews
             ↓
        User approves
             ↓
       Final amount updated

## 31. Payment & Financial Boundary

The platform is a job coordination platform, not a payment intermediary or escrow service.

## Direct Payment

Payment occurs directly from User to Worker.

- UPI

- QR

- Other mutually agreed direct payment methods

## Platform Responsibilities

- Display the agreed amount.

- Record the final agreed amount.

- Provide payment-related reminders.

- Maintain payment-related job metadata where required.

## Platform Does Not

- Hold worker money.

- Transfer money between user and worker.

- Operate an escrow wallet.

- Take transaction commission.

- Store UPI PIN/OTP.

- Guarantee payment.

- Guarantee refunds.

- Automatically recover money from either party.

The external payment method remains the authoritative mechanism for the actual financial transaction.

## 32. Job State Machine

DRAFT
  ↓
POSTED
  ↓
MATCHING
  ↓
ALERT_SENT
  ↓
ACCEPTED
  ↓
ASSIGNED
  ↓
CHAT / COORDINATION
  ↓
ON_THE_WAY
  ↓
ARRIVED
  ↓
IN_PROGRESS
  ↓
DONE_REQUESTED
  ↓
APPROVED
  ↓
COMPLETED
  ↓
RATING

POSTED → CANCELLED
POSTED → EXPIRED
ACCEPTED → NO_SHOW
DONE_REQUESTED → DISPUTED → ADMIN REVIEW → RESOLUTION

## 33. Job Completion

Worker cannot directly finalize a job as completed. Worker selects Job Done. The user receives a completion request.

- Approve

- Raise Issue/Dispute

COMPLETED
   ↓
Completed Count +1
   ↓
Rating
   ↓
Reputation Update
   ↓
Achievement Progress
   ↓
Worker History Update

## 34. Reopen Job

- Worker cancels

- Worker becomes unavailable

- Worker does not show up

- Worker cannot complete the assignment

REOPEN
  ↓
SMART MATCHING
  ↓
NEXT ELIGIBLE WORKERS

## 35. Job Expiry

- New acceptance is disabled.

- Relevant alerts stop.

- Job becomes expired.

- User receives notification.

- Relevant workers receive status notification.

## 36. Worker No-Show

- User can report no-show.

- Incident can be reviewed.

- Reliability impact can be applied when appropriately verified.

- Repeated incidents can trigger admin review.

## 37. User Fake/Misleading Job

- Repeated fake or misleading behaviour may affect reliability.

- May trigger report review.

- May trigger administrative action.

Unverified accusations should not automatically destroy reputation.

## 38. Two-Way Rating

## User → Worker

- Rating

- Review

## Worker → User

- Rating

- Review

Only eligible completed jobs contribute to normal reputation.

## 39. Reputation System

## Worker

- Completed jobs

- User ratings

- Reliability

- No-show history

- Relevant experience

## User

- Completed jobs

- Worker feedback

- Verified reliability incidents

The exact calculation is configurable.

## 40. Worker Achievements

- Verified Worker — 3+ user-approved completed jobs

- Highly Rated — configured rating threshold

- Quick Response — configured response-performance threshold

- 50 Jobs Completed — 50 approved completed jobs

## 41. Worker Availability

- Active / Inactive status

- Date

- Start time

- End time

Matching uses this information.

## 42. Worker Portfolio

The application does not store worker media directly.

Workers can provide a Google Drive portfolio link.

- URL

- Title

- Description

- Metadata

Users open the portfolio externally. Before/after proof can also use Google Drive links.

## 43. Worker Subscription

## First 30 Days

Completely Free. All worker features are available.

## After 30 Days

₹100/month.

## Expiry

- Profile remains.

- Existing/ongoing jobs can continue.

- New jobs cannot be accepted.

- New Open Jobs cannot be accepted.

## Renewal

Full worker access returns after renewal.

## 44. Subscription Administration

- Subscription price

- Trial duration

- Plans

- Offers

- Deals

- Discounts

Settings are database/API driven so changes do not require app redeployment.

## 45. Smart Reminders

- Scheduled job reminder

- Pending completion approval

- Pending rating

- Upcoming job

- Subscription expiry

- Reopened job

- Important status changes

## 46. Notification System

## User Notifications

- Job posted

- Matching started

- Worker found

- Worker assigned

- Worker on the way

- Worker arrived

- Work started

- Job done request

- Completion

- Rating request

- Cancellation

- Reopen

- Dispute

- Payment-related reminder

- Admin announcement

## Worker Notifications

- New job

- Assignment

- Job timing

- User cancellation

- Reopened job

- Rating

- Subscription expiry

- Admin announcement

## 47. Hindi + English

The application supports Hindi and English. UI, notifications and system messages should be localization-ready.

## 48. Emergency SOS & Safety Assistance

Emergency safety is available to both Users and Workers.

- Misbehavior

- Harassment

- Threats

- Physical confrontation

- Home-visit danger

- Medical emergency

- Other immediate safety situations

## 49. SOS Activation

The intended emergency interaction includes a rapid hardware-button gesture such as power button pressed 3–4 times.

Actual detection depends on Android/device capabilities and system restrictions. Where supported, the gesture triggers the SOS workflow. The application must not claim universal interception of power-button presses by a normal third-party Android app.

## 50. SOS Workflow

Emergency Trigger
       ↓
SOS Activated
       ↓
Location Captured
       ↓
Emergency Alert
       ↓
Emergency Contact / Emergency Call Flow
       ↓
SOS Safety Session

An appropriate accidental-trigger cancellation mechanism should be provided where technically possible.

## 51. Emergency Location

- Current location is captured.

- Timestamp is recorded.

- Location is included in the emergency workflow.

- Configured trusted contacts/authorized emergency mechanisms can receive the alert.

- SOS session status is tracked.

## 52. Emergency Calling

- Emergency calling

- Configured trusted emergency contact

- Appropriate police/emergency assistance flow

The system should not claim guaranteed automatic connection to the nearest police station unless an actual integration exists.

## 53. SOS Audio Evidence

After SOS activation, emergency audio recording can automatically start.

- No recording during normal application usage.

- Recording begins only after SOS activation.

- Recording follows Android microphone/background restrictions.

- Recording is stored locally on the device.

- Audio should be encrypted.

- Recording stops when the SOS session ends/cancels or configured recording conditions are reached.

## 54. SOS Audio Privacy

- Avoid normal cloud media storage by default.

- Store audio locally.

- Restrict application access.

- Encrypt stored audio.

- Provide appropriate deletion/export controls.

- Follow applicable privacy and recording requirements.

## 55. SOS Session Data

- SOS ID

- Account ID

- Timestamp

- Location

- Trigger type

- Emergency status

- Local audio reference

- Incident/report status

## 56. Safety Reporting

- Misbehavior

- Harassment

- Threats

- Physical confrontation

- Abuse

- Fake jobs

- No-show

- Safety concerns

- Other inappropriate behaviour

Reports enter the moderation/dispute system.

## 57. Payment & Dispute Boundary

The platform separates financial transactions from platform dispute handling.

## Financial Boundary

- The platform does not hold funds.

- The platform does not process payments.

- The platform does not act as escrow.

- The platform does not guarantee refunds.

- The platform does not guarantee payment recovery.

- The platform does not take transaction commission.

User and worker are responsible for completing agreed payment directly.

## Platform Dispute Boundary

- Worker no-show

- User no-show

- Fake/misleading job

- Misbehavior

- Harassment

- Safety incidents

- Job cancellation

- Reassignment

- Completion disagreement

- Platform assignment problems

- Chat/coordination problems

- Policy violations

## Financial Disagreement

Example: user and worker disagree whether the final amount should be ₹800 or ₹1,200.

The platform can review the agreed amount recorded in the job, relevant in-app chat, additional-work approvals, job history and reports/evidence.

The platform does not automatically hold money, refund the user, transfer money to the worker, recover money or guarantee a financial outcome.

Admin may take platform-level action such as warning, restriction, suspension, reassignment, case closure or reputation/reliability action where justified.

## 58. Data & Privacy Architecture

## Government ID

Private and restricted.

## Mobile Number

Used for authentication and not automatically exposed.

## Location

Approximate before assignment and exact after appropriate assignment/approval.

## Chat

Private and protected.

## Payment

Direct user-to-worker payment without unnecessary payment credential storage.

## SOS Audio

Encrypted local storage by default.

## Account

Users should have appropriate account controls including deactivation and deletion workflows.

## 59. Creator/Admin Portal

A separate web application for platform administration.

- Dashboard

- Users

- Workers

- Verification

- Jobs

- Reports

- Disputes

- Subscriptions

- Offers

- Ads / Promotions

- Notifications

- Analytics

- Matching Settings

- Platform Settings

- Moderation

## 60. User Management

- Search users

- View profiles

- View relevant job history

- View reports

- Manage account restrictions

- Review verification

- Handle moderation cases

## 61. Worker Management

- Search workers

- View skills

- View availability

- View completed jobs

- View ratings

- View achievements

- View subscription status

- Review identity verification

- Handle reports

- Manage restrictions

## 62. Verification Management

ID Submitted
     ↓
Verification Process
     ↓
Verified / Rejected / Review Required
     ↓
Identity Status Updated

The exact verification mechanism may use an appropriate verification provider or controlled administrative verification.

## 63. Job Administration

- Active jobs

- Matching jobs

- Assigned jobs

- Completed jobs

- Cancelled jobs

- Expired jobs

- Reopened jobs

- Disputed jobs

- No-show cases

## 64. Dispute Management

Report / Dispute
       ↓
Case Created
       ↓
Evidence Collected
       ↓
Relevant Job / Chat Reviewed
       ↓
Admin Resolution
       ↓
Case Closed

Access to private information must be restricted to authorized cases/personnel.

## 65. Reports & Moderation

- User reports

- Worker reports

- Safety incidents

- Fake-job reports

- No-show reports

- Abuse reports

- Disputes

Possible administrative actions: Warning, Restriction, Suspension, Verification Review, Case Closure.

Sensitive administrative actions should be auditable.

## 66. Ads & Promotions

- Promotional banners

- Sponsored listings

- Offers

- Deals

- Announcements

- Campaigns

Promotional content must clearly display Sponsored / Advertisement.

## 67. Analytics Dashboard

## Users

- Total users

- Active users

- New users

## Workers

- Total workers

- Active workers

- Verified workers

- Active subscriptions

## Jobs

- Jobs posted

- Jobs matched

- Jobs assigned

- Jobs completed

- Jobs cancelled

- Jobs expired

- Jobs reopened

## Matching

- Match success rate

- Average matching time

- Acceptance rate

- Rejection rate

- Radius expansion frequency

## Reliability

- No-show rate

- Cancellation rate

- Dispute rate

- Average rating

## Revenue

- Active subscriptions

- Trial conversions

- Subscription revenue

## 68. Admin Matching & Platform Configuration

## Matching

- Skill-match weighting

- Distance weighting

- Availability weighting

- Rating weighting

- Experience weighting

- Search radius

- Radius expansion

- Smart retry behaviour

## Platform

- Subscription price

- Trial duration

- Job expiry

- Achievement thresholds

- Notification rules

- Moderation rules

- Offers

- Promotions

- Language/configuration

All configurable values should be database/API driven.

## 69. System & Backend Architecture

MOBILE APP
                        │
                        ▼
                    API LAYER
                        │
          ┌─────────────┴─────────────┐
          │                           │
        AUTH                    APPLICATION LAYER
                                      │
       ┌────────────┬────────────┬────┴────────────┐
       ↓            ↓            ↓                 ↓
   JOB SERVICE   MATCHING    NOTIFICATION       CHAT
       │          ENGINE        SERVICE         SERVICE
       │            │              │               │
       ↓            ↓              ↓               ↓
  STATE MACHINE  WORKER       PUSH / BUZZER    MESSAGES
                 SEARCH
       │
       ├───────────────┬──────────────┐
       ↓               ↓              ↓
  REPUTATION      SUBSCRIPTION     SAFETY / SOS
       │               │              │
       └───────────────┴──────────────┘
                       │
                       ▼
                    DATABASE
                       │
                       ▼
                CREATOR PORTAL

## 70. Logical Backend Services

## Authentication Service

- OTP

- Sessions

- Account identity

## Profile Service

- Users

- Workers

- Skills

- Availability

- Profiles

## Job Service

- Job creation

- Dynamic specifications

- Assignments

- State transitions

- Reopening

- Expiry

## AI / Need Understanding Service

- Requirement understanding

- Category detection

- Skill detection

- Dynamic questions

- Structured specifications

## Matching Service

- Eligibility

- Ranking

- Radius expansion

- Smart retry

- Matching explanation

## Notification Service

- Worker buzzer

- Push notifications

- Reminders

- Status notifications

## Chat Service

- Private conversations

- Messages

- Safety/moderation signals

## Reputation Service

- Ratings

- Reviews

- Reliability

- Achievements

## Subscription Service

- Trial

- Subscription

- Expiry

- Renewal

- Offers

## Safety Service

- SOS

- Safety incidents

- Reports

- Emergency session data

## Admin Service

- Creator portal

- Moderation

- Configuration

- Analytics

## 71. Core Database Entities

User
WorkerProfile
Skill
WorkerSkill
Availability
IdentityVerification

Job
JobRequirement
JobAssignment
JobWorker
JobStatusHistory
JobPrice

Chat
ChatMessage

Rating
Review
Report
Dispute

Achievement
WorkerAchievement
PortfolioLink

Subscription
SubscriptionPlan

Notification

SOSSession
SOSLocation
SOSAudioReference

AdminUser
AdminAction

Promotion
Banner
PlatformSetting

## 72. Core Relationships

User
 ├── Profile
 ├── Identity Verification
 ├── Jobs
 ├── Ratings
 ├── Reports
 └── SOS Sessions

User
 └── Worker Profile
       ├── Skills
       ├── Availability
       ├── Portfolio
       ├── Subscription
       ├── Achievements
       ├── Job Assignments
       └── Ratings

## 73. Core Job Data

- Job ID

- User ID

- Requirement text

- Detected category

- Required skills

- Dynamic specifications

- Approximate location

- Exact location

- Location-sharing status

- Budget

- Final agreed price

- Deadline

- Required worker count

- Assigned worker count

- Search radius

- Current status

- Created timestamp

- Updated timestamp

- Expiry timestamp

## 74. Job Audit Trail

- Job created

- Matching started

- Worker alerted

- Worker accepted

- Worker rejected

- Assignment created

- Worker cancelled

- Worker no-show

- Job reopened

- Job done requested

- User approved

- Job completed

- Rating submitted

- Report created

- Admin action

- Subscription changed

This provides traceability for disputes and system debugging.

## 75. Security Architecture

- Secure authentication

- Role-based access control

- Least-privilege access

- Encryption of sensitive data

- Restricted government-ID access

- Location access control

- Protected chat

- Secure audit logs

- Encrypted SOS audio

- Appropriate data retention

- Account deletion/deactivation workflows

## 76. Important Edge Cases

- No worker found

- Worker rejection

- All workers reject

- Radius expansion

- Worker cancellation

- Worker no-show

- User cancellation

- Job expiry

- Multiple workers required

- Worker already busy

- Worker subscription expired

- User disputes completion

- Worker disputes user behaviour

- Price disagreement

- Additional work

- Worker unavailable

- Location permission denied

- Notification permission denied

- Microphone permission denied

- Network interruption

- Duplicate job submission

- Duplicate assignment

- SOS trigger limitations caused by device/OS restrictions

## 77. User Experience Principles

The user should not need to understand the internal marketplace.

“I need this work done.”
          ↓
System understands
          ↓
Relevant questions
          ↓
Job confirmed
          ↓
Suitable workers found
          ↓
Workers alerted
          ↓
Worker assigned
          ↓
Chat & coordination
          ↓
Work executed
          ↓
Worker requests completion
          ↓
User approves
          ↓
Direct payment
          ↓
Rating & reputation

The product should feel like an agent coordinating local work, not simply a worker directory.

## 78. Final Product Architecture

┌─────────────────────────────────────────────────────┐
│                    MOBILE APP                       │
│                                                     │
│   USER MODE                  WORKER MODE            │
│                                                     │
│   Create Work                Job Alerts             │
│   Track Jobs                 Skills                 │
│   Chat                       Availability           │
│   Ratings                    Portfolio              │
│   UPI / QR                   Subscription           │
│   Reopen                     Achievements           │
│   SOS                        Job History            │
└───────────────────────┬─────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────┐
│                  AGENTIC BACKEND                    │
│                                                     │
│ Need Understanding                                  │
│ Dynamic Work Specification                          │
│ Smart Matching                                     │
│ Radius Expansion                                   │
│ Smart Retry                                        │
│ Worker Alerts                                      │
│ Job State Machine                                  │
│ Chat & Notifications                               │
│ Reputation & Ratings                               │
│ Subscription                                       │
│ Safety / SOS                                       │
│ Database                                           │
└───────────────────────┬─────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────┐
│                CREATOR / ADMIN PORTAL               │
│                                                     │
│ Users • Workers • Verification • Jobs              │
│ Reports • Disputes • Subscriptions                 │
│ Offers • Ads • Notifications • Analytics           │
│ Matching Settings • Moderation • Platform Settings │
└─────────────────────────────────────────────────────┘

## 79. Final Product Definition

Immediate Local Work is not a conventional worker marketplace.

Agentic local-work discovery, matching and coordination platform.

NEED
 ↓
UNDERSTAND
 ↓
SPECIFY
 ↓
CONFIRM
 ↓
MATCH
 ↓
ALERT
 ↓
ASSIGN
 ↓
CHAT
 ↓
COORDINATE
 ↓
EXECUTE
 ↓
JOB DONE REQUEST
 ↓
USER APPROVAL
 ↓
COMPLETED
 ↓
DIRECT PAYMENT
 ↓
RATING
 ↓
REPUTATION

The platform combines: AI + Local Discovery + Smart Matching + Real-Time Coordination + Reputation + Privacy + Safety + Subscription-Based Worker Monetization.

This document represents the final functional scope and source of truth for the current production product.

## 80. Production Architecture — Final Decision

- KaamNow is production-first and uses a modular monolith rather than a large microservices fleet at launch.

- Mobile: Flutter + Dart for Android/iOS, with Kotlin Android platform integration for supported emergency/device capabilities.

- Edge: Cloudflare DNS/CDN/WAF/DDoS protection and edge rate controls.

- Compute: Google Cloud Run running the containerized FastAPI backend.

- Database: managed PostgreSQL with PostGIS as the authoritative source of truth.

- Cache/realtime coordination: managed Redis/Memorystore.

- Async processing: Google Cloud Pub/Sub with idempotent consumers and retry/dead-letter handling.

- Object storage: Cloudflare R2 using private buckets and signed URLs.

- Push notifications: Firebase Cloud Messaging.

- Admin: Next.js + TypeScript with a protected Admin API.

- Observability: OpenTelemetry plus Sentry/Grafana Cloud.

- CI/CD: GitHub Actions.

- Infrastructure as Code: Terraform/OpenTofu.

- AI: Python AI Orchestrator with provider/model adapters, strict structured-output validation and deterministic/manual fallback.

## 81. Final System Architecture

Flutter Mobile App
(User Mode + Worker Mode)
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
 ├── Auth & Accounts
 ├── Users / Workers
 ├── Jobs / Requirements
 ├── Matching / PostGIS
 ├── Assignments
 ├── Chat / Realtime
 ├── Ratings / Reputation
 ├── Subscriptions
 ├── Notifications
 ├── Disputes / Reports
 ├── SOS / Safety
 ├── Admin APIs
 └── AI Orchestrator
        │
   ┌────┼───────────────┐
   ▼    ▼               ▼
PostgreSQL  Redis      Pub/Sub
+ PostGIS   Cache      Async Events
   │          │            │
   │          │            ▼
   │          │      Background Workers
   │          │
   └──────────┴──────► Business Data / Coordination

Object Storage: Cloudflare R2
Push: Firebase Cloud Messaging
Maps: Google Maps Platform
OTP/SMS: Approved provider
Admin: Next.js + TypeScript
Observability: OpenTelemetry + Sentry/Grafana
CI/CD: GitHub Actions
IaC: Terraform/OpenTofu

## 82. Backend Modular Architecture

- auth: OTP, sessions, token lifecycle, device sessions and RBAC.

- users: user profile, preferences and account lifecycle.

- workers: worker profile, skills, availability, verification, reputation and portfolio links.

- jobs: job creation, requirements, deadlines, radius, budget, state machine and history.

- matching: eligibility, PostGIS radius filtering, deterministic ranking, alerts and retry.

- assignments: atomic acceptance, position reservation, rejection, reassignment and multi-worker fulfillment.

- chat: private job chat, WebSocket delivery, persisted messages and system events.

- ratings: two-way ratings, reviews, reputation and achievement triggers.

- subscriptions: worker trial, ₹100/month plan, expiry and configurable offers/plans.

- notifications: in-app notifications, FCM push and reminders.

- disputes: reports, conduct issues, completion issues and admin resolution.

- sos: emergency session, location events, emergency workflow and local-audio reference metadata.

- admin: verification, moderation, jobs, reports, disputes, subscriptions, promotions, matching configuration and audit.

- ai: requirement understanding, dynamic clarification and structured job extraction.

## 83. Database and Data Ownership

- PostgreSQL is the authoritative source of truth for accounts, jobs, assignments, state history, chat messages, ratings, subscriptions, notifications, reports, disputes, SOS metadata and audit records.

- PostGIS is used for geospatial worker discovery and radius queries.

- Redis is not the primary database. It is used for cache, ephemeral state, presence, realtime coordination and other safe derived state.

- Cloudflare R2 stores binary objects. PostgreSQL stores object metadata, ownership and keys rather than file blobs.

- Worker portfolio media is not stored directly by default; Google Drive portfolio links are supported.

- Sensitive identity data is isolated and access-controlled.

- Government IDs are never exposed through public profile APIs.

## 84. API and Business-Logic Rules

- All client requests use authenticated HTTPS APIs except explicitly public endpoints.

- FastAPI validates request schema, authentication, authorization and business rules before domain execution.

- Business logic is not trusted from the mobile client.

- AI output is schema-validated before entering job/matching logic.

- Every important state transition validates the current state.

- Assignment, acceptance, completion and other critical operations are idempotent.

- Duplicate requests must not create duplicate jobs, assignments or notifications.

- Background Pub/Sub consumers must be safe to retry.

- External services are accessed through integration adapters so the core domain is not tightly coupled to a single vendor.

## 85. Final Matching Architecture

- AI understands the user's requirement and helps produce a structured job requirement.

- Deterministic backend logic decides worker eligibility and ranking.

- Eligibility checks required skill, active state, availability, current radius, subscription entitlement, restrictions and conflicting assignments.

- PostGIS performs distance/radius filtering.

- Ranking may use distance, rating, relevant experience, similar completed jobs and reliability.

- Matching weights and radius-expansion policies are configurable from the admin system.

- Worker alerts are generated through the notification/event pipeline.

- Atomic assignment prevents two workers from claiming the same single-worker position.

- Rejected/unavailable workers are skipped and the next eligible candidates can be alerted.

- Open Jobs provides a discovery path for new workers and broader fulfillment.

## 86. Final Job Lifecycle and UI Status

- Authoritative backend state machine: DRAFT → POSTED → MATCHING → ALERT_SENT → ACCEPTED → ASSIGNED → CHAT/COORDINATION → ON_THE_WAY → ARRIVED → IN_PROGRESS → DONE_REQUESTED → APPROVED → COMPLETED → RATING.

- Additional states/paths: POSTED → CANCELLED; POSTED → EXPIRED; ACCEPTED → NO_SHOW; DONE_REQUESTED → DISPUTED → ADMIN REVIEW → RESOLUTION.

- Important UI clarification: the mobile UI does not show separate 'On the Way' or 'Arrived' status screens.

- User-facing operational status is: Assigned → In Progress → Done Requested → Approved → Completed → Rating.

- Worker selects Job Done; worker cannot directly set COMPLETED.

- User approves completion or reports an issue.

- Only user approval creates the authoritative COMPLETED transition.

- Completion triggers history, reputation, achievements and rating eligibility updates.

## 87. Final Payment and Financial Boundary

- KaamNow is a job coordination platform, not an escrow service or payment intermediary for job payments.

- User pays Worker directly using UPI, QR or another mutually agreed external payment method.

- KaamNow does not hold, transfer, escrow, recover or guarantee job-payment funds.

- KaamNow does not store UPI PINs or payment OTPs.

- Transaction commission is not part of the current monetization model.

- Agreed amount and payment-related job metadata may be displayed/recorded.

- Inspection-based pricing follows Worker proposal → User approval → agreed amount → work.

- Additional work follows Worker proposal → User approval → updated agreed amount.

- Platform disputes can review job evidence, agreed amount and chat context, but the platform does not guarantee a financial recovery/refund outcome.

- Worker subscription billing, if implemented through an external payment provider, is a separate platform subscription function and must not turn ordinary job payments into platform-held funds.

## 88. Final Worker Subscription Rules

- Worker subscription is ₹100/month under the current product specification.

- First 30 days are completely free with worker features enabled.

- After trial/renewal expiry, the profile remains and ongoing/existing jobs can continue, but new jobs and Open Jobs cannot be accepted.

- Renewal restores full worker acceptance capability.

- Price, trial duration, plans, offers, deals and discounts are database/API driven.

- Client UI must never be the authoritative source of entitlement; backend checks subscription state.

- Subscription configuration changes are audited.

## 89. Final SOS and Safety Architecture

- SOS is available to both users and workers.

- Emergency scenarios include harassment, threats, physical confrontation, home-visit danger, medical emergency and other immediate safety situations.

- Hardware trigger behavior depends on Android/device capabilities. The product must not claim universal third-party interception of power-button gestures.

- SOS flow: Emergency Trigger → SOS Activated → Location Captured → Emergency Alert → Emergency Contact/Emergency Call Flow → SOS Safety Session.

- Audio recording starts only after SOS activation. Normal app use must never secretly record.

- Recording follows Android microphone/background restrictions and applicable privacy/recording requirements.

- Audio is encrypted and stored locally on the device by default.

- Backend stores protected SOS metadata and a local-audio reference rather than ordinary cloud audio by default.

- Emergency calling/trusted-contact flow is supported where technically available; guaranteed automatic police dispatch must not be claimed without a real integration.

- SOS cancellation/end behavior and accidental-trigger protection must be tested on supported devices.

## 90. Final Privacy and Security Architecture

- HTTPS is mandatory for production API traffic.

- Cloudflare WAF/DDoS protection and edge rate controls protect public endpoints.

- Application-level rate limiting protects OTP, login, messaging, report, SOS and other abuse-sensitive endpoints.

- RBAC is enforced server-side for user, worker, moderator and admin capabilities.

- Exact address is hidden before the appropriate assignment stage.

- Approximate area/distance is used during pre-assignment discovery.

- Government ID is restricted and never public.

- Chat is private to authorized job participants, subject to legitimate report/dispute review workflows.

- SOS data is separately protected.

- Secrets are injected through managed secret configuration and never committed to Git.

- Audit logs capture sensitive admin actions and important job state transitions.

- Data retention and deletion/deactivation workflows are required.

## 91. Final Notification and Realtime Architecture

- FCM provides mobile push notifications.

- PostgreSQL stores authoritative in-app notification records.

- Pub/Sub carries asynchronous notification events and retryable work.

- Redis supports realtime presence and cross-instance coordination.

- WebSocket provides private job-chat realtime delivery.

- Notification delivery is idempotent and safe to retry.

- Invalid/expired FCM device tokens are removed or disabled.

- Critical events remain recoverable in-app if push delivery fails.

## 92. Final External Integration Boundary

- Google Maps Platform is used for location/geocoding/map features where required; API credentials are restricted and never exposed as private server secrets in the client.

- OTP/SMS is provided by an approved external provider; credentials remain server-side.

- Firebase Cloud Messaging is used for push delivery.

- Cloudflare R2 is used for object storage.

- AI model providers are accessed only through the backend AI Orchestrator.

- External integrations are isolated behind adapters and can be replaced without rewriting core domain logic.

- No external service is allowed to bypass KaamNow's authorization, privacy, payment-boundary or safety rules.

## 93. Final Admin / Creator Architecture

- Admin portal is Next.js + TypeScript.

- Admin communicates only through protected Admin APIs.

- Admin never connects directly to PostgreSQL from the browser.

- Admin capabilities include users, workers, verification, jobs, reports, disputes, subscriptions, offers, ads/promotions, notifications, analytics, matching settings, moderation and platform settings.

- High-risk actions require explicit authorization and are written to audit logs.

- Subscription pricing and trial settings are configurable without mobile-app redeployment.

- Matching settings and safe operational limits are configurable without changing application code where appropriate.

## 94. Final DevOps, CI/CD and Infrastructure

- GitHub Actions runs linting, unit tests, integration tests, dependency checks and container/image security checks.

- Terraform/OpenTofu manages cloud infrastructure and environment configuration.

- Staging and production environments are separated.

- Production deployments use immutable container images.

- Database migrations are controlled deployment steps.

- Smoke tests run after deployment.

- Rollback to a known-good application image is supported.

- OpenTelemetry provides traces/metrics/log correlation.

- Sentry captures application errors.

- Grafana/Cloud Monitoring provides operational dashboards and alerts.

- Backups are automated and restore procedures are periodically tested.

- RPO/RTO targets must be defined before production launch.

## 95. Final Production Scaling Strategy

- Phase 1: modular FastAPI monolith on horizontally scalable Cloud Run instances.

- Phase 2: scale background workers, matching and notification processing independently.

- Phase 3: extract only measured bottlenecks such as Matching or Chat/Realtime into separate services.

- Phase 4: introduce stronger event-driven boundaries only when real traffic, reliability or team ownership justifies the complexity.

- Kubernetes is not required at launch.

- Kafka is not required at launch.

- MongoDB is not required as a second primary database.

- Multiple databases are not introduced without a demonstrated requirement.

- PostgreSQL remains the primary source of truth.

## 96. Final Edge Cases Added by Production Architecture

- Duplicate assignment caused by concurrent worker acceptance.

- Duplicate Pub/Sub delivery.

- Redis unavailable while API remains operational.

- Cloud Run instance restart during a WebSocket session.

- FCM token expiry or notification failure.

- AI provider timeout/failure or malformed structured output.

- Maps/geocoding provider failure.

- R2 upload interruption or signed URL expiry.

- Database migration failure and rollback.

- Cloudflare/WAF false-positive blocking.

- Subscription entitlement cache mismatch.

- Worker accepts while subscription expires concurrently.

- User approves completion while a duplicate approval request arrives.

- SOS trigger attempted on an unsupported Android/device configuration.

- Local SOS recording permission denied or recording interrupted.

- Backup exists but restore fails — restore testing is mandatory.

## 97. Final Production Acceptance Criteria

- The product is not considered production-ready merely because the website/app loads.

- End-to-end flow must pass: OTP → requirement → AI understanding → dynamic clarification → confirmation → PostGIS matching → worker alert → acceptance → assignment → private chat → work → Job Done → user approval → completion → rating/reputation.

- Cancellation, rejection, no-worker, radius expansion, no-show, reopen, additional work, completion dispute and subscription expiry must pass.

- Security, RBAC, exact-address privacy, identity restrictions, SOS behavior and audit logging must pass.

- Database backup and restore must be tested.

- CI/CD deployment and rollback must be tested.

- Monitoring and critical alerts must be tested.

- Production load/performance testing must cover job creation, matching, chat and notification workloads.

- All production secrets must be outside source control.

- Legal/product pages and user-facing payment/safety boundaries must be clear.

## 98. Final Source of Truth

The functional product scope in this PRD and the production infrastructure decisions in sections 80–97 together form the current KaamNow source of truth. If an older section conflicts with the final production architecture, the architecture-aligned rule in sections 80–97 takes precedence.
