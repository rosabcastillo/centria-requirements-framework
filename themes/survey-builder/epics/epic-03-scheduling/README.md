# Epic 03 — Recurring & Event-Triggered Scheduling

**Status:** ⬜ Ready
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin
**Target:** Weeks 8–9

## Goal
Surveys send automatically on a repeating schedule or in response to a clinical event.

## Definition of Done
- [ ] One-time, recurring, and manual sends work end-to-end
- [ ] Google Calendar–style recurrence patterns (RRULE) supported
- [ ] "Next 5 dates" preview shows correct upcoming sends
- [ ] New recurring instance automatically closes previous instance
- [ ] New families mid-cycle receive current instance; discharged families excluded
- [ ] Manual one-off send available on any published survey
- [ ] Event-triggered survey can be configured (post-97156 at MVP) — stories Q1–Q3 BLOCKED
- [ ] Admin can deactivate a recurring series without deleting it
- [ ] Mocked-clock testing infrastructure in place

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-3.1-configure-recurring-schedule | Configure a recurring schedule | ⬜ Ready |
| story-3.2-set-series-dates | Set start and optional end date for recurring series | ⬜ Ready |
| story-3.3-manual-one-off-send | Send a manual one-off survey | ⬜ Ready |
| story-3.4-recurring-instance-lifecycle | Each recurring send creates a new independent instance | ⬜ Ready |
| story-3.5-view-instance-history | View instance history for a recurring survey | ⬜ Ready |
| story-3.6-new-family-members | New family members receive the current instance | ⬜ Ready |
| story-3.7-configure-event-triggered | Configure a survey to trigger on a clinical event | 🚫 Blocked |
| story-3.8-event-triggered-instance | Event-triggered instance created per qualifying event | 🚫 Blocked |
| story-3.9-view-event-triggered-history | View event-triggered instances in survey history | 🚫 Blocked |
| story-3.10-see-upcoming-sends | See upcoming scheduled sends | ⬜ Ready |
| story-3.11-deactivate-recurring-series | Deactivate a recurring series | ⬜ Ready |
| story-3.12-distinguish-survey-types | Distinguish survey types in list view | ⬜ Ready |
| story-3.13-preview-schedule | Preview the schedule before publishing | ⬜ Ready |

## Key constraints
- Recurring: Google Calendar–style RRULE patterns + custom interval fallback
- When new instance opens, previous closes regardless of completion status
- Market-based audience targeting required
- Stories 3.7, 3.8, 3.9: 🚫 BLOCKED — waiting on event-trigger architecture decision (Kerri + Timothy + Emily + Son + Harish). Do NOT start until unblocked.
- Mocked-clock testing infrastructure required for scheduler tests
