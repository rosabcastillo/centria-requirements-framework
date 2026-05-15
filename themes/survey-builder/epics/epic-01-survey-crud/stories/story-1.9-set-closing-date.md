## Story 1.9 — Set a closing date

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to optionally set a date on which the survey closes automatically
### So that I don't have to remember to close it manually

### Acceptance criteria
- Given a survey, when I set a closing date that is after the send date, then the survey closes automatically on that date
- Given a survey, when I do not set a closing date, then the survey stays live until I close it manually
- Given a closing date set before the send date, when I try to publish, then validation blocks publishing with a clear message

### Test plan
- Unit: Validate that closing date before send date fails pre-publish validation; validate that omitting closing date is a valid state; validate automatic closure fires at closing date (use mocked clock)
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.9 — Set a closing date.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.9-set-closing-date.md.
>  Key constraints: (1) Closing date is optional — null is valid; (2) Closing date must be validated as after send date, not just after today; (3) Automatic closure is handled by the background scheduler (story 1.15) — this story covers the configuration UI and validation only; (4) Store closing date in the schedule JSON on the surveys table.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
