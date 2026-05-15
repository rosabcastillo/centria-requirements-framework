## Story 0.2 — Add Surveys nav entry in CareConnect (role-gated)

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** careconnect-admin
**Epic:** epic-00-foundation

### As a VP-level survey administrator
### I want to see a Surveys entry in the CareConnect navigation
### So that I can access the survey builder from the main application without knowing the direct URL

### Acceptance criteria
- Given I am logged in as a VP-level admin or Super Admin, when I view the main CareConnect navigation, then a "Surveys" entry is visible
- Given I am logged in as a DCS or OD user, when I view the main CareConnect navigation, then "Surveys" is not visible
- Given a DCS or OD user knows the /surveys URL and navigates to it directly, when the page loads, then they receive a 403 Forbidden response — not just a hidden nav entry
- Given I am a VP-level admin and I click "Surveys," when the page loads, then I see a placeholder page ("Coming soon" or similar)

### Test plan
- Unit: Validate role-check middleware returns 403 for DCS/OD on the /surveys route; validate nav config shows entry only for VP+ and Super Admin roles
- E2E scenario: E2E-01-01 (first step — nav visibility check)
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-00-foundation/README.md. Also read /docs/architecture/auth-roles.md before touching any auth code.
>  Implement story 0.2 — Add Surveys nav entry in CareConnect.
>  Story spec: themes/survey-builder/epics/epic-00-foundation/stories/story-0.2-surveys-nav-entry.md.
>  Key constraints: (1) DCS and OD must be blocked at the URL level — hidden nav is not enough. Route middleware must return 403; (2) Use the existing CareConnect role middleware — do not create new role types; (3) The nav entry points to a placeholder page for now — the full feature is built in epic-01 and beyond.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
