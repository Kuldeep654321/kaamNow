# KaamNow — Final UI/UX Design Document

**Version:** 3.0
**Status:** Final / Production Architecture Aligned / Design Source of Truth
**Platform:** Flutter Android + iOS Mobile App + Creator/Admin Web Portal

Complete UI/UX Design System, Screen Specification & Visual Direction

**Product:** KaamNow — Immediate Local Work

**Document:** Complete UI/UX Design System, Screen Specification & Visual Direction

---

## 1. Purpose

This document defines the complete visual and interaction language for KaamNow.

It is intended to be used by:

- UI/UX designers

- Frontend developers

- Mobile developers

- AI design-generation tools

- Product designers

- QA teams

- Creator/Admin portal developers

This document must be used together with the product PRD. The PRD defines product behavior; this document defines how that behavior is represented visually and interactively.

---

## 2. Product Design Vision

KaamNow is an AI-powered local-work discovery, matching, and coordination platform.

It should NOT look like a generic classifieds marketplace or a traditional service-listing app.

The experience should communicate:

**Tell us what you need → understand the requirement → find suitable local workers → coordinate privately → complete the job → approve completion.**

The UI should make a technically complex agentic workflow feel simple.

## Core UX principles

1. One obvious primary action per screen.

2. Keep the first interaction extremely simple.

3. Ask only relevant questions.

4. Reveal complexity progressively.

5. Make system status visible.

6. Preserve user control over AI decisions.

7. Make privacy understandable.

8. Make safety actions accessible.

9. Use consistent components across User and Worker modes.

10. Design every loading, empty, error, offline, success, and permission state.

11. Avoid unnecessary decorative UI.

12. Never create a fake sense of certainty around price, safety, verification, or payment.

---

## 3. Reference Visual Direction

The visual direction is informed by the clean discovery-oriented design principles of the referenced Hubbly coworking-space finder concept.

Reference:

https://dribbble.com/shots/26298704-Hubbly-Coworking-Space-Finder-App

The reference is inspiration only.

## Principles adapted

- Clean discovery-first hierarchy.

- Large primary search/action area.

- Rounded cards.

- Soft surfaces.

- Clear icons.

- Strong whitespace.

- Short information blocks.

- Progressive disclosure.

- Simple navigation.

- Clear primary CTAs.

## Explicitly not copied

Do not reproduce:

- Exact layouts.

- Exact artwork.

- Exact illustrations.

- Exact iconography.

- Exact typography.

- Exact brand identity.

- Distinctive compositions.

KaamNow must have its own visual identity.

---

## 4. Final KaamNow Color Palette

The following palette is locked.

| Token | Hex | Primary role |

|---|---|---|

| Pitch Black | #141204 | Main dark text, deep surfaces, strong contrast |

| Dark Khaki | #262A10 | Primary dark surface, navigation, headers |

| Dark Khaki 2 | #54442B | Secondary dark surface, borders, muted elements |

| Cinnamon Wood | #A9714B | Primary brand/action color |

| Toasted Almond | #E8985E | Highlight, active state, secondary CTA accent |

The `ff` alpha suffix from the supplied CSS HEX values means fully opaque. For implementation, use the six-digit values above unless an explicit alpha value is required.

---

## 5. Color Roles

## 5.1 Pitch Black — #141204

Use for:

- Main text on light surfaces.

- Strong headings.

- Important icons.

- Deep dark backgrounds.

- High-priority navigation elements.

- High-contrast content.

Do not use it for every element. Preserve hierarchy.

## 5.2 Dark Khaki — #262A10

Use for:

- Dark navigation.

- Header surfaces.

- Worker mode surfaces where a stronger visual identity is useful.

- Secondary dark cards.

- Dark mode base layers.

## 5.3 Dark Khaki 2 — #54442B

Use for:

- Secondary surfaces.

- Borders on dark UI.

- Muted labels.

- Dividers.

- Secondary card backgrounds.

- Supporting dark UI.

## 5.4 Cinnamon Wood — #A9714B

Use as the main action/brand color:

- Primary CTA.

- Selected controls.

- Main interactive buttons.

- Important links.

- Active states.

- Key highlights.

## 5.5 Toasted Almond — #E8985E

Use for:

- Hover/pressed/active accents.

- Secondary CTA emphasis.

- Small highlights.

- Important selected indicators.

- Progress accents.

- Limited decorative emphasis.

It should support Cinnamon Wood rather than replace it.

---

## 6. Background Strategy

The locked palette does not contain a dedicated light background token, therefore the app uses a warm neutral/ivory canvas token derived from the design system. This is a surface token, not a new brand color.

Recommended:

- Warm off-white / ivory for primary light-mode canvas.

- Dark Khaki / Pitch Black for dark surfaces.

The background must remain visually quiet so Cinnamon Wood becomes the action color.

Avoid pure-white-heavy fintech styling.

---

## 7. Dark Mode

Dark mode must be intentionally designed.

## Base

- Pitch Black

- Dark Khaki

## Cards

- Dark Khaki

- Dark Khaki 2

## Text

- Warm off-white primary text.

- Muted neutral secondary text.

## Accent

- Cinnamon Wood.

- Toasted Almond.

Do not simply invert the light theme.

---

## 8. Typography

Use a modern Android-compatible sans-serif.

Recommended visual characteristics:

- Geometric but readable.

- Strong numerals.

- Clear Hindi glyph support.

- Good readability at small sizes.

## Type hierarchy

| Level | Suggested size | Weight |

|---|---:|---|

| Display | 32–36 | Bold |

| H1 | 28–32 | Bold |

| H2 | 22–24 | SemiBold |

| H3 | 18–20 | SemiBold |

| Body Large | 16–18 | Regular |

| Body | 14–16 | Regular |

| Caption | 12–14 | Regular |

| Label | 12–14 | Medium/SemiBold |

Typography should never be used as decoration.

---

## 9. Spacing System

Use a 4/8-point spacing system.

Core values:

**4, 8, 12, 16, 20, 24, 32, 40, 48**

Typical screen padding:

**16–20 dp**

Section separation:

**24–32 dp**

Cards:

**16 dp internal padding** as a starting point.

---

## 10. Corner Radius

Recommended:

- Small controls: 8 dp.

- Inputs: 12 dp.

- Cards: 16 dp.

- Hero panels: 20–24 dp.

- Bottom sheets: 20–24 dp.

- Pills: fully rounded.

Avoid putting a large rounded rectangle around every piece of text.

---

## 11. Shadows and Elevation

Use subtle shadows.

## Level 0

Flat background.

## Level 1

Interactive cards.

## Level 2

Important floating actions.

## Level 3

Dialogs and bottom sheets.

Avoid heavy black shadows.

---

## 12. Icon System

Use a single consistent icon family.

Icons must:

- Have consistent stroke weight.

- Be recognizable.

- Work at small sizes.

- Have accessible labels where needed.

Do not use emoji as production icons.

---

## 13. Illustration Direction

Illustrations should be:

- Minimal.

- Warm.

- Local.

- Human.

- Functional.

Use illustrations primarily for:

- Onboarding.

- Empty states.

- Success states.

- Safety education.

- No-result states.

Do not add an illustration to every screen.

---

## 14. Navigation Architecture

## User Mode

Bottom navigation:

**Home | Jobs | Chat | Notifications | Profile**

## Worker Mode

Bottom navigation:

**Home | Open Jobs | My Jobs | Chat | Profile**

One account can switch between User Mode and Worker Mode.

Mode switching must not create a second account.

---

## 15. Home Screen — User

The Home screen is the most important screen.

## Header

- KaamNow logo.

- Location/area.

- Notification icon.

- Profile avatar.

## Hero section

Headline:

**What do you need today?**

Supporting text:

**Describe the work you need help with.**

Input placeholder:

**e.g. Bathroom tap is leaking**

Primary CTA:

**Find a Worker**

## Category shortcuts

- Electrician

- Plumber

- Cleaning

- Painting

- Car/Bike Wash

- Cooking

- Pet Care

- Appliance Repair

- More

Categories are shortcuts, not restrictions.

---

## 16. Home Screen — Visual Layout

Recommended hierarchy:

1. Header.

2. Large requirement hero card.

3. Quick categories.

4. Active job.

5. Trust/verified-worker section.

6. Recent jobs.

7. Bottom navigation.

The hero card should dominate the upper half of the screen without filling the entire screen.

---

## 17. Requirement Input

The requirement input must support natural-language descriptions.

Example:

> “Bathroom tap is leaking and I need someone today.”

The UI should show:

- Search/input icon.

- Multiline support.

- Clear button when text exists.

- Submit CTA.

Do not add voice input to the normal requirement flow.

---

## 18. AI Understanding Screen

After submission:

## State 1 — Analyzing

**Understanding your requirement…**

## State 2 — Detected

Example:

**Plumber**

Supporting text:

**We detected a plumbing repair from your description.**

Actions:

- Continue.

- Edit requirement.

AI must not silently modify important details.

---

## 19. Dynamic Questions

The next screen should ask only relevant questions.

## Cleaning

- Area.

- Basic/deep.

- Number of workers.

- Date/time.

- Budget.

## Electrician

- Device/problem.

- Number of items.

- Inspection.

- Date/time.

- Workers.

## Painting

- Interior/exterior.

- Area.

- Approximate size.

- Paint type.

- Workers.

- Budget.

## Plumbing

- Problem.

- Fixture.

- Quantity.

- Inspection.

- Date/time.

- Workers.

The question engine should visually feel like one continuous form, not separate disconnected screens.

---

## 20. Progress Indicator

For multi-step forms:

Example:

**1 / 4**

Use a minimal progress bar.

Active segment:

Cinnamon Wood.

Completed segment:

Toasted Almond / muted success.

Remaining:

neutral.

---

## 21. Location UI

Show:

- Current approximate area.

- Map preview where useful.

- Search radius.

Radius options:

**5 km | 10 km | 15 km | 20 km**

The selected chip uses Cinnamon Wood.

Before assignment:

- Approximate location only.

- Approximate distance only.

Exact address remains protected until the appropriate assignment stage.

---

## 22. Budget UI

For budget-oriented work:

- Budget input.

- Optional range.

- Worker count.

- Date/time.

For inspection-based work:

Show:

**Final price will be proposed after inspection.**

Never create a false fixed price.

---

## 23. Matching Screen

The matching screen is a major KaamNow differentiator.

Headline:

**Finding the right worker**

Supporting text:

**We're checking skills, availability and distance.**

## Progress

- Understanding requirement.

- Searching nearby workers.

- Checking skills.

- Checking availability.

- Finding matches.

## Visual

Use:

- Subtle map/area representation if appropriate.

- Worker markers.

- Central user location.

- Search radius ring.

- Calm animation.

Avoid overly futuristic AI graphics.

---

## 24. Radius Expansion

If no suitable worker is found:

Show:

**No suitable match in your selected area.**

Then:

**Expanding search area…**

The user must understand why the radius changed.

---

## 25. Worker Discovery Screen

Headline:

**Workers Found**

Supporting text:

**12 workers near you**

Filter control:

**Filter**

Worker cards should be vertically scrollable.

---

## 26. Worker Card

Each worker card includes:

- Profile photo.

- Name.

- Identity Verified.

- Rating.

- Completed jobs.

- Skill.

- Relevant experience.

- Approx distance.

- Availability.

- Profile action.

Example:

**Rohit Sharma ✓**

**4.8 ★ · 127 jobs · 2.3 km**

**Plumber · 5+ years**

**Available today**

CTA:

**View Profile**

---

## 27. Matching Explanation

Inside the worker profile/match area:

**Why this match?**

- Required skill.

- Distance.

- Availability.

- Relevant completed jobs.

Example:

> Plumbing skill · 3.2 km away · Available today · Similar jobs completed

Do not expose proprietary scoring weights.

---

## 28. Worker Profile

Sections:

## Header

- Profile photo.

- Name.

- Verification badge.

- Rating.

## Information

- Skills.

- Relevant experience.

- Completed jobs.

- Reviews.

- Achievements.

## Portfolio

External Google Drive portfolio link.

Do not store large portfolio media directly in the platform by default.

---

## 29. Assignment Screen

Once a worker accepts:

**Worker Assigned**

Show:

- Worker card.

- Job summary.

- Date/time.

- Number of workers.

- Agreed amount if applicable.

- Chat.

Actions:

- Open Chat.

- View Job.

- Report.

- SOS.

Do not include:

- On the Way.

- Arrived.

---

## 30. Job Status

Final flow:

**Assigned → In Progress → Done Requested → Approved → Completed → Rating**

## Stepper

Assigned:

Cinnamon Wood active marker.

In Progress:

Cinnamon Wood active marker.

Done Requested:

highlight when active.

Approved:

success treatment.

Completed:

final success state.

Rating:

post-completion action.

---

## 31. In Progress Screen

Show:

- Worker.

- Job title.

- Current status.

- Start time.

- Agreed amount.

- Chat.

- Report.

- SOS.

Worker action:

**Job Done**

---

## 32. Job Done Request

Worker presses:

**Job Done**

The user sees:

**Worker has requested completion approval.**

Actions:

**Approve Completion**

**Report an Issue**

The worker cannot directly set the job to Completed.

---

## 33. Completion Screen

After approval:

- Success indicator.

- Job summary.

- Final agreed amount.

- Completion time.

- Rating CTA.

Use a clean success card rather than a large celebratory animation.

---

## 34. Rating UI

User rates Worker.

Worker rates User.

Components:

- 1–5 stars.

- Review field.

- Optional structured feedback.

Avoid manipulative copy.

---

## 35. Chat UI

Private User ↔ Worker chat.

Features:

- Text messages.

- Timestamps.

- Job system messages.

- Agreed amount card.

- Additional work proposal.

- Report.

- SOS during active job.

Phone number is not automatically exposed.

---

## 36. Additional Work UI

Worker proposes:

- Work description.

- Additional amount.

- Reason.

User sees:

**Additional Work Requested**

Actions:

- Approve.

- Reject.

- Discuss.

The final amount updates only after approval.

---

## 37. Payment UI

Payment is direct between User and Worker.

Show:

**Agreed Amount

₹800**

Notice:

**Payment is made directly between the user and worker. KaamNow does not hold or transfer payment.**

Do not display:

- Wallet balance.

- Escrow balance.

- Platform-held funds.

- Fake payment guarantees.

Never request UPI PIN, payment OTP, or bank password.

---

## 38. Jobs Screen

Filters/tabs:

- Active.

- Completed.

- Cancelled.

- Reopened.

- Disputed.

Each job card:

- Work type.

- Worker.

- Date.

- Status.

- Amount where applicable.

---

## 39. Reopen Job

Triggers:

- Worker cancellation.

- No-show.

- Worker unavailable.

- Worker cannot complete.

UI:

**Reopen this job?**

Primary:

**Reopen Job**

Then return to matching.

---

## 40. Dispute UI

Categories:

- Worker no-show.

- User no-show.

- Fake/misleading job.

- Misbehavior.

- Harassment.

- Safety incident.

- Cancellation.

- Completion disagreement.

- Assignment issue.

- Chat/coordination.

- Policy violation.

- Other.

Evidence can reference:

- Job details.

- Relevant chat.

- Additional-work approvals.

- Reports.

The platform handles platform/job/conduct issues, not financial recovery.

---

## 41. SOS UI

SOS must be visually distinct.

## Main emergency panel

**Emergency SOS**

Actions:

- Activate SOS.

- Emergency contact.

- Emergency call flow.

- Location status.

Flow:

**Emergency Trigger → SOS Activated → Location Captured → Emergency Alert → Emergency Contact / Emergency Call Flow → SOS Safety Session**

## Audio

- Starts only after SOS activation.

- Clear recording indicator.

- Stops when SOS session ends/configured condition occurs.

- Encrypted local storage.

- No secret recording during normal use.

Do not claim guaranteed automatic police-station connection unless an actual integration exists.

---

## 42. Worker Home

Header:

- Worker name.

- Profile.

- Availability toggle.

Cards:

- New opportunities.

- Active jobs.

- Today's activity.

- Rating.

- Completed jobs.

Primary control:

**Available / Unavailable**

---

## 43. Worker Job Alert

Show:

- Work type.

- Approx distance.

- Skill.

- Date/time.

- Budget if available.

- Number of workers.

- Matching explanation.

Actions:

**Accept**

**Reject**

---

## 44. Open Jobs

Open Jobs provides opportunities to new/unverified workers.

Filters:

- Distance.

- Work type.

- Skill.

- Budget.

- Date.

- Time.

Cards:

- Job title.

- Area.

- Approx distance.

- Budget.

- Date/time.

- Required workers.

---

## 45. Worker Active Job

Status:

**Assigned → In Progress → Done Requested**

Actions:

- Start Work.

- Chat.

- Additional Work.

- Job Done.

- Report.

- SOS.

---

## 46. Worker Profile

Show:

- Photo.

- Name.

- Identity Verified.

- Verified Worker.

- Skills.

- Experience.

- Completed jobs.

- Rating.

- Reviews.

- Achievements.

- Portfolio.

- Availability.

---

## 47. Verification UI

Identity verification:

- ID type.

- Secure submission.

- Pending.

- Verified.

- Rejected.

- Review Required.

Public profile shows only:

**Identity Verified**

Actual government ID is never public.

Worker verification:

**Verified Worker after 3 user-approved completed jobs.**

---

## 48. Achievements

Examples:

- Verified Worker.

- Highly Rated.

- Quick Response.

- 50 Jobs Completed.

Achievement cards should be subtle and useful.

---

## 49. Subscription UI

Worker plan:

**30 Days Free**

Then:

**₹100/month**

During trial:

- All worker features available.

After expiry:

- Profile remains.

- Existing jobs can continue.

- New jobs cannot be accepted.

- Open Jobs unavailable.

- Renewal CTA.

Pricing and trial configuration are controlled by Admin.

---

## 50. Notifications

User:

- Job posted.

- Matching.

- Worker found.

- Assignment.

- Work started.

- Job done.

- Completion.

- Rating.

- Cancellation.

- Reopen.

- Dispute.

- Payment reminder.

- Announcement.

Worker:

- New job.

- Assignment.

- Timing.

- Cancellation.

- Reopened job.

- Rating.

- Subscription expiry.

- Announcement.

---

## 51. Profile & Settings

Sections:

- Account.

- User/Worker mode.

- Verification.

- Privacy.

- Notifications.

- Language.

- Emergency contacts.

- Safety.

- Security.

- Deactivate.

- Logout.

---

## 52. Buttons

Variants:

- Primary.

- Secondary.

- Outlined.

- Text.

- Destructive.

- Icon-only.

## Primary button

Background:

Cinnamon Wood.

Text:

Warm light/cream.

Pressed:

Toasted Almond.

## Secondary

Dark Khaki / Dark Khaki 2 depending on context.

---

## 53. Input Components

Types:

- Requirement input.

- Search.

- Multiline text.

- OTP.

- Budget.

- Number.

- Dropdown.

- Date.

- Time.

- Chips.

States:

- Default.

- Focus.

- Filled.

- Error.

- Disabled.

- Loading.

Focus indicators must remain visible.

---

## 54. Chips

Use chips for:

- Radius.

- Skill.

- Work type.

- Budget.

- Date.

- Time.

- Status.

Selected:

Cinnamon Wood.

Supporting highlight:

Toasted Almond.

---

## 55. Cards

Required cards:

- Worker card.

- Job card.

- Match card.

- Notification card.

- Subscription card.

- Achievement card.

- Safety card.

- Status card.

- Completion approval card.

- Additional-work card.

---

## 56. Loading States

Every network-dependent screen requires:

- Skeleton.

- Spinner where appropriate.

- Retry.

- Offline fallback.

Do not show blank screens.

---

## 57. Empty States

Examples:

**No Active Jobs**

“Your active jobs will appear here.”

**No Open Jobs**

“No matching jobs are available right now.”

Provide a useful action where possible.

---

## 58. Error States

Error copy must explain:

- What happened.

- Whether data was saved.

- What can be done.

Example:

**We couldn't find workers nearby.**

Actions:

**Expand Search**

**Edit Requirement**

**Try Again**

---

## 59. Offline States

Show:

- Offline banner.

- Last known state where safe.

- Retry.

Never display stale live availability as if it were current.

---

## 60. Permission UX

## Location

Explain why location is needed before asking.

## Notifications

Explain that notifications are required for job alerts.

## Microphone

Request only for SOS audio after activation and according to Android rules.

Do not request unrelated permissions during onboarding.

---

## 61. Accessibility

Minimum requirements:

- Large touch targets.

- Strong contrast.

- Screen reader labels.

- Logical focus order.

- Text scaling.

- Color-independent status communication.

- Reduced-motion support.

- Accessible SOS controls.

---

## 62. Localization

Supported:

- English.

- Hindi.

All strings must be externalizable.

Never bake UI text into images.

Allow longer Hindi strings without clipping.

---

## 63. Responsive Mobile Design

Support:

- Small Android phones.

- Standard phones.

- Large phones.

- High-density displays.

- Large accessibility fonts.

Important CTAs must remain accessible.

---

## 64. Admin / Creator Web UI

Structure:

**Sidebar + Top Bar + Main Content**

Sidebar:

- Dashboard.

- Users.

- Workers.

- Verification.

- Jobs.

- Matching.

- Reports.

- Disputes.

- Subscriptions.

- Offers.

- Ads.

- Notifications.

- Analytics.

- Settings.

- Audit.

Use the same color and component system but increase information density for desktop.

---

## 65. Admin Dashboard

KPI cards:

- Total users.

- Active users.

- Workers.

- Verified workers.

- Active subscriptions.

- Jobs.

- Completed jobs.

- Matching activity.

- Disputes.

- Subscription revenue.

Charts:

- Jobs over time.

- Matching time.

- Acceptance/rejection.

- Radius expansion.

- Subscription conversions.

- Reliability metrics.

---

## 66. Admin Tables

Tables must support:

- Search.

- Filters.

- Sorting.

- Pagination.

- Row actions.

- Status badges.

- Detail drawer/page.

---

## 67. Admin Verification

Queue:

- Pending.

- Verified.

- Rejected.

- Review required.

Sensitive identity information must be visible only to authorized admin roles.

---

## 68. Admin Jobs

Filters:

- Status.

- Work type.

- Date.

- Location.

- User.

- Worker.

- Dispute.

Job detail should show an audit timeline.

---

## 69. Admin Reports & Disputes

Flow:

**Report → Case → Evidence → Review → Resolution → Closed**

Actions:

- Warning.

- Restriction.

- Suspension.

- Verification review.

- Reassignment.

- Case closure.

All sensitive actions must be auditable.

---

## 70. Admin Subscription Controls

Admin can configure:

- Price.

- Trial duration.

- Plans.

- Offers.

- Deals.

- Discounts.

Values should be API/database driven.

---

## 71. Admin Ads & Promotions

Types:

- Banner.

- Sponsored listing.

- Offer.

- Deal.

- Announcement.

- Campaign.

Sponsored/promotional content must be clearly labelled.

---

## 72. Admin Matching Controls

Configurable:

- Skill weight.

- Distance weight.

- Availability weight.

- Rating weight.

- Experience weight.

- Search radius.

- Radius expansion.

- Smart retry.

Do not expose proprietary matching weights to normal users.

---

## 73. Component Image Documentation

Every component should eventually have a visual reference image.

Generate image sheets for:

1. Buttons.

2. Inputs.

3. Search.

4. OTP.

5. Chips.

6. Worker cards.

7. Job cards.

8. Match cards.

9. Status stepper.

10. Notification cards.

11. Achievement cards.

12. Subscription cards.

13. Verification badges.

14. Rating.

15. Reviews.

16. Chat.

17. Additional work.

18. Completion approval.

19. Empty states.

20. Loading states.

21. Error states.

22. Offline state.

23. Bottom sheets.

24. Dialogs.

25. SOS panel.

26. Admin KPI cards.

27. Admin tables.

28. Admin filters.

29. Admin case cards.

30. Admin analytics cards.

All images must use the locked KaamNow palette.

---

## 74. Screen Image Documentation

Generate visual references for at least:

## User

1. Splash.

2. Onboarding.

3. Login/OTP.

4. Home.

5. AI understanding.

6. Dynamic work details.

7. Location/radius.

8. Matching.

9. Worker discovery.

10. Worker profile.

11. Assignment.

12. Chat.

13. In Progress.

14. Job Done approval.

15. Completion.

16. Rating.

17. Jobs history.

18. Reopen.

19. Dispute.

20. SOS.

21. Notifications.

22. Profile/settings.

## Worker

23. Worker home.

24. Availability.

25. Job alert.

26. Open Jobs.

27. Filters.

28. Job details.

29. Active job.

30. Additional work.

31. Job Done.

32. Ratings.

33. Worker profile.

34. Verification.

35. Achievements.

36. Subscription.

37. SOS.

## Admin

38. Dashboard.

39. Users.

40. Workers.

41. Verification.

42. Jobs.

43. Matching.

44. Reports.

45. Disputes.

46. Subscriptions.

47. Promotions.

48. Notifications.

49. Analytics.

50. Settings.

51. Audit.

---

## 75. Five-Screen Primary Design Flow

For design presentations and AI-generated visual boards, the first five screens should represent one coherent journey:

## Screen 01 — Home

**What do you need today?**

Natural-language requirement input.

## Screen 02 — AI Work Details

Detected work type and dynamic questions.

## Screen 03 — Matching

Search radius and worker discovery progress.

## Screen 04 — Worker Discovery

Worker cards with trust and matching explanation.

## Screen 05 — Assigned Job

Assigned worker, job summary, chat and status.

Do not add On the Way or Arrived.

---

## 76. Visual Generation Prompt Rules

When generating UI images:

- Use exact KaamNow palette.

- Use realistic Android dimensions.

- Keep UI text readable.

- Use the same typography hierarchy.

- Use consistent 8-point spacing.

- Use consistent 16 dp cards.

- Use Cinnamon Wood for primary actions.

- Use Toasted Almond as controlled highlight.

- Use Dark Khaki for dark surfaces.

- Use Pitch Black for strong text.

- Use Dark Khaki 2 for supporting surfaces.

- Avoid blue/teal/purple palette contamination.

- Avoid random features.

- Avoid fake UI.

- Avoid excessive gradients.

- Avoid excessive glassmorphism.

- Avoid generic marketplace aesthetics.

- Do not include On the Way or Arrived.

- Do not invent payment-wallet functionality.

- Do not invent voice input.

- Do not imply guaranteed safety or payment.

- Keep all screens visually connected.

---

## 77. UI Content Tone

Copy should be:

- Short.

- Friendly.

- Direct.

- Human.

- Practical.

Prefer:

**Find a Worker**

instead of:

**Initiate Worker Discovery Process**

Prefer:

**Worker has requested completion approval**

instead of:

**Completion state transition pending user confirmation**

---

## 78. Interaction Rules

Every major action must have:

- Immediate visual feedback.

- Loading state if asynchronous.

- Success state.

- Error recovery.

Destructive actions require confirmation.

Critical actions should never depend only on a temporary toast.

---

## 79. Privacy Visual Rules

Always communicate:

- Approximate location before assignment.

- Exact address only when appropriate.

- Government IDs never public.

- Phone number not automatically exposed.

- Portfolio externally hosted.

- SOS recording starts only after activation.

Privacy information should be contextual and concise.

---

## 80. Trust Visual Rules

Use factual indicators:

- Identity Verified.

- Verified Worker.

- Completed jobs.

- Rating.

- Relevant experience.

- Availability.

Do not visually imply:

- Guaranteed quality.

- Guaranteed safety.

- Guaranteed payment.

- Guaranteed police response.

---

## 81. Design QA Checklist

Before approving any screen:

## Visual

- Correct palette.

- Correct typography.

- Correct spacing.

- Correct radius.

- Correct icon system.

- Correct button hierarchy.

- No random colors.

## Functional

- Correct navigation.

- Correct status.

- Correct CTA.

- Correct state.

- Correct privacy visibility.

## Responsive

- Small phone.

- Standard phone.

- Large phone.

- Large text.

## States

- Loading.

- Empty.

- Error.

- Offline.

- Disabled.

- Success.

## Safety

- SOS reachable.

- Recording only after SOS.

- Sensitive information protected.

---

## 82. Final Design Definition

KaamNow's final visual language is:

**Warm + Earthy + Premium + Practical + Local + Intelligent**

The reference-inspired visual principles provide:

- Clean discovery.

- Strong hierarchy.

- Rounded components.

- Soft surfaces.

- Low cognitive load.

- Progressive disclosure.

KaamNow's own identity comes from:

- Pitch Black `#141204`

- Dark Khaki `#262A10`

- Dark Khaki 2 `#54442B`

- Cinnamon Wood `#A9714B`

- Toasted Almond `#E8985E`

The UI must consistently represent the product journey:

**Need → AI Understanding → Dynamic Details → Matching → Worker Discovery → Assignment → Chat → In Progress → Job Done → User Approval → Completed → Rating**

This document is the final visual/UI source of truth for KaamNow.

## 83. Production Architecture Alignment

- Mobile clients use Flutter for Android and iOS. Android-specific emergency/device behavior may use Kotlin through Flutter platform channels where supported.

- The mobile app communicates with the FastAPI backend through authenticated HTTPS APIs; realtime job chat may use WebSocket.

- Cloudflare is an infrastructure/edge layer and must not be represented as consumer-facing business functionality.

- The FastAPI backend is a modular monolith. Consumer UI must not expose internal service/module terminology.

- PostgreSQL + PostGIS, Redis, Pub/Sub and R2 are backend infrastructure and should not appear as internal technical concepts in normal consumer UI.

- Firebase Cloud Messaging is the push transport; the in-app notification center must retain important notifications so missed pushes can be recovered.

- Google Maps Platform may provide map/geocoding/location UI, while approximate-location privacy and exact-address protection must remain visible at the correct stages.

- AI assists requirement understanding and clarification. UI must preserve user control and must not imply AI certainty.

- Job payment UI represents direct User → Worker payment and must not display wallet, escrow, platform-held funds or financial guarantees.

- Worker subscription is separate from job payment. Current product configuration is ₹100/month after a 30-day free trial and entitlement is authoritative on the backend.

- SOS UI must not imply universal hardware-button support, guaranteed police dispatch, or normal-use recording.

- SOS recording indicators appear only during an activated SOS session; normal app screens never show recording as active.

## 84. Production UI Acceptance Additions

- Android and iOS layouts are both covered; no critical flow depends on Android-only visual assumptions.

- Permission-denied states exist for location, notifications and SOS microphone access.

- Offline/reconnect behavior is designed for job status, chat and matching.

- Expired worker subscription blocks new job acceptance/Open Jobs while preserving existing/ongoing job access according to the PRD.

- Assignment, completion approval and retry actions prevent duplicate operations and show processing state.

- Payment screens clearly distinguish the agreed amount from actual external payment completion.

- Exact address never appears in pre-assignment worker discovery cards.

- Government identity documents never appear in normal public profiles.

- Dispute screens explain platform review without promising financial recovery.

- SOS remains reachable from active-job contexts and uses high-contrast emergency treatment.

- AI question generation has loading, retry and deterministic/manual fallback states.

- Every network-dependent primary flow has loading, empty, error and offline states.
