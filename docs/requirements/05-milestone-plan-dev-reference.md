# Survey Builder — Milestone Plan (Claude Code Dev Reference)

This document is the implementation-level companion to the user stories.
It maps business stories to technical milestones with file hints and briefings for Claude Code sessions.

**Scope:** Backend + CareConnect admin UI. Flutter app is a separate dev, separate plan.
**Team:** 1 developer
**Total estimate:** 14–18 weeks

---

## Milestone 0 — Foundation & Scaffolding (Week 1)

**Goal:** Working dev environment, CI baseline, auth wired, empty Surveys section visible in CareConnect.

### M0.1 — Repo and folder structure
- Repo created, docs and architecture folders in place
- README and ROADMAP committed

### M0.2 — Surveys nav entry in CareConnect (role-gated)
**AC:**
- "Surveys" appears in CareConnect main nav
- Visible to VP-level and Super Admin only
- DCS and OD users: link hidden AND direct URL returns 403
- Clicking navigates to placeholder page ("Coming soon")
**Files:** CareConnect nav config, route table, role-check middleware
**Claude Code briefing:** "Read /docs/architecture/auth-roles.md. Add a Surveys nav entry visible only to VP-level and Super Admin roles. Route to a placeholder page. DCS and OD must be blocked at the URL level too."

### M0.3 — Role provisioning check
**AC:**
- Existing CareConnect role system documented in /docs/architecture/auth-roles.md
- Role-based middleware confirmed working for the /surveys route
**Claude Code briefing:** "Inspect the existing CareConnect role and permission system. Document it in /docs/architecture/auth-roles.md. Confirm middleware is wired to the /surveys route."

### M0.4 — CI pipeline
**AC:**
- GitHub Action runs on every push: lint, type check, build, tests
- PR merges blocked if CI fails

### M0.5 — E2E testing framework
**AC:**
- Playwright installed and configured
- First passing test: navigate to /surveys as VP-level user, confirm nav entry is visible
- First failing test: navigate to /surveys as DCS user, confirm 403

---

## Milestone 1 — Survey CRUD & Data Model (Weeks 2–3)

**Goal:** Admin can create, save, list, and delete draft surveys. No questions yet — survey-level metadata only.

### M1.1 — Survey data model and migration
**AC:**
- `surveys` table: id, title, description, status (draft/scheduled/live/closed), created_by, market_id, schedule (JSON), gating fields, confirmation_message, hide_response_history, timestamps
- `survey_audit_log` table: survey_id, actor_id, action, metadata, timestamp
- Status enum enforced at DB level
- `section_id` is NOT nullable on questions — default section must always exist (enforce in M2)
- Migration runs cleanly forward and backward
**Files:** /db/migrations/, /src/models/Survey.ts
**Claude Code briefing:** "Create the surveys table migration per the data model in /docs/architecture/data-model.md. Include the audit log table. Status must be a DB enum. Default section requirement will be enforced in M2 — leave a note."

### M1.2 — Survey API (CRUD)
**AC:**
- POST /surveys — creates draft
- GET /surveys — list with filters: status, created_by, market, date range
- GET /surveys/:id — full detail
- PUT /surveys/:id — update metadata; returns 409 if survey is closed
- DELETE /surveys/:id — draft only; returns 409 if not draft
- All write endpoints: role check (VP+ only) + audit log entry
- OpenAPI spec auto-generated to /docs/api/openapi.yaml
**Dependencies:** M1.1
**Claude Code briefing:** "Implement the survey CRUD API. Every write endpoint must: (1) enforce VP-level role check using existing middleware, (2) append an entry to the audit log using the existing helper service — never write audit rows inline. Generate the OpenAPI spec."

### M1.3 — Survey list screen in CareConnect
**AC:**
- Table: name, status badge (teal=Live, amber=Scheduled, gray=Draft/Closed), type, last sent, completion %
- Filters: status, creator, search by name
- "+ Create Survey" creates draft, navigates to builder
- Empty state with "Create your first survey" prompt
- Other VP admins see surveys in list but edit controls are disabled
**Dependencies:** M1.2
**Claude Code briefing:** "Build the survey list screen. Read /docs/architecture/careconnect-ui-patterns.md for component conventions. Status badge colors: teal for Live, amber for Scheduled, gray for Draft/Closed. Cross-creator restriction: edit controls shown only to the creator and Super Admin."

### M1.4 — Survey detail / settings screen (no questions yet)
**AC:**
- Edit title and description
- Auto-save on change (no explicit Save button needed here — but Save button also available)
- Status and audit trail accessible
- Empty surveys cannot be published (validation blocks it)
- Audit trail panel: read-only list of changes
**Dependencies:** M1.2

### M1.5 — Survey duplication
**AC:**
- Duplicate button available on any survey (any status)
- Duplicate creates new draft: "Copy of [title]", same questions/sections, same schedule structure — but no audience, no send date, status = Draft
- Original responses not included in duplicate
**Dependencies:** M1.1, M1.2

---

## Milestone 2 — Question Authoring (Weeks 4–5)

**Goal:** Admin can add, edit, delete, and reorder all six question types within a survey. Sections are required.

### M2.1 — Section data model and API
**AC:**
- `sections` table: id, title, description, order, survey_id
- Section CRUD API
- Questions must have a section_id (NOT NULL)
- Default section auto-created when a new survey is created
- Section deletion: reassigns orphaned questions to default section (or blocks if it is the last section)
**Claude Code briefing:** "Add the sections table. section_id must be NOT NULL on the questions table. Auto-create a default section titled 'Questions' when a new survey is created. Section deletion must handle orphaned questions."

### M2.2 — Section UI in builder
**AC:**
- Left panel renders sections as collapsible groups
- Drag question into/between sections
- Edit section title and description in right panel when section selected
- Sections can be reordered
- Questions within sections retain their order
**Dependencies:** M2.1

### M2.3 — Question editor — shared controls
**AC:**
- Each question has: question text, required/optional toggle, help text (optional)
- Questions can be reordered within a section via drag-and-drop
- Delete question (with confirmation if branching logic references it)
- Each question has a type selector (shown only on creation; changing type clears type-specific config)
**Dependencies:** M2.1

### M2.4 — Question editor — Likert
**AC:**
- Admin selects a label set from the shared library OR customizes 5 labels inline per question
- Default label set pre-filled (Strongly Disagree → Strongly Agree) but editable
- Custom labels saved with the question (not added to the shared library)
- Renders as 5-point scale in preview
**Dependencies:** M2.3
**Note:** This is Survey Builder Likert — different from Feature 1 data collection Likert (fixed).

### M2.5 — Question editor — Multiple Choice
**AC:**
- Add/remove/reorder options
- Toggle: single-select vs. multi-select
- Toggle: "Other" write-in
- Minimum 2 options enforced on save
**Dependencies:** M2.3

### M2.6 — Question editor — Yes/No
**AC:**
- Default labels "Yes" / "No" (overridable, e.g., "Agree" / "Disagree")
- Optional "Other" write-in toggle
**Dependencies:** M2.3

### M2.7 — Question editor — Short Answer
**AC:**
- Optional character limit field
- Validation: limit must be a positive integer if set
**Dependencies:** M2.3

### M2.8 — Question editor — Ranking
**AC:**
- Add/remove/reorder items
- Minimum 2 items enforced on save
- Default admin-set order shown; respondent reorders in app
**Dependencies:** M2.3

### M2.9 — Question editor — Star Rating
**AC:**
- Fixed 1–5 scale, no customization
- Renders as 5-star display in preview
**Dependencies:** M2.3

---

## Milestone 3 — Preview (Weeks 6–7)

**Goal:** Admin can preview the survey in a mobile frame before publishing.

### M3.1 — Preview mode (mobile frame, English only, no branching)
**AC:**
- Preview button opens modal with mobile frame (iPhone-style)
- One question per screen
- Section titles appear above first question of section
- All 6 question types render correctly
- Navigate forward and back through questions
- Clearly labeled "Preview mode — responses not recorded"
- Auto-advance UX simulated (tapping an answer advances screen)
**Dependencies:** M2.4–M2.9

### M3.2 — Default confirmation message stub
**AC:**
- Confirmation screen shown after final question in preview
- Default message text displayed (text to be confirmed — see open decision #2)
- Schema field `confirmation_message` on surveys table accepts override text

---

## Milestone 4 — Branching Logic (Weeks 8–10)

**Goal:** Admin can configure section-level conditional logic. This is the riskiest milestone — allow buffer.

### M4.1 — Branching data model
**AC:**
- ConditionalLogic table: source_question_id, trigger_answer, action (skip_to_section / end_survey), target_section_id
- Multiple rules per question supported
- Validation: target must be a forward section (not current or previous)
- Circular logic detection (MVP: basic forward-only enforcement)
**Claude Code briefing:** "Add the ConditionalLogic table. Branching is section-level only — no question-level skip targets. Target must always be a forward section. Document the data model in /docs/architecture/branching-engine.md."

### M4.2 — Branching API
**AC:**
- Endpoints to add/edit/remove rules on a question
- Validation: target exists, is forward-direction, is in the same survey
- Returns 422 with specific errors for invalid configs
**Dependencies:** M4.1

### M4.3 — Branching UI in question editor
**AC:**
- Conditional Logic panel (collapsible) on each question
- "If this question = [answer], then skip to [section] OR end survey"
- Target section selector dynamically populated
- Visual indicator on question card when branching is configured
- Removing a section that is a branching target: warns admin and removes the rule
**Dependencies:** M4.2

### M4.4 — Branching engine (server-side path resolver)
**AC:**
- Function: (survey, current_question_id, answers_so_far) → next_question_id OR "end"
- Multi-level nesting: if skip takes respondent to section 3, and section 3 has its own rule, it evaluates correctly
- Engine has unit tests: simple skip, nested skip, end-survey, no-branch path
- Back-navigation: recalculates path based on updated answers (changing an earlier answer may change the path)
- Skipped questions recorded as `was_skipped = true`
- Engine documented in /docs/architecture/branching-engine.md
**Dependencies:** M4.1

### M4.5 — Preview mode with branching
**AC:**
- Preview mode uses the branching engine
- Selecting an answer that triggers a rule skips to the correct section
- Skipped questions are not shown (invisible to the user)
- Back navigation recalculates path
**Dependencies:** M4.4, M3.1

---

## Milestone 5 — Scheduling & Delivery (Weeks 11–12)

**Goal:** One-time, recurring, and manual sends working end-to-end. Event-triggered (M5.4) is blocked pending architecture decision.

### M5.1 — Schedule configuration UI
**AC:**
- Settings drawer includes Schedule section
- Three send types: One-time, Recurring, Event-triggered (MVP: post-97156 only)
- One-time: date/time picker, must be in the future
- Recurring: Google Calendar–style pattern builder (daily, weekly on specific days, monthly, custom interval fallback)
- Recurring: optional end date
- Recurring: "Preview upcoming dates" shows next 5 instances
- Market audience selector required for all types
- Validation blocks publishing without valid schedule and audience

### M5.2 — Survey instance data model
**AC:**
- SurveyAssignment table: survey_id, instance_id, client_id, assigned_at, due_at, status (pending/in_progress/completed/expired), reminder_count, parent_reminder_override
- Status transitions logged to audit
**Dependencies:** M1.1

### M5.3 — Scheduler / cron job for recurring surveys
**AC:**
- Background job runs daily, evaluates active recurring surveys
- For each due instance: closes previous instance (regardless of completion), creates new SurveyAssignments for active caseload in target market
- Families added mid-cycle start from next instance
- Discharged families excluded from future instances
- Manual trigger endpoint exists for testing
- Mocked-clock testing infrastructure included
**Dependencies:** M5.2

### M5.4 — Event trigger handler (post-97156) ⚠️ BLOCKED
**Status:** Blocked pending architecture decision
**Waiting on:** Kerri + Timothy + Emily (business decision); Son + Harish (architecture proposal)
**Do not start until unblocked.**

### M5.5 — Survey publishing flow
**AC:**
- Publish button on builder
- Pre-publish validation: at least one question, valid schedule, audience selected, no orphan branching targets
- Publishing transitions: draft → scheduled (if future) OR draft → live (if immediate)
- Audit log records publish event
- Confirmation dialog summarizes: send type, audience, send date
**Dependencies:** M5.1

### M5.6 — Survey deactivation / closing
**AC:**
- Admin can close a Live survey from survey list or detail screen
- Confirmation dialog shows count of in-progress responses
- Closure: status → Closed, scheduler stops creating new instances
- Existing in-progress responses remain submittable for a grace period (TBD — default 24h)
**Dependencies:** M5.5

### M5.7 — Manual one-off send
**AC:**
- "Send Now" button on a published survey
- Confirmation shows audience and asks to confirm
- Creates a new instance labeled "Manual send"
- Appears in survey history with send date and completion stats
**Dependencies:** M5.2

---

## Milestone 6 — Reminders & Gating (Weeks 13–14)

### M6.1 — Reminder cadence configuration
**AC:**
- Settings drawer: Reminders section with toggle on/off
- Default cadence: every 2 days (admin-configurable)
- Settings saved per survey

### M6.2 — Push notification dispatch
**AC:**
- Notification service sends push on schedule per reminder cadence
- Quiet hours enforced: 5pm–8pm parent local timezone (working assumption — see open decision #1)
- Message: "You have a survey to complete"

### M6.3 — Parent reminder override
**AC:**
- Parent can toggle their personal notification preference in app settings
- Override recorded per parent per survey instance

### M6.4 — Completion suppression
**AC:**
- When a parent submits a completed survey, all pending reminders for that instance are cancelled
- No "you have a survey" notification fires after completion

### M6.5 — Gating configuration (Super Admin only)
**AC:**
- Gating toggle available on survey settings (Super Admin only — VP-level admins cannot see this control)
- Delay setting: "days after sending" — input field, default 0 = immediate
- Gate is linked to a specific survey instance

### M6.6 — Gating enforcement and blur overlay
**AC:**
- When a gating-active survey is pending for a parent, main app content is blurred
- Calendar, messages, and settings navigation remains accessible
- Full-screen takeover is NOT used
- Gate lifts immediately when survey is submitted
- Parents who complete the survey before the gate delay expires: gate never activates

---

## Milestone 7 — Results & Reporting (Weeks 15–16)

### M7.1 — Response storage
**AC:**
- SurveyResponse table: instance_id, client_id, question_id, answer_value, was_skipped, submitted_at
- `was_skipped` is distinct from null/unanswered
- Responses immutable once submitted

### M7.2 — Per-question result aggregation
**AC:**
- Admin can view results for any closed or live survey
- Per question: response distribution (counts and percentages per answer option)
- Skipped responses shown separately from answered responses

### M7.3 — Cross-instance trend view
**AC:**
- For recurring surveys: aggregate completion % and response distributions across instances
- Timeline view showing how results shift over time

### M7.4 — Completion statistics
**AC:**
- Per instance: total sent, total completed, completion %, average time to complete

---

## Milestone 8 — Hardening & Launch Prep (Weeks 17–18)

### M8.1 — Audit trail UI
**AC:**
- Audit trail panel accessible from survey detail
- Shows: action, actor, timestamp, metadata summary
- Read-only; paginated

### M8.2 — Multi-language admin support
**AC:**
- Admin UI: English only (no change)
- Respondent content fields (question text, section titles, confirmation message) accept Spanish and Arabic translations
- Arabic content: RTL flag set (Flutter renders accordingly)

### M8.3 — Edge case hardening
**AC:**
- Live-edit behavior formally confirmed and implemented (see open decision #4)
- Survey with 0 responses closes cleanly
- Scheduler handles daylight saving time transitions
- Branching engine handles 100+ question surveys without performance degradation

### M8.4 — API contract review
**AC:**
- OpenAPI spec reviewed with Flutter dev before they start
- All response schemas match what Flutter needs
- Breaking changes identified and resolved

---

## Development Anti-Patterns

These are known failure modes. Do not do these.

- **Do not write audit log rows inline.** Always use the existing audit log helper service.
- **Do not conflate Survey Builder Likert with Feature 1 data collection Likert.** They are different. Survey Builder Likert has customizable labels. Data collection Likert uses fixed templates.
- **Do not allow questions without a section.** section_id is NOT NULL — the default section must be auto-created.
- **Do not start M5.4 (event triggers) before the architecture decision is resolved.**
- **Do not design the gating UI as a full-screen takeover.** It is a blur overlay.
- **Do not build auto-advance as a "Proceed" button.** Selecting an answer advances automatically.
- **Do not use unbounded scroll for survey history.** Pagination or accordion only.
- **Do not use the date library before a decision record locks the choice.** Check /docs/architecture/decisions/ for the date library decision.

---

## Key Architecture References

- `/docs/architecture/auth-roles.md` — existing CC role system (written in M0.3)
- `/docs/architecture/data-model.md` — full survey data model
- `/docs/architecture/branching-engine.md` — branching path resolver spec (written in M4.4)
- `/docs/api/openapi.yaml` — auto-generated, updated each milestone
- `/docs/requirements/01-PRD-v1.1.md` — product requirements
- `/docs/requirements/02-decisions-log.md` — all resolved and open decisions
