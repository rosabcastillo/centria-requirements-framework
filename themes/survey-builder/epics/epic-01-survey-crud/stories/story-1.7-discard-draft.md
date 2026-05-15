## Story 1.7 — Discard a draft

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to permanently delete a draft survey I no longer need
### So that the survey list doesn't accumulate abandoned drafts

### Acceptance criteria
- Given a draft survey, when I click "Delete" and confirm, then the survey is permanently removed
- Given a scheduled or live survey, when I try to delete it, then deletion is blocked and I am told only drafts can be deleted (I must close a live survey first, then delete)
- Given I click "Delete," when I see the confirmation dialog, then it clearly states this action is permanent and cannot be undone

### Test plan
- Unit: Validate DELETE /surveys/:id returns 409 if status is not draft; validate that a confirmed delete removes the survey from GET /surveys; validate confirmation dialog text
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.7 — Discard a draft.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.7-discard-draft.md.
>  Key constraints: (1) DELETE endpoint must return 409 with a clear message if survey is not in draft status; (2) Confirmation dialog must explicitly state the action is permanent and irreversible; (3) Audit log the delete event using the existing helper service.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
