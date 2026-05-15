## Story 3.1 — Configure a recurring schedule using calendar-style patterns

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to set a recurring schedule using familiar calendar-style recurrence options
### So that I can configure the survey to send on a consistent cadence without manual intervention each time

### Acceptance criteria
- Given I am configuring a survey, when I select "Recurring" as the send type, then I see pattern options consistent with Google Calendar–style recurrence: daily, weekly (on specific days), monthly (on a date or day of week), and a custom interval option
- Given I select a weekly pattern on Mondays, when the schedule is saved, then the survey will be sent every Monday
- Given I select a custom interval of 14 days, when the schedule is saved, then the survey will be sent every 14 days from the configured start date
- Given I select a recurring pattern, when I preview the schedule, then I see the next 5 planned send dates

### Test plan
- Unit: Validate RRULE generation for each pattern type (daily, weekly by day, monthly by date, monthly by day-of-week, custom interval); validate next-5-dates preview calculation is correct for each pattern
- E2E scenario: E2E-03-01 (schedule configuration step)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.1 — Configure a recurring schedule.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.1-configure-recurring-schedule.md.
>  Key constraints: (1) Use RRULE standard for recurrence patterns (RFC 5545) — Google Calendar–style patterns map to RRULE; (2) The 'next 5 dates' preview must be computed correctly from the RRULE; (3) Custom interval fallback is for non-standard patterns the RRULE builder cannot express; (4) Do not start M5.4 event-trigger stories — those are blocked separately; (5) Do not use a date/time library without checking /docs/architecture/ for the approved library.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
