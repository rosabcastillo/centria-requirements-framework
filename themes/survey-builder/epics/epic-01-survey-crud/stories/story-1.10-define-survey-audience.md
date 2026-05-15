## Story 1.10 — Define the survey audience

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to target a survey to a specific market
### So that it only reaches the families in the relevant locations

### Acceptance criteria
- Given a survey, when I open the audience settings, then I can select one or more markets
- Given I select a market, when the survey is sent, then only families associated with that market receive it
- Given I want to send to multiple markets, when I create separate survey instances per market, then each instance targets its own market correctly (no batch targeting UI — handled by duplication)
- Given no market is selected, when I try to publish, then validation blocks publishing with a message that audience is required

### Test plan
- Unit: Validate that publishing with no market selected fails validation; validate that market_id is stored on the survey; validate that audience filtering is applied when creating SurveyAssignments
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.10 — Define the survey audience.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.10-define-survey-audience.md.
>  Key constraints: (1) Market is required before publishing — validation must block; (2) No batch targeting UI — multi-market is handled by duplicating survey instances, not by multi-select here; (3) Market ID is stored on the surveys table (market_id field from M1.1 data model); (4) The actual audience filtering (which families receive the survey) happens in the scheduler, not here.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
