## Story 1.1 — Manage the Likert label set library

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to create, update, and manage a library of reusable Likert label sets
### So that I can quickly apply consistent scales across multiple surveys without retyping them

### Acceptance criteria

*Creating a label set:*
- Given I am a survey administrator, when I navigate to the Likert label set library, then I see a list of all existing label sets and a button to create a new one
- Given I click "Create label set," when I enter a name and five point labels, then the new set appears in the library
- Given I try to save a label set with fewer than five labels defined, when I click Save, then an error message tells me all five labels are required

*Editing a label set:*
- Given an existing label set, when I edit its name or any label and save, then the updated version replaces the old one in the library
- Given a label set is already in use on a published survey, when I edit that label set, then the change is reflected on future surveys using it but does NOT retroactively change historical responses

*Deleting a label set:*
- Given a label set not used by any survey, when I delete it, then it is removed from the library
- Given a label set used by at least one survey, when I try to delete it, then I am told it cannot be deleted while in use

### Test plan
- Unit: Validate label set creation requires exactly 5 labels; validate delete is blocked when label set has associated surveys; validate edit does not retroactively modify responses
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.1 — Manage the Likert label set library.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.1-manage-likert-label-library.md.
>  Key constraints: (1) This is Survey Builder Likert — different from Feature 1 data collection Likert which uses fixed templates; (2) Audit log all mutations using the existing helper service — never inline; (3) Editing an in-use label set must NOT retroactively change historical response data.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
