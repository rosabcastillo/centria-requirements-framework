## Story 3.9 — View event-triggered instances in survey history

**Status:** 🚫 Blocked
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

**BLOCKED:** Waiting on event-trigger architecture decision. Stakeholders: Kerri + Timothy + Emily (business decision); Son + Harish (architecture proposal). Do NOT start until this decision is resolved and this story is explicitly unblocked. See decisions.md open decision #5.

### As a survey administrator
### I want to see all instances triggered by clinical events
### So that I can audit which events resulted in survey sends

### Acceptance criteria
- Given an event-triggered survey with multiple instances, when I view the survey history, then I see each instance labeled with the event type and timestamp that triggered it
- Given I click on an instance, when I view its detail, then I can see the completion statistics for that send

### Test plan
- Unit: Validate instance history endpoint returns event_type and triggered_at fields for event-triggered instances; validate completion statistics are correct per instance
- E2E scenario: none yet (to be defined when unblocked)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  DO NOT START — story 3.9 is 🚫 Blocked. The event-trigger architecture has not been decided.
>  When unblocked: implement story 3.9 — View event-triggered instance history.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.9-view-event-triggered-history.md.
>  Key constraints: (1) History entries must include the triggering event type and timestamp; (2) Completion statistics must match actual responses for that specific instance."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
