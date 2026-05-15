## Story 1.14 — Close a live survey manually

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to close a live survey manually before its scheduled end date
### So that I can stop collecting responses when I have enough data or if a problem is discovered

### Acceptance criteria
- Given a live survey, when I click "Close Survey" and confirm, then the survey status changes to "Closed" and no new responses can be submitted
- Given I confirm closure, when a dialog shows me how many responses are in progress, then I can make an informed decision
- Given a closed survey, when a parent tries to submit a response, then they see a message that the survey is no longer accepting responses
- Given I close a survey, when I view the audit trail, then a "Closed" entry appears with my name and timestamp

### Test plan
- Unit: Validate live → closed transition; validate that the API returns 409 or similar for new response submissions on closed surveys; validate in-progress count is returned in the close confirmation payload; validate audit log entry on manual close
- E2E scenario: E2E-01-01 (close step)
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.14 — Close a live survey manually.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.14-close-live-survey-manually.md.
>  Key constraints: (1) Pre-close dialog must show count of in-progress responses (SurveyAssignment records with status = in_progress); (2) After closure, the API must reject new response submissions with a clear error message; (3) Audit log the manual close using the existing helper service; (4) In-progress responses remain submittable for a grace period (check M5.6 spec — default 24h).
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
