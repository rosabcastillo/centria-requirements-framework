## Story 3.6 — New family members receive the current instance

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want families added to the caseload mid-cycle to receive the current active instance
### So that new families are not left out

### Acceptance criteria
- Given an active recurring survey for a market, when a new family joins that market, then they receive the current open instance
- Given a family discharged from the caseload, when the next recurring instance is created, then that family does not receive it

### Test plan
- Unit: Validate that a family added mid-cycle gets a SurveyAssignment for the currently live instance; validate that discharged families are excluded from new instance assignment creation; validate the caseload eligibility check used by the scheduler
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.6 — New family members receive current instance.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.6-new-family-members.md.
>  Key constraints: (1) When a new family is added to a market that has an active survey, create a SurveyAssignment for the current live instance; (2) When the scheduler creates a new instance, it queries for active (non-discharged) families in the market — discharged families must not receive new assignments; (3) The definition of 'active' and 'discharged' comes from the existing CareConnect caseload — consult the existing caseload service or model.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
