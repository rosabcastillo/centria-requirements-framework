# Epic 04 — Reminders & Notifications

**Status:** ⬜ Ready
**Jira Epic:** [link]
**Repos:** survey-service, notification-service
**Target:** Weeks 10–11

## Goal
Parents receive timely, non-intrusive reminders to complete surveys. Admins configure reminder cadence per survey.

## Definition of Done
- [ ] Admin can toggle reminders on/off per survey and set cadence (default 2 days)
- [ ] Push notifications dispatched on schedule per cadence
- [ ] Quiet hours enforced (5pm–8pm parent local timezone — pending clinical confirmation)
- [ ] Parent can override personal notification preference
- [ ] Completing a survey suppresses all remaining reminders for that instance

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-4.1-reminder-cadence-config | Configure reminder cadence per survey | ⬜ Ready |
| story-4.2-toggle-reminders | Toggle reminders on/off | ⬜ Ready |
| story-4.3-push-notification-dispatch | Push notification dispatch | ⬜ Ready |
| story-4.4-quiet-hours-enforcement | Quiet hours enforcement | ⬜ Ready |
| story-4.5-parent-reminder-override | Parent personal notification override | ⬜ Ready |
| story-4.6-completion-suppression | Suppress reminders on completion | ⬜ Ready |

## Key constraints
- Default cadence: every 2 days (admin can change)
- Quiet hours: 5pm–8pm parent local timezone — OPEN DECISION #1, working assumption only
- Completion suppresses ALL pending reminders for that instance
- Push notification only at MVP
- Stories 4.4 depends on open decision #1 being confirmed — can build with working assumption, flag for update
