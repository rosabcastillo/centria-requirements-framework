## Story 1.6 — Save my work explicitly

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to be able to save my work at any time with an explicit "Save" action
### So that I know my progress is preserved, in addition to auto-save

### Acceptance criteria
- Given I am in the survey builder, when I click "Save," then a confirmation appears that my changes have been saved
- Given I make changes and then navigate away without saving, when I return, then my changes are still present (auto-save is also active)
- Given I make changes and my browser crashes, when I return to the survey, then my last auto-saved state is restored

### Test plan
- Unit: Validate that explicit save triggers a PUT request and returns success; validate that auto-save fires after a debounce interval on field changes; validate that returning to the survey after navigation shows the last saved state
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.6 — Save my work explicitly.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.6-save-work-explicitly.md.
>  Key constraints: (1) Both explicit save (button) and auto-save on change must be active simultaneously; (2) Auto-save should debounce — do not fire on every keystroke; (3) Show a visual save confirmation (toast or indicator) on both explicit save and auto-save; (4) Saved state must survive navigation away and browser refresh.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
