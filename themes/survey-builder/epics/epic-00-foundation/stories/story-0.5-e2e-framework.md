## Story 0.5 — E2E testing framework with first passing test

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-00-foundation

### As a developer
### I want Playwright installed and configured with two passing baseline tests
### So that the QA team has a working E2E framework to build on from day one

### Acceptance criteria
- Given Playwright is installed and configured, when I run the test suite, then the first test passes: navigate to /surveys as a VP-level user and confirm the Surveys nav entry is visible
- Given Playwright is installed and configured, when I run the test suite, then the second test passes: navigate to /surveys as a DCS user and confirm a 403 response is received
- Given the E2E suite runs in CI, when the pipeline executes, then E2E tests run as part of the full suite

### Test plan
- Unit: N/A — framework setup story
- E2E scenario: these two tests ARE the first E2E scenarios (pre-E2E-01-01 baseline)
- Smoke impact: yes (these tests validate the core auth gate)
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-00-foundation/README.md.
>  Implement story 0.5 — E2E testing framework.
>  Story spec: themes/survey-builder/epics/epic-00-foundation/stories/story-0.5-e2e-framework.md.
>  Key constraints: (1) Use Playwright as the E2E framework; (2) First test: log in as VP-level user, navigate to /surveys, assert nav entry is visible; (3) Second test: log in as DCS user, navigate to /surveys, assert 403 is returned; (4) Both tests must run in CI as part of the GitHub Actions pipeline (story 0.4 must be done first); (5) Test credentials must come from environment variables — never hardcoded.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
