## Story 3.8 — Event-triggered instance is created per qualifying event

**Status:** 🚫 Blocked
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

**BLOCKED:** Waiting on event-trigger architecture decision. Stakeholders: Kerri + Timothy + Emily (business decision); Son + Harish (architecture proposal). Do NOT start until this decision is resolved and this story is explicitly unblocked. See decisions.md open decision #5.

### As a survey administrator
### I want each qualifying clinical event to generate a new survey send
### So that outcome data is captured consistently for every relevant session

### Acceptance criteria
- Given a 97156 session note is completed for a family in the survey's audience, when the event fires, then the family receives the survey
- Given the same family has an open instance from a previous event, when a new event fires, then a new instance is created (the system does not suppress the send due to an existing open instance — unless a business rule is explicitly configured)
- Given the event fires for a family not in the survey audience, when the system processes it, then no survey is sent to that family

### Test plan
- Unit: Validate event handler creates a new SurveyAssignment for the qualifying family; validate that an existing open instance does not suppress a new send unless a business rule is configured; validate that out-of-audience families are filtered out
- E2E scenario: none yet (to be defined when unblocked)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  DO NOT START — story 3.8 is 🚫 Blocked. The event-trigger architecture has not been decided.
>  When unblocked: implement story 3.8 — Event-triggered instance creation.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.8-event-triggered-instance.md.
>  Key constraints: (1) Each qualifying 97156 event creates a new instance — no suppression by default; (2) Audience check must be applied before sending; (3) Architecture must be extensible for future event types."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
