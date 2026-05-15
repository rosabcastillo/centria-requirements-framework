## Story 3.4 — Each recurring send creates a new independent instance

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want each recurring send to be tracked as its own instance
### So that I can see completion and responses per occurrence

### Acceptance criteria
- Given a recurring survey, when a new instance is created, then the previous instance is automatically closed regardless of completion status
- Given the new instance is created, when I view the survey, then I can see the new instance is "Live" and previous instances are "Closed"
- Given a parent who did not complete the previous instance, when a new instance opens, then they receive the new survey (not the old one)

### Test plan
- Unit: Validate that creating a new instance transitions the previous instance to Closed; validate that parents assigned to the previous instance receive a new assignment for the current instance; validate mocked-clock test for the instance transition timing
- E2E scenario: E2E-03-01 (lifecycle step)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.4 — Recurring instance lifecycle.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.4-recurring-instance-lifecycle.md.
>  Key constraints: (1) When the scheduler creates a new recurring instance, the immediately previous instance must be automatically closed — regardless of whether parents completed it; (2) SurveyAssignments for the new instance are created for currently active families in the market — discharged families are excluded; (3) Mocked-clock testing required; (4) Audit log both the new instance creation and the previous instance closure.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
