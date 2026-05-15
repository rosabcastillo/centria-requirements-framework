## Story 3.2 — Set a start and optional end date for a recurring series

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to define when the recurring series starts and optionally when it ends
### So that the survey runs only during the intended period

### Acceptance criteria
- Given a recurring schedule, when I set a start date, then the first instance sends on that date
- Given I set an optional end date, when that date passes, then no new instances are created
- Given I do not set an end date, when the series is active, then it continues indefinitely until I manually deactivate it
- Given I try to set an end date before the start date, when I save, then validation blocks saving with a clear message

### Test plan
- Unit: Validate end date before start date fails validation; validate that no instances are created after end date; validate that an absent end date results in indefinite series (scheduler keeps creating instances until deactivated)
- E2E scenario: E2E-03-01 (date configuration step)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.2 — Set series dates.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.2-set-series-dates.md.
>  Key constraints: (1) End date is optional — null means run indefinitely; (2) Validation: end date must be after start date; (3) When end date is set, the background scheduler must check it before creating a new instance; (4) Series end date is stored in the schedule JSON on the surveys table alongside the RRULE.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
