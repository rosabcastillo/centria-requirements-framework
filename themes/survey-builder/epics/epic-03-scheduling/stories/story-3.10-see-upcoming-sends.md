## Story 3.10 — See upcoming scheduled sends

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to see the next planned send dates for a recurring survey
### So that I can anticipate when instances will go out and plan accordingly

### Acceptance criteria
- Given a recurring survey, when I open its schedule settings, then I see the next 5 planned send dates listed
- Given the schedule has an end date, when all remaining sends are within view, then I see all remaining dates (not limited to 5)
- Given I change the recurrence pattern, when I save, then the upcoming dates list updates immediately

### Test plan
- Unit: Validate next-5-dates calculation from RRULE is correct; validate that when fewer than 5 remain before end date, all remaining are shown; validate that pattern changes trigger recalculation of upcoming dates
- E2E scenario: E2E-03-01 (preview step)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.10 — See upcoming sends.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.10-see-upcoming-sends.md.
>  Key constraints: (1) Default: show next 5 dates; if fewer than 5 remain before end date, show all remaining; (2) Dates are computed from the RRULE and start date; (3) When admin changes the pattern, the preview must update without requiring a page reload; (4) Do not use a date/time library without checking /docs/architecture/ for the approved library.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
