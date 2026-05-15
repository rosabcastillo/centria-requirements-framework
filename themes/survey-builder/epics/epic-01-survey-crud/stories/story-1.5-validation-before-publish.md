## Story 1.5 — See what's missing before I can publish

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to see a clear validation summary of everything that needs to be fixed before I can publish
### So that I don't discover problems at the last minute

### Acceptance criteria
- Given a draft with missing required fields, when I click "Publish," then a validation panel shows a list of specific issues (e.g., "No questions added," "No schedule set," "Section has no questions")
- Given all validation issues are resolved, when I click "Publish," then publishing proceeds without showing the validation panel
- Given the validation panel is showing, when I click a listed issue, then I am taken directly to the area that needs fixing

### Test plan
- Unit: Validate each individual error condition (no questions, no schedule, empty section, no audience); validate that clicking a listed issue navigates to the correct builder section; validate that a fully valid survey passes all checks
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.5 — Validation before publish.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.5-validation-before-publish.md.
>  Key constraints: (1) Validation panel must list specific named issues, not generic 'Form invalid' messages; (2) Each listed issue must be clickable and link directly to the problem area in the builder; (3) Publishing is blocked until all issues are resolved — validation runs server-side as well as client-side.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
