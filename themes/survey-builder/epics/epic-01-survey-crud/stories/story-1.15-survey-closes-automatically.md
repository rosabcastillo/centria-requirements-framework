## Story 1.15 — Survey closes automatically

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want a survey to close automatically on its configured closing date
### So that I don't have to monitor it manually

### Acceptance criteria
- Given a survey with a closing date, when that date arrives, then the status changes to "Closed" automatically
- Given the survey closes automatically, when I check the audit trail, then an automated "Status changed to Closed" entry appears

### Test plan
- Unit: Validate background scheduler evaluates surveys due to close using a mocked clock; validate live → closed transition fires at closing date; validate audit log entry with automated actor label
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.15 — Survey closes automatically.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.15-survey-closes-automatically.md.
>  Key constraints: (1) Same background scheduler as story 1.13 — extend it to also close surveys past their closing date; (2) Mocked-clock testing required; (3) Audit log the automated close using the existing helper service — actor = system/scheduler; (4) Surveys without a closing date are never auto-closed by this job.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
