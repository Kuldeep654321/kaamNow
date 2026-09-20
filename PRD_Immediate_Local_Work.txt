IMMEDIATE LOCAL WORK
FINAL PRODUCT REQUIREMENTS DOCUMENT (PRD)
Repository Version
============================================================

Product: Immediate Local Work
Document Type: Final PRD
Status: Final
Purpose: Complete product, functional, technical, safety, admin, and architecture specification.

Immediate Local Work
Final Product Requirements Document (PRD)
Version: 1.0
Status: Final / Scope Locked
Product Type: Agentic Local Work Discovery, Matching & Coordination Platform
Interfaces: Mobile Application + Creator/Admin Web Portal

================================================================================
1. PRODUCT OVERVIEW
================================================================================

------------------------------------------------------------
1.1 Product Vision
------------------------------------------------------------
Immediate Local Work is an agentic local-work coordination platform that allows users to describe a legitimate local task instead of manually searching through worker listings.
The system understands the user's requirement, identifies the required skill, dynamically collects relevant details, finds suitable nearby workers, alerts them, manages assignment, enables communication, coordinates the work, verifies completion and builds reputation.
“Don't search for a worker. Just tell us what needs to be done.”

================================================================================
2. PROBLEM STATEMENT
================================================================================
Finding reliable local workers is often fragmented and time-consuming.
Search for workers manually.
Decide which category to select.
Call multiple workers.
Explain the same problem repeatedly.
Check worker availability.
Negotiate prices.
Share location.
Deal with cancellations and no-shows.
Determine worker reliability.
Workers commonly face difficulty finding nearby jobs, dependence on personal contacts, irregular job opportunities, difficulty building reputation, limited digital visibility and difficulty managing multiple skills.
Immediate Local Work creates an intelligent coordination layer between users and local workers.

================================================================================
3. PRODUCT OBJECTIVES
================================================================================
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

================================================================================
4. PRODUCT SCOPE
================================================================================
Mobile Application
        +
Agentic Backend
        +
Creator/Admin Web Portal
The mobile application supports both User Mode and Worker Mode through the same account.

================================================================================
5. USER TYPES
================================================================================

------------------------------------------------------------
5.1 User
------------------------------------------------------------
A person who needs local work completed.
Cleaning
Electrical work
Plumbing
Painting
Cooking
Pet care
Vehicle washing
Appliance repair
Moving assistance
Other legitimate local work

------------------------------------------------------------
5.2 Worker
------------------------------------------------------------
A local service provider who can offer one or multiple skills. A worker is not restricted to a single profession.

------------------------------------------------------------
5.3 Creator/Admin
------------------------------------------------------------
Users
Workers
Verification
Jobs
Reports
Disputes
Subscriptions
Offers
Promotions
Matching configuration
Analytics
Platform settings

================================================================================
6. ACCOUNT ARCHITECTURE
================================================================================
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

================================================================================
7. AUTHENTICATION
================================================================================
Mobile number login
OTP verification
Secure session management
Login/logout
Account recovery
One mobile number → one account
The mobile number is not automatically exposed to another user or worker.

================================================================================
8. PROFILE SYSTEM
================================================================================

------------------------------------------------------------
User Profile
------------------------------------------------------------
Name
Profile picture
Mobile number
General location/area
Identity verification status
Ratings/reputation
Relevant completed jobs
Reliability information where applicable

------------------------------------------------------------
Worker Profile
------------------------------------------------------------
Name
Profile picture
Skills
Service areas
Availability
Rating
Completed jobs
Achievements
Identity verification status
Verified Worker status
Portfolio links
Subscription status

================================================================================
9. IDENTITY VERIFICATION
================================================================================
Users and workers can provide Aadhaar, PAN or another supported government-issued identity document.

------------------------------------------------------------
Privacy
------------------------------------------------------------
Government ID is never publicly displayed.
Government ID is not visible to other users/workers.
Access is restricted.
Sensitive information is securely stored.
Retention follows minimum-necessary principles.
Public profiles display only verification status.
Identity badge: Identity Verified. This is separate from worker service verification.

================================================================================
10. WORKER VERIFICATION
================================================================================
A worker receives the Verified Worker status after achieving 3 or more user-approved completed jobs.
Government identity verification does not automatically create the Verified Worker badge.

================================================================================
11. REQUIREMENT ENTRY
================================================================================
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

================================================================================
12. NEED UNDERSTANDING
================================================================================
Work category
Required skill
Sub-skill
Work type
Number of workers required
Deadline
Budget relevance
Inspection requirement
Other necessary attributes

================================================================================
13. DYNAMIC WORK SPECIFICATION
================================================================================
Questions are generated according to the detected work.

------------------------------------------------------------
Example: Cleaning
------------------------------------------------------------
User: “Ghar saaf karwana hai.”
System asks: What needs cleaning?
Room
Bathroom
Kitchen
Full House
Windows
Other
Then: Cleaning type?
Basic
Deep Cleaning
Dusting
Floor Cleaning
Complete Cleaning
Other
The same principle applies to electrician, plumber, painting, cooking, pet care, AC repair, appliance repair and other services.

================================================================================
14. JOB CONFIRMATION
================================================================================
Work: Deep House Cleaning
Area: Vijay Nagar
Date: 22 September
Time: 10:00 AM
Budget: ₹800
Workers Required: 1
Search Radius: 10 KM
User selects Confirm Job. Matching begins after confirmation.

================================================================================
15. DEADLINE
================================================================================
Deadline is optional. User can select a date/time or no deadline.
Worker availability
Matching
Notifications
Reminders
Expiry

================================================================================
16. BUDGET SYSTEM
================================================================================

------------------------------------------------------------
Budget-Based Work
------------------------------------------------------------
Cleaning
Car washing
Bike washing
Painting
Cooking
Pet care
Art/drawing
Small assistance

------------------------------------------------------------
Inspection-Based Work
------------------------------------------------------------
Electrician
Plumber
AC repair
Appliance repair
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

================================================================================
17. SEARCH RADIUS
================================================================================
5 km
10 km
15 km
20 km
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

================================================================================
18. LOCATION PRIVACY
================================================================================

------------------------------------------------------------
Before Assignment
------------------------------------------------------------
Approximate area
Approximate distance
Exact address hidden

------------------------------------------------------------
After Assignment
------------------------------------------------------------
Exact location can be shared after appropriate user approval.

================================================================================
19. SMART MATCHING ENGINE
================================================================================
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

================================================================================
20. WORKER ELIGIBILITY
================================================================================
Required skill is available.
Worker is active.
Worker is available during the required time.
Worker is inside the current radius.
Subscription permits new-job acceptance.
Worker is not restricted.
Worker does not have a conflicting assignment.

================================================================================
21. SMART MATCHING EXPLANATION
================================================================================
Why this job matches you: Required cleaning skill; 3.2 km away; available tomorrow; similar jobs completed.

================================================================================
22. WORKER JOB ALERT
================================================================================
NEW JOB

Deep House Cleaning
Distance: 3.4 KM
Date: Tomorrow
Time: 10:00 AM
Budget: ₹800
Workers Required: 1

[ ACCEPT ]   [ REJECT ]

================================================================================
23. SMART RETRY
================================================================================
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

================================================================================
24. OPEN JOB POSTING
================================================================================
User can select Open Job Posting. The job becomes available to relevant workers.
Increase worker discovery
Improve job fulfillment
Give new workers opportunities
Reduce dependence on existing reputation

================================================================================
25. OPEN JOB FILTERS
================================================================================
Distance
Work type
Required skill
Budget
Date
Time

================================================================================
26. MULTIPLE WORKER JOBS
================================================================================
A job can require multiple workers.
Required Workers: 3

Worker A → Assigned
Worker B → Assigned
Worker C → Assigned
Matching continues until the required count is fulfilled.

================================================================================
27. JOB ASSIGNMENT
================================================================================
Assignment is created.
Position is reserved.
Other workers cannot take that position.
Notifications are sent.
Matching stops for that position.
For multiple-worker jobs, matching continues for remaining positions.

================================================================================
28. IN-APP CHAT
================================================================================
Work details
Timing
Price discussion
Additional requirements
Coordination

------------------------------------------------------------
Privacy
------------------------------------------------------------
Phone number is not automatically exposed.
Chat is protected.
Automated safety/moderation checks may apply.
Authorized review may occur during reports/disputes.
Normal chats are not continuously human-monitored.

================================================================================
29. PRICE NEGOTIATION
================================================================================
The platform does not enforce a universal price. User and worker can discuss and agree on pricing. The final agreed amount is recorded against the job.

================================================================================
30. ADDITIONAL WORK
================================================================================
Worker proposes additional amount
             ↓
        User reviews
             ↓
        User approves
             ↓
       Final amount updated

================================================================================
31. PAYMENT & FINANCIAL BOUNDARY
================================================================================
The platform is a job coordination platform, not a payment intermediary or escrow service.

------------------------------------------------------------
Direct Payment
------------------------------------------------------------
Payment occurs directly from User to Worker.
UPI
QR
Other mutually agreed direct payment methods

------------------------------------------------------------
Platform Responsibilities
------------------------------------------------------------
Display the agreed amount.
Record the final agreed amount.
Provide payment-related reminders.
Maintain payment-related job metadata where required.

------------------------------------------------------------
Platform Does Not
------------------------------------------------------------
Hold worker money.
Transfer money between user and worker.
Operate an escrow wallet.
Take transaction commission.
Store UPI PIN/OTP.
Guarantee payment.
Guarantee refunds.
Automatically recover money from either party.
The external payment method remains the authoritative mechanism for the actual financial transaction.

================================================================================
32. JOB STATE MACHINE
================================================================================
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

================================================================================
33. JOB COMPLETION
================================================================================
Worker cannot directly finalize a job as completed. Worker selects Job Done. The user receives a completion request.
Approve
Raise Issue/Dispute
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

================================================================================
34. REOPEN JOB
================================================================================
Worker cancels
Worker becomes unavailable
Worker does not show up
Worker cannot complete the assignment
REOPEN
  ↓
SMART MATCHING
  ↓
NEXT ELIGIBLE WORKERS

================================================================================
35. JOB EXPIRY
================================================================================
New acceptance is disabled.
Relevant alerts stop.
Job becomes expired.
User receives notification.
Relevant workers receive status notification.

================================================================================
36. WORKER NO-SHOW
================================================================================
User can report no-show.
Incident can be reviewed.
Reliability impact can be applied when appropriately verified.
Repeated incidents can trigger admin review.

================================================================================
37. USER FAKE/MISLEADING JOB
================================================================================
Repeated fake or misleading behaviour may affect reliability.
May trigger report review.
May trigger administrative action.
Unverified accusations should not automatically destroy reputation.

================================================================================
38. TWO-WAY RATING
================================================================================

------------------------------------------------------------
User → Worker
------------------------------------------------------------
Rating
Review

------------------------------------------------------------
Worker → User
------------------------------------------------------------
Rating
Review
Only eligible completed jobs contribute to normal reputation.

================================================================================
39. REPUTATION SYSTEM
================================================================================

------------------------------------------------------------
Worker
------------------------------------------------------------
Completed jobs
User ratings
Reliability
No-show history
Relevant experience

------------------------------------------------------------
User
------------------------------------------------------------
Completed jobs
Worker feedback
Verified reliability incidents
The exact calculation is configurable.

================================================================================
40. WORKER ACHIEVEMENTS
================================================================================
Verified Worker — 3+ user-approved completed jobs
Highly Rated — configured rating threshold
Quick Response — configured response-performance threshold
50 Jobs Completed — 50 approved completed jobs

================================================================================
41. WORKER AVAILABILITY
================================================================================
Active / Inactive status
Date
Start time
End time
Matching uses this information.

================================================================================
42. WORKER PORTFOLIO
================================================================================
The application does not store worker media directly.
Workers can provide a Google Drive portfolio link.
URL
Title
Description
Metadata
Users open the portfolio externally. Before/after proof can also use Google Drive links.

================================================================================
43. WORKER SUBSCRIPTION
================================================================================

------------------------------------------------------------
First 30 Days
------------------------------------------------------------
Completely Free. All worker features are available.

------------------------------------------------------------
After 30 Days
------------------------------------------------------------
₹100/month.

------------------------------------------------------------
Expiry
------------------------------------------------------------
Profile remains.
Existing/ongoing jobs can continue.
New jobs cannot be accepted.
New Open Jobs cannot be accepted.

------------------------------------------------------------
Renewal
------------------------------------------------------------
Full worker access returns after renewal.

================================================================================
44. SUBSCRIPTION ADMINISTRATION
================================================================================
Subscription price
Trial duration
Plans
Offers
Deals
Discounts
Settings are database/API driven so changes do not require app redeployment.

================================================================================
45. SMART REMINDERS
================================================================================
Scheduled job reminder
Pending completion approval
Pending rating
Upcoming job
Subscription expiry
Reopened job
Important status changes

================================================================================
46. NOTIFICATION SYSTEM
================================================================================

------------------------------------------------------------
User Notifications
------------------------------------------------------------
Job posted
Matching started
Worker found
Worker assigned
Worker on the way
Worker arrived
Work started
Job done request
Completion
Rating request
Cancellation
Reopen
Dispute
Payment-related reminder
Admin announcement

------------------------------------------------------------
Worker Notifications
------------------------------------------------------------
New job
Assignment
Job timing
User cancellation
Reopened job
Rating
Subscription expiry
Admin announcement

================================================================================
47. HINDI + ENGLISH
================================================================================
The application supports Hindi and English. UI, notifications and system messages should be localization-ready.

================================================================================
48. EMERGENCY SOS & SAFETY ASSISTANCE
================================================================================
Emergency safety is available to both Users and Workers.
Misbehavior
Harassment
Threats
Physical confrontation
Home-visit danger
Medical emergency
Other immediate safety situations

================================================================================
49. SOS ACTIVATION
================================================================================
The intended emergency interaction includes a rapid hardware-button gesture such as power button pressed 3–4 times.
Actual detection depends on Android/device capabilities and system restrictions. Where supported, the gesture triggers the SOS workflow. The application must not claim universal interception of power-button presses by a normal third-party Android app.

================================================================================
50. SOS WORKFLOW
================================================================================
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

================================================================================
51. EMERGENCY LOCATION
================================================================================
Current location is captured.
Timestamp is recorded.
Location is included in the emergency workflow.
Configured trusted contacts/authorized emergency mechanisms can receive the alert.
SOS session status is tracked.

================================================================================
52. EMERGENCY CALLING
================================================================================
Emergency calling
Configured trusted emergency contact
Appropriate police/emergency assistance flow
The system should not claim guaranteed automatic connection to the nearest police station unless an actual integration exists.

================================================================================
53. SOS AUDIO EVIDENCE
================================================================================
After SOS activation, emergency audio recording can automatically start.
No recording during normal application usage.
Recording begins only after SOS activation.
Recording follows Android microphone/background restrictions.
Recording is stored locally on the device.
Audio should be encrypted.
Recording stops when the SOS session ends/cancels or configured recording conditions are reached.

================================================================================
54. SOS AUDIO PRIVACY
================================================================================
Avoid normal cloud media storage by default.
Store audio locally.
Restrict application access.
Encrypt stored audio.
Provide appropriate deletion/export controls.
Follow applicable privacy and recording requirements.

================================================================================
55. SOS SESSION DATA
================================================================================
SOS ID
Account ID
Timestamp
Location
Trigger type
Emergency status
Local audio reference
Incident/report status

================================================================================
56. SAFETY REPORTING
================================================================================
Misbehavior
Harassment
Threats
Physical confrontation
Abuse
Fake jobs
No-show
Safety concerns
Other inappropriate behaviour
Reports enter the moderation/dispute system.

================================================================================
57. PAYMENT & DISPUTE BOUNDARY
================================================================================
The platform separates financial transactions from platform dispute handling.

------------------------------------------------------------
Financial Boundary
------------------------------------------------------------
The platform does not hold funds.
The platform does not process payments.
The platform does not act as escrow.
The platform does not guarantee refunds.
The platform does not guarantee payment recovery.
The platform does not take transaction commission.
User and worker are responsible for completing agreed payment directly.

------------------------------------------------------------
Platform Dispute Boundary
------------------------------------------------------------
Worker no-show
User no-show
Fake/misleading job
Misbehavior
Harassment
Safety incidents
Job cancellation
Reassignment
Completion disagreement
Platform assignment problems
Chat/coordination problems
Policy violations

------------------------------------------------------------
Financial Disagreement
------------------------------------------------------------
Example: user and worker disagree whether the final amount should be ₹800 or ₹1,200.
The platform can review the agreed amount recorded in the job, relevant in-app chat, additional-work approvals, job history and reports/evidence.
The platform does not automatically hold money, refund the user, transfer money to the worker, recover money or guarantee a financial outcome.
Admin may take platform-level action such as warning, restriction, suspension, reassignment, case closure or reputation/reliability action where justified.

================================================================================
58. DATA & PRIVACY ARCHITECTURE
================================================================================

------------------------------------------------------------
Government ID
------------------------------------------------------------
Private and restricted.

------------------------------------------------------------
Mobile Number
------------------------------------------------------------
Used for authentication and not automatically exposed.

------------------------------------------------------------
Location
------------------------------------------------------------
Approximate before assignment and exact after appropriate assignment/approval.

------------------------------------------------------------
Chat
------------------------------------------------------------
Private and protected.

------------------------------------------------------------
Payment
------------------------------------------------------------
Direct user-to-worker payment without unnecessary payment credential storage.

------------------------------------------------------------
SOS Audio
------------------------------------------------------------
Encrypted local storage by default.

------------------------------------------------------------
Account
------------------------------------------------------------
Users should have appropriate account controls including deactivation and deletion workflows.

================================================================================
59. CREATOR/ADMIN PORTAL
================================================================================
A separate web application for platform administration.
Dashboard
Users
Workers
Verification
Jobs
Reports
Disputes
Subscriptions
Offers
Ads / Promotions
Notifications
Analytics
Matching Settings
Platform Settings
Moderation

================================================================================
60. USER MANAGEMENT
================================================================================
Search users
View profiles
View relevant job history
View reports
Manage account restrictions
Review verification
Handle moderation cases

================================================================================
61. WORKER MANAGEMENT
================================================================================
Search workers
View skills
View availability
View completed jobs
View ratings
View achievements
View subscription status
Review identity verification
Handle reports
Manage restrictions

================================================================================
62. VERIFICATION MANAGEMENT
================================================================================
ID Submitted
     ↓
Verification Process
     ↓
Verified / Rejected / Review Required
     ↓
Identity Status Updated
The exact verification mechanism may use an appropriate verification provider or controlled administrative verification.

================================================================================
63. JOB ADMINISTRATION
================================================================================
Active jobs
Matching jobs
Assigned jobs
Completed jobs
Cancelled jobs
Expired jobs
Reopened jobs
Disputed jobs
No-show cases

================================================================================
64. DISPUTE MANAGEMENT
================================================================================
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

================================================================================
65. REPORTS & MODERATION
================================================================================
User reports
Worker reports
Safety incidents
Fake-job reports
No-show reports
Abuse reports
Disputes
Possible administrative actions: Warning, Restriction, Suspension, Verification Review, Case Closure.
Sensitive administrative actions should be auditable.

================================================================================
66. ADS & PROMOTIONS
================================================================================
Promotional banners
Sponsored listings
Offers
Deals
Announcements
Campaigns
Promotional content must clearly display Sponsored / Advertisement.

================================================================================
67. ANALYTICS DASHBOARD
================================================================================

------------------------------------------------------------
Users
------------------------------------------------------------
Total users
Active users
New users

------------------------------------------------------------
Workers
------------------------------------------------------------
Total workers
Active workers
Verified workers
Active subscriptions

------------------------------------------------------------
Jobs
------------------------------------------------------------
Jobs posted
Jobs matched
Jobs assigned
Jobs completed
Jobs cancelled
Jobs expired
Jobs reopened

------------------------------------------------------------
Matching
------------------------------------------------------------
Match success rate
Average matching time
Acceptance rate
Rejection rate
Radius expansion frequency

------------------------------------------------------------
Reliability
------------------------------------------------------------
No-show rate
Cancellation rate
Dispute rate
Average rating

------------------------------------------------------------
Revenue
------------------------------------------------------------
Active subscriptions
Trial conversions
Subscription revenue

================================================================================
68. ADMIN MATCHING & PLATFORM CONFIGURATION
================================================================================

------------------------------------------------------------
Matching
------------------------------------------------------------
Skill-match weighting
Distance weighting
Availability weighting
Rating weighting
Experience weighting
Search radius
Radius expansion
Smart retry behaviour

------------------------------------------------------------
Platform
------------------------------------------------------------
Subscription price
Trial duration
Job expiry
Achievement thresholds
Notification rules
Moderation rules
Offers
Promotions
Language/configuration
All configurable values should be database/API driven.

================================================================================
69. SYSTEM & BACKEND ARCHITECTURE
================================================================================
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

================================================================================
70. LOGICAL BACKEND SERVICES
================================================================================

------------------------------------------------------------
Authentication Service
------------------------------------------------------------
OTP
Sessions
Account identity

------------------------------------------------------------
Profile Service
------------------------------------------------------------
Users
Workers
Skills
Availability
Profiles

------------------------------------------------------------
Job Service
------------------------------------------------------------
Job creation
Dynamic specifications
Assignments
State transitions
Reopening
Expiry

------------------------------------------------------------
AI / Need Understanding Service
------------------------------------------------------------
Requirement understanding
Category detection
Skill detection
Dynamic questions
Structured specifications

------------------------------------------------------------
Matching Service
------------------------------------------------------------
Eligibility
Ranking
Radius expansion
Smart retry
Matching explanation

------------------------------------------------------------
Notification Service
------------------------------------------------------------
Worker buzzer
Push notifications
Reminders
Status notifications

------------------------------------------------------------
Chat Service
------------------------------------------------------------
Private conversations
Messages
Safety/moderation signals

------------------------------------------------------------
Reputation Service
------------------------------------------------------------
Ratings
Reviews
Reliability
Achievements

------------------------------------------------------------
Subscription Service
------------------------------------------------------------
Trial
Subscription
Expiry
Renewal
Offers

------------------------------------------------------------
Safety Service
------------------------------------------------------------
SOS
Safety incidents
Reports
Emergency session data

------------------------------------------------------------
Admin Service
------------------------------------------------------------
Creator portal
Moderation
Configuration
Analytics

================================================================================
71. CORE DATABASE ENTITIES
================================================================================
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

================================================================================
72. CORE RELATIONSHIPS
================================================================================
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

================================================================================
73. CORE JOB DATA
================================================================================
Job ID
User ID
Requirement text
Detected category
Required skills
Dynamic specifications
Approximate location
Exact location
Location-sharing status
Budget
Final agreed price
Deadline
Required worker count
Assigned worker count
Search radius
Current status
Created timestamp
Updated timestamp
Expiry timestamp

================================================================================
74. JOB AUDIT TRAIL
================================================================================
Job created
Matching started
Worker alerted
Worker accepted
Worker rejected
Assignment created
Worker cancelled
Worker no-show
Job reopened
Job done requested
User approved
Job completed
Rating submitted
Report created
Admin action
Subscription changed
This provides traceability for disputes and system debugging.

================================================================================
75. SECURITY ARCHITECTURE
================================================================================
Secure authentication
Role-based access control
Least-privilege access
Encryption of sensitive data
Restricted government-ID access
Location access control
Protected chat
Secure audit logs
Encrypted SOS audio
Appropriate data retention
Account deletion/deactivation workflows

================================================================================
76. IMPORTANT EDGE CASES
================================================================================
No worker found
Worker rejection
All workers reject
Radius expansion
Worker cancellation
Worker no-show
User cancellation
Job expiry
Multiple workers required
Worker already busy
Worker subscription expired
User disputes completion
Worker disputes user behaviour
Price disagreement
Additional work
Worker unavailable
Location permission denied
Notification permission denied
Microphone permission denied
Network interruption
Duplicate job submission
Duplicate assignment
SOS trigger limitations caused by device/OS restrictions

================================================================================
77. USER EXPERIENCE PRINCIPLES
================================================================================
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

================================================================================
78. FINAL PRODUCT ARCHITECTURE
================================================================================
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

================================================================================
79. FINAL PRODUCT DEFINITION
================================================================================
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
This document represents the final functional scope and source of truth for the current hackathon product.
