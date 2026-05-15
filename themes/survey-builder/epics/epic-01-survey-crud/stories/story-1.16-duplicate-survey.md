## Story 1.16 — Duplicate a survey

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to duplicate a closed or existing survey
### So that I can create a new version or reuse the same structure for a different audience or time period

### Acceptance criteria
- Given any survey (in any status), when I click "Duplicate," then a new draft is created with the same title (prefixed "Copy of"), same questions, same sections, and same schedule structure — but with no audience, no send date, and status = Draft
- Given I duplicate a survey, when I view the duplicate, then the original's responses are not included
- Given a closed survey, when duplication is the primary recovery path shown, then the "Duplicate" button is prominently visible

### Test plan
- Unit: Validate that duplicate creates a new draft with correct title prefix; validate that the duplicate has no audience, no send date, status = draft; validate that original responses are not copied; validate that duplicate is available from all survey statuses
- E2E scenario: E2E-01-03
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.16 — Duplicate a survey.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.16-duplicate-survey.md.
>  Key constraints: (1) Duplicate must copy questions, sections, and schedule structure — but clear audience (market_id = null) and send date; (2) Title prefix is 'Copy of [original title]'; (3) Status of duplicate is always draft regardless of original status; (4) Responses are NOT copied — only the survey structure; (5) Audit log the duplication event.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
