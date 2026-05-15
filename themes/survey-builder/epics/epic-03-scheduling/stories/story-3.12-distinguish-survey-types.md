## Story 3.12 — Distinguish survey types in the list view

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to see at a glance whether a survey is one-time, recurring, or event-triggered
### So that I can manage them without opening each one

### Acceptance criteria
- Given the survey list, when I look at any row, then the survey type (One-time / Recurring / Event-triggered) is visible as a label or icon
- Given a recurring survey currently in an active instance, when I look at its row, then I see both the type and the current instance's status

### Test plan
- Unit: Validate that GET /surveys returns a type field (one-time / recurring / event-triggered) for each survey; validate that recurring surveys include current instance status in the list response
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.12 — Distinguish survey types in list view.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.12-distinguish-survey-types.md.
>  Key constraints: (1) Survey type is derived from the schedule JSON — one-time, recurring (RRULE present), or event-triggered; (2) The list API must return this type field; (3) For recurring surveys, the list row shows type AND current instance status (as covered in story 1.18); (4) Event-triggered surveys will only exist after stories 3.7–3.9 are unblocked — this story should gracefully handle the absence of event-triggered surveys.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
