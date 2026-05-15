## Story 0.3 — Survey Administrator role provisioning check

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** careconnect-admin, survey-service
**Epic:** epic-00-foundation

### As a developer
### I want the existing CareConnect role and permission system documented and confirmed working for the /surveys route
### So that all future survey stories can rely on a tested, documented auth foundation

### Acceptance criteria
- Given the existing CareConnect role system, when I look at /docs/architecture/auth-roles.md, then it describes which roles map to survey administrator access (VP-level = access, DCS/OD = no access, Super Admin = elevated access)
- Given the documentation is written, when I run the role-check middleware against the /surveys route in tests, then VP+ roles pass and DCS/OD roles return 403
- Given a Super Admin user, when they access /surveys, then they have access with elevated privileges (gating controls visible in future stories)

### Test plan
- Unit: Validate role middleware returns correct access decisions for all four role categories against the /surveys route
- E2E scenario: none yet (smoke checklist item #1 and #2 cover this in deployment)
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-00-foundation/README.md.
>  Implement story 0.3 — Role provisioning check.
>  Story spec: themes/survey-builder/epics/epic-00-foundation/stories/story-0.3-role-provisioning-check.md.
>  Key constraints: (1) Do not create new roles — inspect and document existing CareConnect roles only; (2) Write the auth-roles.md documentation file at /docs/architecture/auth-roles.md; (3) Confirm that the middleware wired in story 0.2 correctly enforces the roles documented; (4) Super Admin = IT-granted elevated role, distinct from VP-level admin.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
