## Story 1.13 — Survey goes live automatically

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want a scheduled survey to transition to "Live" status automatically at its scheduled send time
### So that I don't need to be present to trigger delivery

### Acceptance criteria
- Given a survey scheduled for a future time, when that time arrives, then the status automatically changes to "Live" and the survey is dispatched to the target audience
- Given a survey that went live, when I check the audit trail, then an automated "Status changed to Live" entry appears with the timestamp

### Test plan
- Unit: Validate background job/scheduler evaluates surveys at the correct time using a mocked clock; validate scheduled → live transition; validate audit log entry is created with the automated actor label
- E2E scenario: E2E-01-01 (status transition step — requires mocked clock in test)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.13 — Survey goes live automatically.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.13-survey-goes-live-automatically.md.
>  Key constraints: (1) A background scheduler (cron job or hosted service) evaluates surveys due to go live; (2) Mocked-clock testing infrastructure is required — do not test with real time.sleep(); (3) Audit log the automated transition using the existing helper service — actor should be system/scheduler, not a user; (4) This transition triggers SurveyAssignment creation for the target market audience.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
