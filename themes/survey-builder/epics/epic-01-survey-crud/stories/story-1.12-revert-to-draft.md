## Story 1.12 — Move a scheduled survey back to draft

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to revert a scheduled survey back to draft if I need to make changes before it sends
### So that I don't have to delete and recreate it

### Acceptance criteria
- Given a scheduled survey whose send time has not yet passed, when I click "Revert to Draft," then the status changes to Draft and I can edit it again
- Given a live survey, when I look for a "Revert to Draft" option, then it is not available (live surveys cannot be reverted — only closed)
- Given I revert a scheduled survey, when I view the audit trail, then a "Reverted to Draft" entry appears

### Test plan
- Unit: Validate scheduled → draft transition succeeds when send time is in future; validate that live surveys return 409 on revert attempt; validate audit log entry on revert
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.12 — Revert to draft.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.12-revert-to-draft.md.
>  Key constraints: (1) Revert is only valid from 'scheduled' status where send time has not yet passed — return 409 for live surveys; (2) Hide the Revert to Draft button entirely for live surveys — do not just disable it; (3) Audit log the revert event using the existing helper service.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
