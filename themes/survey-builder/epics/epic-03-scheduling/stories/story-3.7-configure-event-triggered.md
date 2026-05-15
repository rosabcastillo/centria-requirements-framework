## Story 3.7 — Configure a survey to trigger on a clinical event

**Status:** 🚫 Blocked
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-03-scheduling

**BLOCKED:** Waiting on event-trigger architecture decision. Stakeholders: Kerri + Timothy + Emily (business decision); Son + Harish (architecture proposal). Do NOT start until this decision is resolved and this story is explicitly unblocked. See decisions.md open decision #5.

### As a survey administrator
### I want to configure a survey to send automatically when a specific clinical event occurs
### So that I can capture timely feedback without manual scheduling

### Acceptance criteria
- Given I am configuring a survey, when I select "Event-triggered" as the send type, then I see a dropdown of available clinical events
- Given the available events at MVP include only "Post-97156 session completion," when I select it, then the survey will be sent each time a 97156 session note is completed for a family in the target audience
- Given I configure an event-triggered survey, when I preview what will happen, then I see a description: "This survey will be sent to [audience] each time a 97156 session note is completed"

### Test plan
- Unit: Validate event-triggered send type configuration is stored correctly; validate the event dropdown shows only post-97156 at MVP; validate the preview description renders correctly
- E2E scenario: none yet (to be defined when unblocked)
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-03-scheduling/README.md.
>  DO NOT START — story 3.7 is 🚫 Blocked. The event-trigger architecture has not been decided.
>  When unblocked: implement story 3.7 — Configure event-triggered survey.
>  Story spec: themes/survey-builder/epics/epic-03-scheduling/stories/story-3.7-configure-event-triggered.md.
>  Key constraints: (1) MVP scope: post-97156 only; (2) Architecture must accommodate future triggers (intake, auth expiration) without rework; (3) Wait for architecture decision from Son + Harish before touching this story."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
