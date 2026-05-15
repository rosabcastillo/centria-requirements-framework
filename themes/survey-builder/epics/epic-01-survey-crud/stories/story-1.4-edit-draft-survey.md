## Story 1.4 — Edit a draft survey

**Status:** ⬜ Ready
**Jira:** SURV-TBD
**Repo(s):** survey-service, careconnect-admin
**Epic:** epic-01-survey-crud

### As a survey administrator
### I want to freely edit all aspects of a survey while it is in Draft status
### So that I can refine it before publishing

### Acceptance criteria
- Given a draft survey, when I edit the title, description, or any question, then my changes are preserved
- Given a scheduled survey whose send time has not yet arrived, when I edit it, then my changes are preserved (same freedom as Draft)
- Given a live survey, when I try to edit any field, then all editing is disabled with a message that live surveys cannot be edited
- Given a closed survey, when I try to edit any field, then all editing is disabled — I am offered the option to duplicate instead

### Test plan
- Unit: Validate that PUT /surveys/:id returns 409 when survey is closed; validate that live surveys return edit-disabled state; validate that scheduled (not yet sent) surveys are fully editable
- E2E scenario: none yet
- Smoke impact: no
- Regression impact: yes

### Claude Code briefing
> "Read CLAUDE.md and themes/survey-builder/epics/epic-01-survey-crud/README.md.
>  Implement story 1.4 — Edit a draft survey.
>  Story spec: themes/survey-builder/epics/epic-01-survey-crud/stories/story-1.4-edit-draft-survey.md.
>  Key constraints: (1) Scheduled surveys (send time not yet arrived) are editable — same as draft; (2) Live and closed surveys return editing disabled; (3) Closed surveys should show a 'Duplicate' prompt as the recovery path; (4) All edits must go through the existing audit log helper service.
>  All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
