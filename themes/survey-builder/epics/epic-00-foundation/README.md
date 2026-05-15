# Epic 00 — Foundation & Scaffolding

**Status:** 🔵 In Progress
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin
**Target:** Week 1

## Goal
Working dev environment, CI baseline, auth wired, empty Surveys section visible in CareConnect to VP+ users only.

## Definition of Done
- [ ] Repo structure matches framework spec
- [ ] Surveys nav entry visible to VP+ only; DCS/OD blocked at URL level (403)
- [ ] Auth roles documented in /docs/architecture/auth-roles.md
- [ ] CI pipeline runs lint, type check, build, tests on every push
- [ ] Playwright E2E framework installed with first two passing tests

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-0.1-repo-and-folder-structure | Set up project workspace and repo structure | ✅ Done |
| story-0.2-surveys-nav-entry | Add Surveys nav entry in CareConnect (role-gated) | ⬜ Ready |
| story-0.3-role-provisioning-check | Survey Administrator role provisioning check | ⬜ Ready |
| story-0.4-ci-pipeline | CI pipeline with lint, type check, build, tests | ⬜ Ready |
| story-0.5-e2e-framework | E2E testing framework with first passing test | ⬜ Ready |

## Key constraints
- DCS and OD must be blocked at the URL level — not just hidden in nav
- Role middleware must use the existing CareConnect role system — no new roles
