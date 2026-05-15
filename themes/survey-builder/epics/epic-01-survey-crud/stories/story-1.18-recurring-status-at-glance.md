## Story 1.18 — Understand status at a glance for recurring surveys

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to see the current instance's status for a recurring survey
### So that I know whether it's currently active without drilling into each instance

### Acceptance criteria
- Given a recurring survey with multiple instances, when I view it in the list, then I see the status of the current/most recent instance
- Given a recurring survey, when I click into it, then I can see a list of past instances with their completion statistics

### Test plan
- Unit: Validate that the survey list query returns current instance status for recurring surveys; validate that the survey detail endpoint returns instance history with completion stats
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.18 — Recurring status at a glance.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.18-recurring-status-at-glance.md.
>  Key constraints: (1) The survey list row for a recurring survey shows the current/most recent instance status, not the series status; (2) The detail view includes instance history — this is a list of past SurveyInstances with send date, close date, and completion %; (3) This story is UI-only for displaying what exists — the instance lifecycle itself is in epic-03-scheduling.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
