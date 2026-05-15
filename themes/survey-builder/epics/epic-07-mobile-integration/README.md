# Epic 07 — Mobile App Integration (Flutter)

**Status:** ⬜ Ready
**Owner:** Separate Flutter developer
**Repos:** flutter-family-app
**Target:** After API contract from epics 01–06 is stable

## Goal
Parents can receive, complete, and review surveys inside the Family Connect app.

## Definition of Done
- [ ] API contract reviewed with Flutter dev (story 8.4 in milestone plan)
- [ ] One question per screen, auto-advance on answer selection
- [ ] Branching invisible to parents — only next relevant question shown
- [ ] Blur overlay for gating
- [ ] Closed surveys show "closed" state, not answerable
- [ ] Survey history: pagination or accordion (no unbounded scroll)
- [ ] Multi-language: English, Spanish, Arabic (Arabic = RTL)

## Dependencies
- All API contracts from epics 01–06 must be stable and documented in OpenAPI spec
- Gating blur overlay design from Epic 05 must be finalized
- Open decision #6 (survey history UI pattern — pagination vs. accordion) must be resolved before Flutter dev starts

## Key constraints
- Auto-advance: selecting an answer advances — NO Proceed button
- Gating UI: blur overlay, NOT full-screen takeover
- Arabic: RTL layout required — Flutter-level concern, not just translation
- Survey history: pagination or accordion — NO unbounded scroll
- Open decision #6 (history pattern) is Rosa's decision
