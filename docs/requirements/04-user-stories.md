# Survey Builder — User Stories

All user stories written to date, in INVEST format with acceptance criteria.
Stories are organized by epic. Stories marked (PARTIAL) have been started but not fully detailed.

---

# Epic 01 — Survey Creation & Status Management

## Group A — Foundations: Likert Label Sets

### A1 — Manage the Likert label set library

**As a** survey administrator
**I want** to create, update, and manage a library of reusable Likert label sets
**So that** I can quickly apply consistent scales across multiple surveys without retyping them.

**Acceptance criteria:**

*Creating a label set:*
- Given I am a survey administrator, when I navigate to the Likert label set library, then I see a list of all existing label sets and a button to create a new one
- Given I click "Create label set," when I enter a name and five point labels, then the new set appears in the library
- Given I try to save a label set with fewer than five labels defined, when I click Save, then an error message tells me all five labels are required

*Editing a label set:*
- Given an existing label set, when I edit its name or any label and save, then the updated version replaces the old one in the library
- Given a label set is already in use on a published survey, when I edit that label set, then the change is reflected on future surveys using it but does NOT retroactively change historical responses

*Deleting a label set:*
- Given a label set not used by any survey, when I delete it, then it is removed from the library
- Given a label set used by at least one survey, when I try to delete it, then I am told it cannot be deleted while in use

**Test scenarios:**
1. Create a "Frequency" scale (Never / Rarely / Sometimes / Often / Always) — confirm it appears in the library
2. Edit an existing scale mid-survey — confirm historical data unaffected
3. Delete an in-use scale — confirm deletion is blocked with a clear message

---

### A2 — Default label set pre-loaded

**As a** survey administrator
**I want** a standard agree-disagree Likert scale available from day one
**So that** I don't have to create the most common scale from scratch.

**Acceptance criteria:**
- Given the system is set up for the first time, when I open the Likert label set library, then "Strongly Disagree / Disagree / Neutral / Agree / Strongly Agree" is already available
- Given this default label set, when I try to delete it, then I am told the default set cannot be deleted
- Given the default set, when I use it in a question, then it behaves identically to any other label set (including the ability to override labels at the question level)

---

## Group B — Drafting

### B1 — Create a new survey draft

**As a** survey administrator
**I want** to create a new blank survey draft with a title
**So that** I have a starting point I can build on over time.

**Acceptance criteria:**
- Given I am logged in as a survey administrator, when I click "Create Survey," then a blank draft is created and I am taken to the survey builder
- Given a new draft, when I look at its status, then it shows "Draft"
- Given a new draft, when I have not added any title, then a placeholder title ("Untitled Survey") is shown and I am prompted to add one
- Given I enter a title and navigate away, when I return to the survey, then my title has been saved automatically
- Given I am a VP-level user who did not create this draft, when I find it in the survey list, then I can view it but the edit controls are disabled

**Test scenarios:**
1. Create a survey, add a title, navigate away, return — confirm title persisted
2. Log in as a different VP-level user — confirm edit is disabled (read-only)

---

### B2 — Edit a draft survey

**As a** survey administrator
**I want** to freely edit all aspects of a survey while it is in Draft status
**So that** I can refine it before publishing.

**Acceptance criteria:**
- Given a draft survey, when I edit the title, description, or any question, then my changes are preserved
- Given a scheduled survey whose send time has not yet arrived, when I edit it, then my changes are preserved (same freedom as Draft)
- Given a live survey, when I try to edit any field, then all editing is disabled with a message that live surveys cannot be edited
- Given a closed survey, when I try to edit any field, then all editing is disabled — I am offered the option to duplicate instead

---

### B3 — See what's missing before I can publish

**As a** survey administrator
**I want** to see a clear validation summary of everything that needs to be fixed before I can publish
**So that** I don't discover problems at the last minute.

**Acceptance criteria:**
- Given a draft with missing required fields, when I click "Publish," then a validation panel shows a list of specific issues (e.g., "No questions added," "No schedule set," "Section has no questions")
- Given all validation issues are resolved, when I click "Publish," then publishing proceeds without showing the validation panel
- Given the validation panel is showing, when I click a listed issue, then I am taken directly to the area that needs fixing

**Test scenarios:**
1. Try to publish with no questions — confirm specific error shown
2. Try to publish with no schedule — confirm specific error shown
3. Try to publish with an empty section — confirm specific error shown

---

### B4 — Save my work explicitly

**As a** survey administrator
**I want** to be able to save my work at any time with an explicit "Save" action
**So that** I know my progress is preserved, in addition to auto-save.

**Acceptance criteria:**
- Given I am in the survey builder, when I click "Save," then a confirmation appears that my changes have been saved
- Given I make changes and then navigate away without saving, when I return, then my changes are still present (auto-save is also active)
- Given I make changes and my browser crashes, when I return to the survey, then my last auto-saved state is restored

---

### B5 — Discard a draft

**As a** survey administrator
**I want** to permanently delete a draft survey I no longer need
**So that** the survey list doesn't accumulate abandoned drafts.

**Acceptance criteria:**
- Given a draft survey, when I click "Delete" and confirm, then the survey is permanently removed
- Given a scheduled or live survey, when I try to delete it, then deletion is blocked and I am told only drafts can be deleted (I must close a live survey first, then delete)
- Given I click "Delete," when I see the confirmation dialog, then it clearly states this action is permanent and cannot be undone

---

## Group C — Scheduling

### C1 — Configure a one-time schedule

**As a** survey administrator
**I want** to set a specific date and time for a survey to be sent
**So that** it reaches parents at the right moment.

**Acceptance criteria:**
- Given a draft survey, when I open the Schedule section, then I can select "One-time" as the send type
- Given I select One-time, when I choose a date and time, then that selection is saved with the survey
- Given a scheduled send time in the past, when I try to publish, then validation blocks publishing with a message that the send time must be in the future
- Given a one-time survey that has been sent, when I view it, then the status shows "Live"

**Test scenarios:**
1. Set a schedule time 2 minutes in the future — confirm survey goes live automatically
2. Try to set a schedule in the past — confirm validation error

---

### C2 — Set a closing date

**As a** survey administrator
**I want** to optionally set a date on which the survey closes automatically
**So that** I don't have to remember to close it manually.

**Acceptance criteria:**
- Given a survey, when I set a closing date that is after the send date, then the survey closes automatically on that date
- Given a survey, when I do not set a closing date, then the survey stays live until I close it manually
- Given a closing date set before the send date, when I try to publish, then validation blocks publishing with a clear message

---

### C3 — Define the survey audience

**As a** survey administrator
**I want** to target a survey to a specific market
**So that** it only reaches the families in the relevant locations.

**Acceptance criteria:**
- Given a survey, when I open the audience settings, then I can select one or more markets
- Given I select a market, when the survey is sent, then only families associated with that market receive it
- Given I want to send to multiple markets, when I create separate survey instances per market, then each instance targets its own market correctly (no batch targeting UI — handled by duplication)
- Given no market is selected, when I try to publish, then validation blocks publishing with a message that audience is required

---

## Group D — Publishing & Lifecycle

### D1 — Publish a survey

**As a** survey administrator
**I want** to publish a survey once it is ready
**So that** it enters the delivery pipeline.

**Acceptance criteria:**
- Given a valid draft with a schedule and audience, when I click "Publish" and confirm, then the survey transitions to "Scheduled" status
- Given a survey scheduled for immediate delivery (send time = now or past within a grace period), when I publish it, then the status transitions directly to "Live"
- Given I publish a survey, when I view the audit trail, then a "Published" entry appears with my name and the timestamp
- Given a survey with at least one validation error, when I click "Publish," then a validation summary appears and publishing is blocked

**Test scenarios:**
1. Publish a valid scheduled survey — confirm status = Scheduled, audit entry created
2. Publish with send time set to "now" — confirm status = Live

---

### D2 — Move a scheduled survey back to draft

**As a** survey administrator
**I want** to revert a scheduled survey back to draft if I need to make changes before it sends
**So that** I don't have to delete and recreate it.

**Acceptance criteria:**
- Given a scheduled survey whose send time has not yet passed, when I click "Revert to Draft," then the status changes to Draft and I can edit it again
- Given a live survey, when I look for a "Revert to Draft" option, then it is not available (live surveys cannot be reverted — only closed)
- Given I revert a scheduled survey, when I view the audit trail, then a "Reverted to Draft" entry appears

---

### D3 — Survey goes live automatically

**As a** survey administrator
**I want** a scheduled survey to transition to "Live" status automatically at its scheduled send time
**So that** I don't need to be present to trigger delivery.

**Acceptance criteria:**
- Given a survey scheduled for a future time, when that time arrives, then the status automatically changes to "Live" and the survey is dispatched to the target audience
- Given a survey that went live, when I check the audit trail, then an automated "Status changed to Live" entry appears with the timestamp

---

### D4 — Close a live survey manually

**As a** survey administrator
**I want** to close a live survey manually before its scheduled end date
**So that** I can stop collecting responses when I have enough data or if a problem is discovered.

**Acceptance criteria:**
- Given a live survey, when I click "Close Survey" and confirm, then the survey status changes to "Closed" and no new responses can be submitted
- Given I confirm closure, when a dialog shows me how many responses are in progress, then I can make an informed decision
- Given a closed survey, when a parent tries to submit a response, then they see a message that the survey is no longer accepting responses
- Given I close a survey, when I view the audit trail, then a "Closed" entry appears with my name and timestamp

**Test scenarios:**
1. Close a survey with 5 in-progress responses — confirm in-progress count shown in dialog
2. Confirm closed survey rejects new submissions

---

### D5 — Survey closes automatically

**As a** survey administrator
**I want** a survey to close automatically on its configured closing date
**So that** I don't have to monitor it manually.

**Acceptance criteria:**
- Given a survey with a closing date, when that date arrives, then the status changes to "Closed" automatically
- Given the survey closes automatically, when I check the audit trail, then an automated "Status changed to Closed" entry appears

---

### D6 — Duplicate a survey

**As a** survey administrator
**I want** to duplicate a closed or existing survey
**So that** I can create a new version or reuse the same structure for a different audience or time period.

**Acceptance criteria:**
- Given any survey (in any status), when I click "Duplicate," then a new draft is created with the same title (prefixed "Copy of"), same questions, same sections, and same schedule structure — but with no audience, no send date, and status = Draft
- Given I duplicate a survey, when I view the duplicate, then the original's responses are not included
- Given a closed survey, when duplication is the primary recovery path shown, then the "Duplicate" button is prominently visible

---

## Group E — Visibility

### E1 — See all surveys in a list

**As a** survey administrator
**I want** to see all surveys I have access to in a filterable list
**So that** I can quickly find and manage any survey.

**Acceptance criteria:**
- Given I am a survey administrator, when I navigate to the Surveys section, then I see a list of all surveys I created, plus all surveys by other admins (read-only for others)
- Given the survey list, when I filter by status (Draft / Scheduled / Live / Closed), then only matching surveys appear
- Given the survey list, when I search by survey name, then matching surveys appear
- Given the survey list, when I filter by creator, then only that creator's surveys appear
- Given the survey list is empty, when I load it, then an empty state is shown with a "Create your first survey" prompt
- Given the list has surveys, when I look at each row, then I see: name, status badge, type, last sent date, completion percentage

**Status badge colors:**
- Live: teal
- Scheduled: amber
- Draft: gray
- Closed: gray (muted)

---

### E2 — Understand status at a glance for recurring surveys

**As a** survey administrator
**I want** to see the current instance's status for a recurring survey
**So that** I know whether it's currently active without drilling into each instance.

**Acceptance criteria:**
- Given a recurring survey with multiple instances, when I view it in the list, then I see the status of the current/most recent instance
- Given a recurring survey, when I click into it, then I can see a list of past instances with their completion statistics

---

## Group F — Testing Support

### F1 — Simulate parent responses for testing

**As a** developer or QA tester
**I want** to seed test responses for a survey
**So that** I can verify reporting and completion logic without involving real families.

**Acceptance criteria:**
- Given a test environment, when I use the seeding tool to generate N responses for a survey, then the system records those responses as if real parents submitted them
- Given seeded responses, when I view survey results, then they appear in the aggregation and reporting views
- Given I seed responses for a branching survey, when I review the results, then skipped questions are recorded as `was_skipped = true` and appear correctly in reporting

---

# Epic 03 — Recurring & Event-Triggered Scheduling

## Group O — Recurring Schedule Authoring

### O1 — Configure a recurring schedule using calendar-style patterns

**As a** survey administrator
**I want** to set a recurring schedule using familiar calendar-style recurrence options
**So that** I can configure the survey to send on a consistent cadence without manual intervention each time.

**Acceptance criteria:**
- Given I am configuring a survey, when I select "Recurring" as the send type, then I see pattern options consistent with Google Calendar–style recurrence: daily, weekly (on specific days), monthly (on a date or day of week), and a custom interval option
- Given I select a weekly pattern on Mondays, when the schedule is saved, then the survey will be sent every Monday
- Given I select a custom interval of 14 days, when the schedule is saved, then the survey will be sent every 14 days from the configured start date
- Given I select a recurring pattern, when I preview the schedule, then I see the next 5 planned send dates

**Test scenarios:**
1. Set weekly on Monday and Wednesday — confirm next 5 dates shown are correct
2. Set 30-day interval starting today — confirm next instance date is 30 days from today

---

### O2 — Set a start and optional end date for a recurring series

**As a** survey administrator
**I want** to define when the recurring series starts and optionally when it ends
**So that** the survey runs only during the intended period.

**Acceptance criteria:**
- Given a recurring schedule, when I set a start date, then the first instance sends on that date
- Given I set an optional end date, when that date passes, then no new instances are created
- Given I do not set an end date, when the series is active, then it continues indefinitely until I manually deactivate it
- Given I try to set an end date before the start date, when I save, then validation blocks saving with a clear message

---

### O3 — Send a manual one-off survey outside the schedule

**As a** survey administrator
**I want** to send a survey to a specific audience manually, independent of any scheduled cadence
**So that** I can handle ad-hoc situations or recover from a scheduling failure.

**Acceptance criteria:**
- Given a published survey, when I click "Send Now," then a confirmation asks me to confirm the audience and send
- Given I confirm a manual send, when the dispatch is complete, then a new survey instance is created and the audience receives it
- Given a manual send, when I view the survey history, then this instance is labeled "Manual send" alongside its send date and completion statistics

---

## Group P — Recurring Instance Lifecycle

### P1 — Each recurring send creates a new independent instance

**As a** survey administrator
**I want** each recurring send to be tracked as its own instance
**So that** I can see completion and responses per occurrence.

**Acceptance criteria:**
- Given a recurring survey, when a new instance is created, then the previous instance is automatically closed regardless of completion status
- Given the new instance is created, when I view the survey, then I can see the new instance is "Live" and previous instances are "Closed"
- Given a parent who did not complete the previous instance, when a new instance opens, then they receive the new survey (not the old one)

---

### P2 — View instance history for a recurring survey

**As a** survey administrator
**I want** to see all past instances of a recurring survey with their statistics
**So that** I can track trends and completion rates over time.

**Acceptance criteria:**
- Given a recurring survey with 3 completed instances, when I open the survey detail, then I see a list of all instances with their send date, close date, and completion percentage
- Given the instance list, when I click on a past instance, then I can view the responses and aggregated results for that instance

---

### P3 — New family members receive the current instance

**As a** survey administrator
**I want** families added to the caseload mid-cycle to receive the current active instance
**So that** new families are not left out.

**Acceptance criteria:**
- Given an active recurring survey for a market, when a new family joins that market, then they receive the current open instance
- Given a family discharged from the caseload, when the next recurring instance is created, then that family does not receive it

---

## Group Q — Event-Triggered Scheduling

### Q1 — Configure a survey to trigger on a clinical event

**As a** survey administrator
**I want** to configure a survey to send automatically when a specific clinical event occurs
**So that** I can capture timely feedback without manual scheduling.

**Acceptance criteria:**
- Given I am configuring a survey, when I select "Event-triggered" as the send type, then I see a dropdown of available clinical events
- Given the available events at MVP include only "Post-97156 session completion," when I select it, then the survey will be sent each time a 97156 session note is completed for a family in the target audience
- Given I configure an event-triggered survey, when I preview what will happen, then I see a description: "This survey will be sent to [audience] each time a 97156 session note is completed"

---

### Q2 — Event-triggered instance is created per qualifying event

**As a** survey administrator
**I want** each qualifying clinical event to generate a new survey send
**So that** outcome data is captured consistently for every relevant session.

**Acceptance criteria:**
- Given a 97156 session note is completed for a family in the survey's audience, when the event fires, then the family receives the survey
- Given the same family has an open instance from a previous event, when a new event fires, then a new instance is created (the system does not suppress the send due to an existing open instance — unless a business rule is explicitly configured)
- Given the event fires for a family not in the survey audience, when the system processes it, then no survey is sent to that family

---

### Q3 — View event-triggered instances in survey history

**As a** survey administrator
**I want** to see all instances triggered by clinical events
**So that** I can audit which events resulted in survey sends.

**Acceptance criteria:**
- Given an event-triggered survey with multiple instances, when I view the survey history, then I see each instance labeled with the event type and timestamp that triggered it
- Given I click on an instance, when I view its detail, then I can see the completion statistics for that send

---

## Group R — Visibility and Admin UX

### R1 — See upcoming scheduled sends

**As a** survey administrator
**I want** to see the next planned send dates for a recurring survey
**So that** I can anticipate when instances will go out and plan accordingly.

**Acceptance criteria:**
- Given a recurring survey, when I open its schedule settings, then I see the next 5 planned send dates listed
- Given the schedule has an end date, when all remaining sends are within view, then I see all remaining dates (not limited to 5)
- Given I change the recurrence pattern, when I save, then the upcoming dates list updates immediately

---

### R2 — Deactivate a recurring series

**As a** survey administrator
**I want** to stop future instances of a recurring series without deleting the survey
**So that** I can pause or end a recurring program while retaining historical data.

**Acceptance criteria:**
- Given a recurring survey, when I click "Deactivate series" and confirm, then no new instances are created after the current one completes
- Given a deactivated series, when I view its status, then it shows "Deactivated" and past instances remain accessible
- Given a deactivated series, when I want to restart it, then I can re-configure a new schedule and re-activate

---

### R3 — Distinguish survey types in the list view

**As a** survey administrator
**I want** to see at a glance whether a survey is one-time, recurring, or event-triggered
**So that** I can manage them without opening each one.

**Acceptance criteria:**
- Given the survey list, when I look at any row, then the survey type (One-time / Recurring / Event-triggered) is visible as a label or icon
- Given a recurring survey currently in an active instance, when I look at its row, then I see both the type and the current instance's status

---

### R4 — Preview the schedule before publishing

**As a** survey administrator
**I want** to preview what the schedule will look like before I commit to publishing
**So that** I can catch any misconfiguration before it affects families.

**Acceptance criteria:**
- Given I have configured a recurring schedule, when I click "Preview schedule," then I see the next 5 instance dates in a simple list view
- Given I review the preview and spot an error, when I go back and fix the schedule, then the preview updates to reflect the corrected dates
- Given a one-time send, when I view the schedule summary, then I see the single send date and time clearly stated

---

# Epic 04 — Reminders & Notifications
*(Stories in progress — to be detailed in next session)*

## Stories planned:
- Reminder cadence configuration (admin per-survey)
- Push notification dispatch
- Quiet hours enforcement
- Parent personal override
- Completion suppression of pending reminders

---

# Epic 05 — Gating
*(Stories planned — to be detailed)*

## Stories planned:
- Gating flag configuration (Super Admin only)
- Gating delay model (days after sending)
- Blur overlay UX
- Gate lift on completion

---

# Epic 06 — Reporting & Aggregation
*(Stories planned — to be detailed)*

## Stories planned:
- Per-question result aggregation
- Cross-instance trend view
- Completion statistics
- Skipped vs. unanswered distinction in reporting
