## Story 3.11 — Deactivate a recurring series

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to stop future instances of a recurring series without deleting the survey
### So that I can pause or end a recurring program while retaining historical data

### Acceptance criteria
- Given a recurring survey, when I click "Deactivate series" and confirm, then no new instances are created after the current one completes
- Given a deactivated series, when I view its status, then it shows "Deactivated" and past instances remain accessible
- Given a deactivated series, when I want to restart it, then I can re-configure a new schedule and re-activate

### Test plan
- Unit: Validate that deactivation sets a flag preventing the scheduler from creating new instances; validate that past instances are not deleted on deactivation; validate that re-activation with a new schedule creates new instances correctly
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.11 — Deactivate a recurring series.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.11-deactivate-recurring-series.md.
>  Key constraints: (1) Deactivation does not delete the survey — it stops the scheduler from creating new instances; (2) Store a deactivated_at timestamp or is_active flag on the series; (3) The current in-flight instance is not immediately closed — it completes normally; (4) Audit log the deactivation event; (5) Re-activation path: admin re-configures a schedule and publishes again.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
