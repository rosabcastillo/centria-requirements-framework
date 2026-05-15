## Story 1.17 — See all surveys in a list

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to see all surveys I have access to in a filterable list
### So that I can quickly find and manage any survey

### Acceptance criteria
- Given I am a survey administrator, when I navigate to the Surveys section, then I see a list of all surveys I created, plus all surveys by other admins (read-only for others)
- Given the survey list, when I filter by status (Draft / Scheduled / Live / Closed), then only matching surveys appear
- Given the survey list, when I search by survey name, then matching surveys appear
- Given the survey list, when I filter by creator, then only that creator's surveys appear
- Given the survey list is empty, when I load it, then an empty state is shown with a "Create your first survey" prompt
- Given the list has surveys, when I look at each row, then I see: name, status badge, type, last sent date, completion percentage

**Status badge colors:**
- Live: teal
- Scheduled: amber
- Draft: gray
- Closed: gray (muted)

### Test plan
- Unit: Validate GET /surveys returns correct filters for status, creator, and name search; validate response includes name, status, type, last_sent, completion_pct fields; validate performance under load (500 surveys, under 2s)
- E2E scenario: E2E-01-01 (list view step), E2E-01-02 (cross-creator visibility)
- Smoke impact: yes
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.17 — See all surveys in a list.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.17-see-all-surveys.md.
>  Key constraints: (1) Status badge colors: teal = Live, amber = Scheduled, gray = Draft, gray muted = Closed; (2) Cross-creator restriction: edit controls must be disabled for surveys not created by the logged-in user; (3) Performance requirement: list must load in under 2 seconds for up to 500 surveys — use pagination or query optimization; (4) Filters are cumulative (status AND creator AND name search together).
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
