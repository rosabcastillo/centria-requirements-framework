## Story 3.13 — Preview the schedule before publishing

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to preview what the schedule will look like before I commit to publishing
### So that I can catch any misconfiguration before it affects families

### Acceptance criteria
- Given I have configured a recurring schedule, when I click "Preview schedule," then I see the next 5 instance dates in a simple list view
- Given I review the preview and spot an error, when I go back and fix the schedule, then the preview updates to reflect the corrected dates
- Given a one-time send, when I view the schedule summary, then I see the single send date and time clearly stated

### Test plan
- Unit: Validate preview endpoint returns next 5 dates for a given RRULE; validate that correcting a schedule recalculates the preview correctly; validate that one-time schedule preview shows the single send date
- E2E scenario: E2E-03-01 (preview step)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.13 — Preview the schedule before publishing.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.13-preview-schedule.md.
>  Key constraints: (1) Preview is a read-only computation from the RRULE and start date — no state change; (2) Preview must update immediately when the schedule is edited without requiring a publish attempt; (3) One-time schedules show a simple single-date summary; (4) Preview is accessible from the schedule configuration section before clicking Publish.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
