## Story 3.5 — View instance history for a recurring survey

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

### As a survey administrator
### I want to see all past instances of a recurring survey with their statistics
### So that I can track trends and completion rates over time

### Acceptance criteria
- Given a recurring survey with 3 completed instances, when I open the survey detail, then I see a list of all instances with their send date, close date, and completion percentage
- Given the instance list, when I click on a past instance, then I can view the responses and aggregated results for that instance

### Test plan
- Unit: Validate GET /surveys/:id/instances returns correct instance records with send_date, close_date, completion_pct; validate that clicking into an instance returns the responses for that instance only
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  Implement story 3.5 — View instance history.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.5-view-instance-history.md.
>  Key constraints: (1) Instance history is available on the survey detail screen; (2) Each row shows: send date, close date, completion % (completed / total assigned); (3) Clicking an instance navigates to a per-instance results view (reporting stories in Epic 06 build the full results UI — this story adds the navigation shell); (4) No unbounded scroll — paginate if more than 20 instances.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
