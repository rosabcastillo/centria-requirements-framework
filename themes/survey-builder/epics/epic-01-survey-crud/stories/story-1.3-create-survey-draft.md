## Story 1.3 — Create a new survey draft

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to create a new blank survey draft with a title
### So that I have a starting point I can build on over time

### Acceptance criteria
- Given I am logged in as a survey administrator, when I click "Create Survey," then a blank draft is created and I am taken to the survey builder
- Given a new draft, when I look at its status, then it shows "Draft"
- Given a new draft, when I have not added any title, then a placeholder title ("Untitled Survey") is shown and I am prompted to add one
- Given I enter a title and navigate away, when I return to the survey, then my title has been saved automatically
- Given I am a VP-level user who did not create this draft, when I find it in the survey list, then I can view it but the edit controls are disabled

### Test plan
- Unit: Validate that POST /surveys creates a draft with status = "draft" and created_by = current user; validate that non-creator VP user gets read-only response from GET /surveys/:id
- E2E scenario: E2E-01-01 (partial — creation step), E2E-01-02
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.3 — Create a new survey draft.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.3-create-survey-draft.md.
>  Key constraints: (1) Status must be enforced as a DB-level enum (draft/scheduled/live/closed); (2) cross-creator restriction: edit controls are disabled for any VP-level user who is not the survey creator — check both role and creator identity; (3) auto-save title on change, not just on explicit save; (4) audit log the creation event using the existing helper service.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
