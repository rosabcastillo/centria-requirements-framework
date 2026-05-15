## Story 1.8 — Configure a one-time schedule

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to set a specific date and time for a survey to be sent
### So that it reaches parents at the right moment

### Acceptance criteria
- Given a draft survey, when I open the Schedule section, then I can select "One-time" as the send type
- Given I select One-time, when I choose a date and time, then that selection is saved with the survey
- Given a scheduled send time in the past, when I try to publish, then validation blocks publishing with a message that the send time must be in the future
- Given a one-time survey that has been sent, when I view it, then the status shows "Live"

### Test plan
- Unit: Validate that a past send time fails pre-publish validation; validate that a future send time saves correctly; validate that the survey transitions to Live at its send time (use mocked clock)
- E2E scenario: E2E-01-01 (schedule step)
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.8 — Configure a one-time schedule.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.8-configure-one-time-schedule.md.
>  Key constraints: (1) Send time must be validated as future at both UI and API level; (2) Schedule is stored as JSON on the surveys table (see M1.1 data model); (3) Do not use a date library without checking /docs/architecture/ for the approved library — this is an open decision; (4) The transition to Live at send time is covered in story 1.13 (scheduler) — this story covers configuration only.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
