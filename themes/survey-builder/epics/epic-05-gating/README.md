# Epic 05 — Survey Gating

**Status:** ⬜ Ready
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin, flutter-family-app
**Target:** Weeks 12–13

## Goal
Super Admins can require parents to complete a survey before accessing certain app content.

## Definition of Done
- [ ] Gating toggle available on any survey (Super Admin only — VP cannot see this control)
- [ ] Gating delay configured as "days after sending" (default 0 = immediate)
- [ ] Blur overlay appears in Flutter app when gating-active survey is pending
- [ ] Calendar, messages, settings remain accessible during gate
- [ ] Gate lifts immediately on survey submission
- [ ] Full-screen takeover is NOT used

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-5.1-gating-configuration | Gating flag configuration (Super Admin only) | ⬜ Ready |
| story-5.2-gating-delay-model | Gating delay model (days after sending) | ⬜ Ready |
| story-5.3-blur-overlay | Blur overlay UX (Flutter) | ⬜ Ready |
| story-5.4-gate-lift-on-completion | Gate lift on completion | ⬜ Ready |

## Key constraints
- Super Admin only — VP-level admins cannot see or manage gating controls
- Any survey can be gated — no pre-approved list
- Blur overlay (NOT full-screen takeover) — calendar, messages, settings remain accessible
- Default gating delay = 0 (immediate gate as soon as survey is sent)
- Flutter-level implementation — coordinate with Flutter dev
