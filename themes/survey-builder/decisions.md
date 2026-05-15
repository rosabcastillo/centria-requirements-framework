# Decisions — Survey Builder

---

## Product Decisions

### 2026-04 — Survey Administrator role uses existing CC permission system
**Decided:** No new role types. Reuse existing CareConnect role and user-based permission system. VP-level users = Survey Administrator. Super Admin (IT-granted) = elevated permissions including gating.
**Decided by:** Pawanjit, PM
**Why:** CC already has a well-defined permission system. New roles create redundancy and migration overhead.
**Alternatives considered:** Dedicated SurveyAdmin and SurveySuperAdmin roles — rejected.
**Implications:** Dev reads existing role docs and reuses middleware. DCS and OD have zero access.

### 2026-04 — Question types locked at six for MVP
**Decided:** Likert, Star Rating, Multiple Choice, Yes/No, Short Answer, Ranking.
**Decided by:** PM + Kerri
**Why:** Covers all identified use cases. Keeps data model manageable.
**Alternatives considered:** File upload, image embedding — explicitly deferred.
**Implications:** Data model stores all answer values as normalized string for future flexibility.

### 2026-04 — Gating eligibility: any survey at admin discretion
**Decided:** Any survey can be flagged for gating. No pre-approved list.
**Decided by:** PM
**Why:** Flexibility for clinical team to gate based on context.
**Implications:** Gating configuration UI must be accessible on any survey.

### 2026-04 — Confirmation screen CTA deferred from MVP
**Decided:** Plain "Back to Home" only. No configurable CTA at MVP.
**Decided by:** PM
**Why:** Out of scope for this phase.
**Implications:** Schema must include CTA fields for future activation; not exposed in UI.

### 2026-05-06 — Likert labels: customizable per question in Survey Builder
**Decided:** Each Survey Builder Likert question has 5 admin-customizable labels. Standard agree-disagree set is the default (pre-filled). Distinct from Feature 1 (data collection) Likert, which remains fixed.
**Decided by:** Kerri (May 6 SME session)
**Why:** Survey Builder needs flexibility for different outcome measures.
**Conflicts with:** Original PRD stated scale templates were not customizable — superseded for Survey Builder only.
**Implications:** Data model must store 5 labels per Likert question. Aggregation logic must be label-aware.

### 2026-05-06 — Star rating: fixed 1–5, not customizable
**Decided:** Star rating is always 1–5. No label customization.
**Decided by:** Kerri (May 6 SME session)

### 2026-05-06 — Section requirement: every question must belong to a section
**Decided:** No orphan questions. Default section auto-created on survey creation. Admins can rename or add more.
**Decided by:** Kerri (May 6 SME session)
**Implications:** section_id is NOT nullable on questions. M1 data model must reflect this.

### 2026-05-06 — Auto-advance respondent UX
**Decided:** Selecting an answer advances to the next question automatically. No "Proceed" button.
**Decided by:** Kerri (May 6 SME session)
**Implications:** Flutter UX — each question screen advances on tap/selection.

### 2026-05-06 — Gating UX: blur overlay, not full-screen takeover
**Decided:** When a gating-active survey is required, main app content is blurred. Navigation to calendar, messages, and settings remains accessible.
**Decided by:** Kerri (May 6 SME session)
**Why:** Full-screen takeover was "too aggressive."
**Implications:** Flutter UX change. Rosa to provide reference video of blur effect.

### 2026-05-06 — Recurring scheduling: Google Calendar–style patterns
**Decided:** Recurring surveys use RRULE patterns (daily, weekly, monthly, by day of week) plus custom interval fallback.
**Decided by:** Kerri (May 6 SME session)
**Implications:** Scheduling UI requires a calendar-style builder.

### 2026-05-06 — Market-based audience targeting required at MVP
**Decided:** Admins target surveys at a market level. Multi-market = duplicate survey instances. No batch targeting UI.
**Decided by:** Kerri (May 6 SME session)
**Implications:** Survey data model includes market field. Admin UI must include market selector.

### 2026-05-06 — Manual one-off send supported
**Decided:** Admins can send a survey manually as a one-off, outside any scheduled cadence.
**Decided by:** Kerri (May 6 SME session)

### 2026-05-06 — Gating model: days after sending, default 0
**Decided:** Gating delay expressed as "days after sending." Default 0 = immediate gate.
**Decided by:** Kerri (May 6 SME session)
**Implications:** Admin UI uses day-count input, not date picker.

### 2026-05-06 — Dynamic survey title
**Decided:** Survey title shown to respondents comes from admin configuration — not hardcoded.
**Decided by:** Kerri (May 6 SME session)
**Implies:** Admin builder must prominently surface the title input field.

### 2026-05-06 — Event-trigger MVP scope: post-97156 only
**Decided:** The only event trigger at MVP is post-97156 session completion. Architecture must accommodate future triggers without major rework.
**Decided by:** PM (May 6 SME session)
**Implications:** M5.4 is the only blocked story in the scheduling epic.

### 2026-05-06 — Cross-creator restriction
**Decided:** Only the survey creator (or Super Admin) can edit a given survey. Other VP-level users see read-only.
**Decided by:** PM
**Implications:** Edit permissions must check both role and creator identity.

### 2026-05-06 — Skipped questions recorded distinctly
**Decided:** Questions skipped by branching logic are recorded as was_skipped = true. Distinct from blank/unanswered.
**Decided by:** PM
**Implications:** Response data model needs a skipped flag per answer. Reporting must distinguish skipped vs. unanswered.

### 2026-05-06 — Recurring instance behavior
**Decided:** When a new recurring instance opens, the previous closes regardless of completion status.
**Decided by:** PM
**Implications:** Instance lifecycle logic in scheduling must enforce this.

### 2026-05-06 — Branching invisible to respondents
**Decided:** Parents see only the next relevant question. No indication of skipped questions or branching.
**Decided by:** PM / Kerri

---

## Architecture Decisions

### 2026-04 — Audit logging via existing helper service
**Decided:** All mutations use the existing audit log helper service. No inline audit log writes.
**Decided by:** PM
**Implications:** Dev must understand the existing audit log helper API before starting Epic 01.

### 2026-05-06 — Live survey edit behavior (provisional)
**Status:** ⚠️ PROVISIONAL — needs formal PM confirmation before Epic 01 data model work begins
**Decided (provisional):** Edits apply only to new respondents. In-progress responses pinned to the version they started. Requires survey versioning in the data model.
**Implications:** Survey versioning must be built into the data model from day one.

### 2026-04 — Reporting: CareConnect-native, no PowerBI
**Decided:** No ETL pipeline or BI integration at MVP.

### 2026-05 — Status enum: draft / scheduled / live / closed
**Decided:** Four states, enforced at DB level as an enum.

### 2026-05 — Survey history: pagination or accordion — never unbounded scroll
**Decided:** Unbounded scroll is explicitly ruled out. Pattern (pagination vs accordion) TBD by Rosa (open decision #6).

---

## Open Decisions

| # | Decision | Owner | Blocks | Notes |
|---|----------|-------|--------|-------|
| 1 | Final notification quiet hours | Clinical leadership | Epic 04 | Working assumption: 5pm–8pm parent local timezone |
| 2 | Default confirmation message text | PM + Kerri | Epic 02 (M3.2) | What's the default thank-you text admins can override |
| 3 | Audit trail retention period | Engineering / Compliance | Epic hardening | 1 year? 7 years? Affects storage planning |
| 4 | Live survey edit behavior (formal confirmation) | PM | Epic 01 data model | Working proposal: edits apply to new respondents only, versioning required |
| 5 | Event-trigger architecture for post-97156 | Kerri + Timothy + Emily; Son + Harish | Epic 03 story Q1–Q3 only | Architectural design meeting needed. Do NOT start Q1–Q3 until resolved. |
| 6 | Survey history UI pattern (pagination vs. accordion) | Rosa | Epic 07 (Flutter app) | Pattern TBD by design |
