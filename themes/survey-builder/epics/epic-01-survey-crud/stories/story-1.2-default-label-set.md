## Story 1.2 — Default label set pre-loaded

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want a standard agree-disagree Likert scale available from day one
### So that I don't have to create the most common scale from scratch

### Acceptance criteria
- Given the system is set up for the first time, when I open the Likert label set library, then "Strongly Disagree / Disagree / Neutral / Agree / Strongly Agree" is already available
- Given this default label set, when I try to delete it, then I am told the default set cannot be deleted
- Given the default set, when I use it in a question, then it behaves identically to any other label set (including the ability to override labels at the question level)

### Test plan
- Unit: Validate that the default seed exists after migration; validate delete of default set is blocked; validate that the default set can be applied to a question
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.2 — Default label set pre-loaded.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.2-default-label-set.md.
>  Key constraints: (1) Seed the default 'Strongly Disagree / Disagree / Neutral / Agree / Strongly Agree' set as part of the database migration or seeder; (2) The default set must be undeletable — flag it in the schema (e.g., is_default = true); (3) It must still be usable and overridable at the question level like any other set.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
