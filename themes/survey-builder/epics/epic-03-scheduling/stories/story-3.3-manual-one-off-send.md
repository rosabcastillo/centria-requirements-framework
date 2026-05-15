## Story 3.3 — Send a manual one-off survey outside the schedule

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to send a survey to a specific audience manually, independent of any scheduled cadence
### So that I can handle ad-hoc situations or recover from a scheduling failure

### Acceptance criteria
- Given a published survey, when I click "Send Now," then a confirmation asks me to confirm the audience and send
- Given I confirm a manual send, when the dispatch is complete, then a new survey instance is created and the audience receives it
- Given a manual send, when I view the survey history, then this instance is labeled "Manual send" alongside its send date and completion statistics

### Test plan
- Unit: Validate that manual send creates a new SurveyInstance with type = manual; validate the confirmation dialog shows correct audience; validate audit log entry for manual send
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.3 — Manual one-off send.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.3-manual-one-off-send.md.
>  Key constraints: (1) Manual send creates a new SurveyInstance with type = 'manual' — distinct from scheduled and event-triggered instances; (2) This instance appears in survey history labeled 'Manual send'; (3) Audience for a manual send uses the survey's configured market; (4) Audit log the manual send event using the existing helper service.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
