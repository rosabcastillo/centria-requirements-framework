## Story 1.11 — Publish a survey

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to publish a survey once it is ready
### So that it enters the delivery pipeline

### Acceptance criteria
- Given a valid draft with a schedule and audience, when I click "Publish" and confirm, then the survey transitions to "Scheduled" status
- Given a survey scheduled for immediate delivery (send time = now or past within a grace period), when I publish it, then the status transitions directly to "Live"
- Given I publish a survey, when I view the audit trail, then a "Published" entry appears with my name and the timestamp
- Given a survey with at least one validation error, when I click "Publish," then a validation summary appears and publishing is blocked

### Test plan
- Unit: Validate draft → scheduled transition; validate draft → live transition for immediate sends; validate audit log entry created on publish; validate publishing blocked when validation errors exist
- E2E scenario: E2E-01-01 (publish step)
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.11 — Publish a survey.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.11-publish-survey.md.
>  Key constraints: (1) Status transition: draft → scheduled (future send) or draft → live (immediate send); (2) Pre-publish validation runs server-side, not just client-side; (3) Audit log the publish event using the existing helper service — never inline; (4) A grace period for 'immediate' delivery should be defined (check M5.5 spec for guidance — default: send time within the last 5 minutes counts as immediate).
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
