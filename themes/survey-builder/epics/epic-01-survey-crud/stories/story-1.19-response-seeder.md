## Story 1.19 — Simulate parent responses for testing

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a developer or QA tester
### I want to seed test responses for a survey
### So that I can verify reporting and completion logic without involving real families

### Acceptance criteria
- Given a test environment, when I use the seeding tool to generate N responses for a survey, then the system records those responses as if real parents submitted them
- Given seeded responses, when I view survey results, then they appear in the aggregation and reporting views
- Given I seed responses for a branching survey, when I review the results, then skipped questions are recorded as `was_skipped = true` and appear correctly in reporting

### Test plan
- Unit: Validate seeder creates correct number of SurveyResponse records; validate was_skipped = true is set correctly for branching paths; validate seeded responses appear in aggregation queries
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: no

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.19 — Response seeder.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.19-response-seeder.md.
>  Key constraints: (1) Seeder must only run in test environments — add a guard; (2) Seeded responses must be structurally identical to real responses (same table, same schema); (3) For branching surveys, seeder must correctly simulate a path and set was_skipped = true on skipped questions; (4) Seeder must be idempotent — safe to re-run without duplicating data; (5) Entrypoint: dotnet run --project src/Centria.Survey.DbUp -- '<conn>' 'Test'.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
