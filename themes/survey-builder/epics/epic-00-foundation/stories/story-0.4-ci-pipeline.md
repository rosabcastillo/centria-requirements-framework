## Story 0.4 — CI pipeline with lint, type check, build, tests

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-00-foundation

### As a developer
### I want a CI pipeline that runs on every push and blocks PR merges if it fails
### So that the team maintains a green build and regressions are caught before merging

### Acceptance criteria
- Given a push to any branch, when the CI pipeline runs, then it executes lint, type check, build, and tests in sequence
- Given any step in the pipeline fails, when a PR is open for that branch, then the PR merge is blocked
- Given all steps pass, when I look at the PR, then a green check mark is shown and the PR is mergeable

### Test plan
- Unit: N/A — CI configuration story
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: no

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-00-foundation/README.md.
>  Implement story 0.4 — CI pipeline.
>  Story spec: themes/survey-builder/epics/epic-00-foundation/stories/story-0.4-ci-pipeline.md.
>  Key constraints: (1) CI must run: ESLint (frontend), dotnet build (backend), dotnet test (backend), TypeScript type check (frontend); (2) GitHub Actions is the assumed CI platform — check the existing repo config; (3) PR merge protection must require all CI checks to pass; (4) Pipeline must complete in under 10 minutes for a standard build.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
