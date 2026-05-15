# Repos — Survey Builder

All repositories this theme touches. Derived from story declarations.

| Repo | Team | Stories |
|------|------|---------|
| survey-service (Centria.Survey.Api) | Dev | 0.1–0.5, 1.1–1.19, 2.1–2.14, 3.1–3.12, 4.1–4.8, 5.1–5.6, 6.1–6.4 |
| careconnect-admin (CareConnect.Backend.Admin) | Dev | 0.2–0.3, 1.3–1.19, 2.2–2.14, 3.1–3.12, 4.1–4.2, 5.1–5.2, 6.1–6.4 |
| notification-service | Dev | 4.3–4.7 |
| flutter-family-app | Flutter Dev | 5.3–5.4, 7.x |

## Blast radius summary
- **survey-service:** All epics — the core backend
- **careconnect-admin:** All UI-facing epics — the admin interface
- **notification-service:** Epic 04 (reminders) only
- **flutter-family-app:** Epic 05 partial (blur overlay), Epic 07 (full respondent experience)

## API contract dependency
Flutter dev cannot start until the OpenAPI spec from epics 01–06 is stable and reviewed (story 8.4 in the milestone plan).
