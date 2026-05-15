# Survey Builder — Product Requirements Document v1.1

**Status:** Draft — Updated with May 6, 2026 SME Session Outcomes
**Last Updated:** May 2026
**Author:** Kerri Milyko
**Product Manager:** Emily Rueber
**Engineering Lead:** TBD
**Designer:** Rosa Batista
**Approvers:** Timothy Yeager, Kerri Milyko
**Part of:** Family Connect App Phase 2 initiative

---

## 1. Overview

The Survey Builder is a self-service tool inside CareConnect that enables survey administrators to create, schedule, and distribute surveys to families. It captures structured parent-reported outcome data to support measurement-based care, payer reporting, and organizational accountability.

This is Feature 3 of Family Connect App Phase 2. Features 1 (Parent Data Collection) and 2 (Monthly Progress Summary) are separate workstreams.

---

## 2. Problem Statement

Parent-reported outcome data is the #1 gap when meeting with payers. There is currently no systematic way to trend parent satisfaction or engagement. Survey infrastructure must support payer-facing outcome reporting requirements. Every survey send today requires manual intervention — there is no automated or recurring mechanism.

---

## 3. Goals

1. Enable administrators to build and publish surveys without engineering support
2. Automate recurring and event-triggered survey delivery
3. Capture structured parent-reported outcome data at scale
4. Surface results inside CareConnect for clinical and operational review

---

## 4. Users and Roles

### Survey Administrator
VP-level (clinical or ops) and Super Admin (IT-granted). Can create, edit, publish, schedule, and close surveys. Can view results.

**Not included:** DCS and OD roles have no access to the Survey Builder or its results — not even read-only.

### Super Admin
IT-granted elevated role. Same as Survey Administrator plus the ability to activate and manage survey gating (blocking app content until a survey is completed).

### Parent / Respondent
Receives surveys via push notification, completes them inside the Family Connect app. Does not interact with CareConnect directly.

### Clinical Staff (SC / BT)
Not direct users of the Survey Builder. Their clinical actions (e.g., completing a 97156 session note) can trigger event-based survey sends.

---

## 5. Feature Scope — IN

### 5.1 Survey Creation
- Create a draft survey with a title, description, and optional confirmation message
- Add questions in six types: Likert, Star Rating, Multiple Choice, Yes/No, Short Answer, Ranking
- Organize questions into sections (every question must belong to a section; a default section is auto-created)
- Reorder questions and sections via drag-and-drop
- Configure branching logic at the section level (Google Forms parity — skip to section based on answer; no question-level branching)
- Preview the survey in a mobile frame before publishing

### 5.2 Question Type Details
- **Likert:** 5-point scale with admin-customizable labels per question. Defaults pre-filled (Strongly Disagree → Strongly Agree). Note: distinct from Feature 1's data collection Likert, which uses fixed scale templates.
- **Star Rating:** Fixed 1–5 scale, not customizable
- **Multiple Choice:** Single or multi-select, with optional "Other" write-in toggle
- **Yes/No:** With optional "Other" write-in and optional custom label pair (e.g., "Agree / Disagree")
- **Short Answer:** Free text, optional character limit
- **Ranking:** Drag-to-order list of items, minimum 2 items

### 5.3 Scheduling
- **One-time send:** Admin selects a specific date and time
- **Recurring:** Google Calendar–style recurrence patterns (daily, weekly, monthly, by day of week, etc.) plus custom interval as fallback. When a new instance opens, the previous instance closes regardless of completion status.
- **Event-triggered (MVP):** Post-97156 session completion only. Architecture must accommodate future triggers (intake, auth expiration) without major rework. Event-trigger architecture is a pending decision (see Section 11).
- **Manual one-off send:** Supported for ad-hoc sends or recovery from scheduling failure
- **Market-based audience targeting:** Required at MVP. Admins target surveys to specific markets. Multi-market scheduling handled by duplicating survey instances (no batch targeting UI at MVP)

### 5.4 Respondent Experience (Flutter app — separate dev)
- One question per screen, auto-advance on selection (no "Proceed" button)
- Survey title is dynamic, sourced from admin configuration — not hardcoded
- Branching is invisible to parents; they see only the next relevant question
- Skipped questions recorded as `was_skipped` — distinct from unanswered; reporting must distinguish them
- When a survey is gated: blur overlay on main app content (similar to "no internet" pattern). Navigation to calendar, messages, and settings remains accessible. Full-screen takeover is NOT used.
- Closed surveys show a visible "closed" state in the app and are not answerable
- Survey history displayed with pagination or accordion (pattern TBD by Rosa; no unbounded scroll)

### 5.5 Reminders and Notifications
- Admin configures reminder cadence per survey (toggle on/off, cadence in days)
- Default cadence: every 2 days
- Quiet hours: 5pm–8pm in parent's local timezone (working assumption — pending clinical confirmation)
- Parent can override their personal notification preference
- Completing a survey suppresses all remaining reminders for that instance
- Push notification only at MVP

### 5.6 Gating
- Any survey can be flagged for gating at admin discretion (not a pre-approved list)
- Gating model: "days after sending" — admin sets a delay value. Default 0 = immediate gate
- Gating is managed by Super Admin only
- Blur overlay UX (see 5.4)

### 5.7 Reporting (CareConnect-native)
- Per-question results aggregated across instances
- Cross-instance trends
- Completion statistics
- Results accessible inside CareConnect — no PowerBI export at MVP

### 5.8 Access and Permissions
- Reuse existing CareConnect role and user-based permission system
- Cross-creator restriction: only the survey creator (or Super Admin) can edit a given survey; other VP-level users see read-only

### 5.9 Audit Logging
- All mutations logged using existing audit log helper service (never inline)
- Audit trail viewable from survey detail screen

### 5.10 Multi-language
- Admin UI: English only at MVP
- Respondent-facing (Flutter): English, Spanish, Arabic (Arabic requires RTL layout — Flutter-level concern, not just translation)

---

## 6. Feature Scope — OUT (MVP)

- DCS and OD role access to surveys or results
- Multi-editor / collaborator survey building
- Image or video embedding in questions
- File upload as a response type
- Question-level branching (section-level only at MVP)
- AI-assisted question generation
- Parent confirmation screen CTA (plain "Back to Home" only; schema fields preserved for later activation)
- PowerBI / external BI export
- Multi-language admin UI
- Approval workflow before publishing
- Schedule Next Session CTA in survey confirmation screen
- Multi-market batch scheduling UI (handled by instance duplication)
- Event triggers beyond post-97156 (intake, auth expiration deferred to Phase 2)
- Survey versioning for live-edit (edits to live surveys not supported at MVP — see open decision)

---

## 7. Milestones (mapped to epics in the new framework)

| Milestone | New Epic Name | Estimated Duration | Status |
|-----------|---------------|-------------------|--------|
| M0 — Foundation | epic-00-foundation | 1 week | In Progress |
| M1 — Survey CRUD | epic-01-survey-crud | 2 weeks | Partially ticketed |
| M2 — Question authoring | epic-02-question-authoring | 2 weeks | Partially ticketed |
| M3 — Sections + preview | epic-03-sections-preview | 1.5 weeks | Not started |
| M4 — Branching logic | epic-04-branching-logic | 2.5 weeks | Not started |
| M5 — Scheduling | epic-05-scheduling | 2 weeks | Not started |
| M6 — Reminders + gating | epic-06-reminders-gating | 2 weeks | Not started |
| M7 — Results + reporting | epic-07-results-reporting | 1.5 weeks | Not started |
| M8 — Hardening + launch | epic-08-hardening-launch | 1.5 weeks | Not started |

**Total estimate:** 14–18 weeks (backend + CareConnect admin UI only)
**Flutter respondent app:** Separate developer, separate timeline, after API contract is stable

---

## 8. Technical Constraints

- Backend scope only at this phase: CareConnect admin UI + APIs
- Flutter parent app is a separate dev, separate timeline
- API contract must be documented (OpenAPI) before Flutter dev starts — it is the contract they build against
- Existing CareConnect role/permission system must be reused — no new role taxonomy
- Audit logging must use the existing audit log helper service
- Arabic RTL is a Flutter-level concern — requires explicit scoping with Flutter dev

---

## 9. Non-Functional Requirements

- HIPAA compliance for all survey response data
- Audit trail for all admin mutations
- Performance: survey list loads under 2 seconds for up to 500 surveys
- Accessibility: WCAG 2.1 AA on CareConnect admin UI

---

## 10. Feature Areas with Hidden Complexity

- **Branching engine (M4):** Multi-level nesting plus dynamic recalculation on back-navigation. Allow buffer time. This is the riskiest milestone.
- **Scheduling/recurring (M5):** Time-based logic requires mocked-clock testing infrastructure
- **Live survey edit safety (M8):** Requires survey versioning — a foundational decision (see open decisions)
- **Arabic RTL support:** Flutter-level, not just translation — needs explicit scoping with Flutter dev

---

## 11. Open Decisions

| # | Decision | Owner | Blocks |
|---|----------|-------|--------|
| 1 | Final quiet hours for notifications | Clinical leadership confirmation | M6 |
| 2 | Default confirmation message text | PM + Kerri | M3 |
| 3 | Audit trail retention period | Engineering / Compliance | M8 |
| 4 | Live survey edit behavior — working proposal: edits apply only to new respondents, in-progress responses pinned to version they started. Requires survey versioning in data model. | PM confirmation | M1 data model, M8 |
| 5 | Event-trigger architecture — post-97156 is the only MVP trigger; architecture must be extensible for intake and auth expiration in Phase 2 | Kerri + Timothy + Emily; Son + Harish to propose | M5.4 only (M5.1–5.3, 5.5, 5.6 unblocked) |
| 6 | Survey history UI pattern — pagination vs. accordion | Rosa (design) | Flutter app |

---

## 12. Resolved Decisions Reference

| Topic | Resolution |
|-------|-----------|
| Survey Administrator role | Existing CC role and user-based permission system. VP-level = admin. No new role taxonomy. |
| Quiet hours working assumption | 5pm–8pm parent local timezone (pending clinical confirmation — see open decision #1) |
| Gating eligibility | Any survey at admin discretion; not a pre-approved list |
| Reporting surface | CareConnect-native; PowerBI deferred |
| Confirmation screen CTA | Deferred from MVP — plain "Back to Home" only |
| Question types | Six types: Likert, Star Rating, Multiple Choice, Yes/No, Short Answer, Ranking |
| Likert customization | Per-question label customization for Survey Builder Likert (5 labels, defaults pre-filled). Distinct from Feature 1's fixed Likert. |
| Star rating customization | None — fixed 1–5 |
| Section requirement | Every question belongs to a section; default section auto-created |
| Branching scope | Section-level only; Google Forms parity |
| Auto-advance UX | Selecting an answer advances to next question — no Proceed button |
| File attachments | Not supported at MVP |
| Closed surveys | Visibly marked in app, not answerable |
| Recurring scheduling pattern | Google Calendar–style patterns, plus custom interval as fallback |
| Multi-market scheduling | Handled by duplicating survey instances (no batch scheduling at MVP) |
| Audience targeting | Market-based targeting required at MVP |
| Manual one-off send | Supported for ad-hoc cases or scheduling failure recovery |
| Gating model | "Days after sending" delay value; default 0 = immediate |
| Gating UI pattern | Blur overlay on main content — not full-screen takeover |
| Event-trigger MVP scope | Post-97156 session completion only. Intake and auth expiration deferred to Phase 2. |
| Cross-creator restriction | Only the survey creator (or Super Admin) can edit; others see read-only |
| Audit logging | Use existing audit log helper service — never inline |
| Skipped questions | Recorded as `was_skipped = true` — distinct from unanswered |
| Recurring instance behavior | New instance opening closes previous instance regardless of completion status |
| Branching visibility | Invisible to parents — they see only next relevant question |
| Multi-language | English + Spanish + Arabic (Arabic = RTL, Flutter-level concern) |
