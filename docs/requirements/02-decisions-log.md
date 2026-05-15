# Survey Builder — Decisions Log

All decisions made during planning across multiple sessions.
Format: resolved decisions with full context, then open decisions with owners.

---

## Resolved Decisions

### 2026-04 — Survey Administrator role uses existing CC permission system
**Decided:** No new role types. Reuse existing CareConnect role and user-based permission system. VP-level users = Survey Administrator capability. Super Admin (IT-granted) = elevated permissions including gating.
**Decided by:** Pawanjit, PM
**Why:** CC already has a well-defined permission system. Inventing new roles creates redundancy and migration overhead.
**Alternatives considered:** Dedicated SurveyAdmin and SurveySuperAdmin roles — rejected.
**Implications:** Dev reads existing role docs and reuses middleware. DCS and OD have zero access.

---

### 2026-04 — Question types locked at six for MVP
**Decided:** Likert, Star Rating, Multiple Choice, Yes/No, Short Answer, Ranking.
**Decided by:** PM + Kerri
**Why:** Covers all identified use cases from stakeholder requirements. Keeps data model manageable.
**Alternatives considered:** Adding file upload and image embedding — explicitly deferred.
**Implications:** Data model stores all answer values as normalized string for future flexibility.

---

### 2026-04 — Gating eligibility: any survey at admin discretion
**Decided:** Any survey can be flagged for gating. No pre-approved list required.
**Decided by:** PM
**Why:** Flexibility for clinical team to gate based on context, not a fixed taxonomy.
**Implications:** Gating configuration UI must be accessible on any survey.

---

### 2026-04 — Reporting surface: CareConnect-native, no PowerBI
**Decided:** Results and aggregation live inside CareConnect. PowerBI export deferred or out of scope.
**Decided by:** PM + Pawanjit
**Why:** Reduces external dependency. CareConnect is where clinical staff already work.
**Implications:** No ETL pipeline or BI integration needed for MVP.

---

### 2026-04 — Confirmation screen CTA deferred from MVP
**Decided:** Plain "Back to Home" only. No configurable CTA at MVP.
**Decided by:** PM
**Why:** Out of scope for this phase. Schema fields preserved for later activation.
**Implications:** Schema must include fields for future CTA config; just not exposed in UI.

---

### 2026-04 — Live survey edits: provisional working proposal
**Decided (provisional — needs PM confirmation):** Edits apply only to new respondents. In-progress responses are pinned to the version they started. Requires survey versioning in the data model.
**Decided by:** PM (provisional)
**Status:** ⚠️ Needs formal confirmation before M1 data model work begins
**Implications:** Survey versioning must be built into the data model from day one. Significant complexity.

---

### 2026-05-06 — Likert labels: customizable per question in Survey Builder
**Decided:** Each Survey Builder Likert question has 5 admin-customizable labels. Standard agree-disagree set is the default (pre-filled). This is distinct from Feature 1 (data collection) Likert, which remains fixed.
**Decided by:** Kerri (May 6 SME session)
**Why:** Survey Builder needs flexibility for different outcome measures (e.g., frequency scales, satisfaction scales).
**Conflicts with:** Original PRD stated scale templates were not customizable — superseded by this decision for Survey Builder only.
**Implications:** Data model must store 5 labels per Likert question. Aggregation logic must be label-aware.

---

### 2026-05-06 — Star rating: fixed 1–5, not customizable
**Decided:** Star rating is always 1–5. No label customization.
**Decided by:** Kerri (May 6 SME session)

---

### 2026-05-06 — Section requirement: every question must belong to a section
**Decided:** No orphan questions. Default section is auto-created on survey creation. Admins can rename it or add more sections.
**Decided by:** Kerri (May 6 SME session)
**Implications:** `section_id` is not nullable on questions. M1 data model must reflect this.

---

### 2026-05-06 — Auto-advance respondent UX
**Decided:** Selecting an answer advances to the next question automatically. No "Proceed" button.
**Decided by:** Kerri (May 6 SME session)
**Implications:** Flutter app UX — each question screen advances on tap/selection.

---

### 2026-05-06 — Gating UX: blur overlay, not full-screen takeover
**Decided:** When a gating-active survey is required, the main app content is blurred (similar to the "no internet" pattern). Navigation to calendar, messages, and settings remains accessible.
**Decided by:** Kerri (May 6 SME session)
**Why:** Full-screen takeover was "too aggressive" and presented too much information upfront.
**Implications:** Flutter app UX change. Rosa to provide reference video of blur effect.

---

### 2026-05-06 — Recurring scheduling: Google Calendar–style patterns
**Decided:** Recurring surveys use Google Calendar–style RRULE patterns (daily, weekly, monthly, by day of week, etc.) plus custom interval as a fallback. Replaces the original "interval in days" approach.
**Decided by:** Kerri (May 6 SME session)
**Implications:** Scheduling UI requires a calendar-style builder. M5.1 scoped accordingly.

---

### 2026-05-06 — Market-based audience targeting required at MVP
**Decided:** Admins target surveys at a market level. Multi-market scheduling is handled by duplicating survey instances — no batch targeting UI at MVP.
**Decided by:** Kerri (May 6 SME session, confirmed)
**Implications:** Survey data model includes market field. Admin UI must include market selector.

---

### 2026-05-06 — Manual one-off send supported
**Decided:** Admins can send a survey manually as a one-off, outside any scheduled cadence. Useful for ad-hoc sends or recovery from scheduling failure.
**Decided by:** Kerri (May 6 SME session)

---

### 2026-05-06 — Gating model: days after sending, default 0
**Decided:** Gating delay is expressed as "days after sending." Default value of 0 means immediate gate (as soon as survey is sent).
**Decided by:** Kerri (May 6 SME session, confirmed)
**Implications:** Admin UI replaces date picker with a day-count input. M6.4 scoped accordingly.

---

### 2026-05-06 — Dynamic survey title
**Decided:** The survey title shown to respondents comes from admin configuration — not hardcoded in the app.
**Decided by:** Kerri (May 6 SME session)
**Implies:** Admin builder must prominently surface the title input field.

---

### 2026-05-06 — Event-trigger MVP scope: post-97156 only
**Decided:** The only event trigger implemented at MVP is post-97156 session completion. Architecture must accommodate future triggers (intake, auth expiration) without major rework.
**Decided by:** PM (May 6 SME session)
**Implications:** M5.4 is the only blocked story in M5. M5.1, M5.2, M5.3, M5.5, M5.6 are unblocked and can proceed.

---

### 2026-05-06 — Cross-creator restriction
**Decided:** Only the survey creator (or Super Admin) can edit a given survey. Other VP-level users see read-only.
**Decided by:** PM
**Implications:** Edit permissions must check both role and creator identity.

---

### 2026-05-06 — Audit logging via existing helper service
**Decided:** All mutations use the existing audit log helper service. No inline audit log writes.
**Decided by:** PM
**Implications:** Dev must understand the existing audit log helper API before starting M1.

---

### 2026-05-06 — Skipped questions recorded distinctly
**Decided:** Questions skipped by branching logic are recorded as `was_skipped = true`. Distinct from questions the respondent left blank. Reporting must distinguish between skipped and unanswered.
**Decided by:** PM
**Implications:** Response data model needs a skipped flag per answer.

---

### 2026-05-06 — Recurring instance behavior
**Decided:** When a new recurring instance opens, the previous instance closes regardless of completion status.
**Decided by:** PM
**Implications:** Instance lifecycle logic in M5 scheduler must enforce this.

---

### 2026-05-06 — Branching invisible to respondents
**Decided:** Parents see only the next relevant question. No indication of skipped questions or branching logic.
**Decided by:** PM / Kerri

---

## Open Decisions

| # | Decision | Owner | Blocks | Notes |
|---|----------|-------|--------|-------|
| 1 | Final notification quiet hours | Clinical leadership | M6 | Working assumption: 5pm–8pm parent local timezone |
| 2 | Default confirmation message text | PM + Kerri | M3 | What's the default thank-you text admins can override |
| 3 | Audit trail retention period | Engineering / Compliance | M8 | 1 year? 7 years? Affects storage planning |
| 4 | Live survey edit behavior (formal confirmation) | PM | M1 data model, M8 | Working proposal: edits apply to new respondents only, versioning required |
| 5 | Event-trigger architecture for post-97156 | Kerri + Timothy + Emily; Son + Harish to propose | M5.4 only | Architectural design meeting needed |
| 6 | Survey history UI pattern (pagination vs. accordion) | Rosa | Flutter app | Pattern TBD by design |
