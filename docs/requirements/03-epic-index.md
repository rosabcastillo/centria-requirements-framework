# Survey Builder — Epic Index

All epics for the Survey Builder feature. Stories are tracked in individual epic files.
Use this as the master index and status tracker.

---

## Epic Map

```
Survey Builder Feature
├── epic-00-foundation
├── epic-01-survey-crud-and-lifecycle      ← Survey Creation & Status Management
├── epic-02-sections-questions-branching   ← Sections, Questions & Branching
├── epic-03-scheduling                     ← Recurring & Event-Triggered Scheduling
├── epic-04-reminders-notifications        ← Reminders & Notifications
├── epic-05-gating                         ← Survey Gating
├── epic-06-reporting                      ← Reporting & Aggregation
└── epic-07-mobile-integration             ← Flutter Respondent App (separate dev)
```

---

## Epic 00 — Foundation

**Status:** 🔵 In Progress
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin

**Goal:** Working dev environment, repo structure, CI baseline, auth wired, empty Surveys section visible in CareConnect.

**Stories:**
| ID | Title | Status |
|----|-------|--------|
| 0.1 | Set up project workspace and repo structure | ✅ Done |
| 0.2 | Add Surveys nav entry in CareConnect (role-gated) | ⬜ Ready |
| 0.3 | Survey Administrator role provisioning check | ⬜ Ready |
| 0.4 | CI pipeline with lint, type check, build, tests | ⬜ Ready |
| 0.5 | E2E testing framework with first passing test | ⬜ Ready |

---

## Epic 01 — Survey Creation & Status Management

**Status:** 🔵 In Progress (partially ticketed in Jira)
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin

**Goal:** Administrators can create, configure, schedule, monitor, and close surveys across their full lifecycle — Draft, Scheduled, Live, Closed.

**Jira Epic Description:**
This epic establishes the foundational administrator workflow for the Survey Builder. Without it, no survey can be built, no survey can reach a family, and no survey can be retired. Administrators can create a draft survey, build it incrementally, validate it before publishing, schedule it for delivery, watch it transition to active status automatically, monitor it while collecting responses, and close it manually or by schedule.

**Story Groups:**
| Group | Description | Stories | Status |
|-------|-------------|---------|--------|
| A | Foundations — Likert label sets | 2 | ⬜ Ready |
| B | Drafting — create, edit, validate, save, discard | 5 | ⬜ Ready |
| C | Scheduling — one-time, closing date, audience | 3 | ⬜ Ready |
| D | Publishing & Lifecycle — publish, revert, auto-live, close, duplicate | 6 | ⬜ Ready |
| E | Visibility — list view, status at a glance | 2 | ⬜ Ready |
| F | Testing support — response seeder | 1 | ⬜ Ready |

**Total stories: 19**

**Key constraints from decisions:**
- Survey list screen: name, status badge, type, last sent, completion %
- Status badges: teal for Live, amber for Scheduled, gray for Draft and Closed
- Cross-creator restriction: only creator or Super Admin can edit
- Likert label sets are a shared admin-managed library

---

## Epic 02 — Sections, Questions & Branching

**Status:** 🔵 In Progress (partially ticketed in Jira)
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin

**Goal:** Administrators can build surveys with typed questions organized into sections, with conditional branching at the section level.

**Jira Epic Description:**
This epic delivers the survey authoring experience. An administrator can organize questions into sections, configure all six question types (Likert, Star Rating, Multiple Choice, Yes/No, Short Answer, Ranking), reorder everything via drag-and-drop, configure conditional logic that skips respondents to different sections based on their answers, and preview the full survey in a mobile frame before publishing.

**Story Groups:**
| Group | Description | Stories | Status |
|-------|-------------|---------|--------|
| — | Section data model and API | 1 | ⬜ Ready |
| — | Section UI in builder | 1 | ⬜ Ready |
| — | Question editor — shared controls | 1 | ⬜ Ready |
| — | Question editor — Likert (with customizable labels) | 1 | ⬜ Ready |
| — | Question editor — Multiple Choice | 1 | ⬜ Ready |
| — | Question editor — Yes/No | 1 | ⬜ Ready |
| — | Question editor — Short Answer | 1 | ⬜ Ready |
| — | Question editor — Ranking | 1 | ⬜ Ready |
| — | Question editor — Star Rating | 1 | ⬜ Ready |
| — | Preview mode (mobile frame) | 1 | ⬜ Ready |
| — | Branching data model and API | 1 | ⬜ Ready |
| — | Branching UI in question editor | 1 | ⬜ Ready |
| — | Branching engine (server-side path resolver) | 1 | ⬜ Ready |
| — | Preview mode with branching | 1 | ⬜ Ready |

**Total stories: ~14**

**Key constraints from decisions:**
- Every question must belong to a section (default auto-created)
- Branching is section-level only — no question-level branching at MVP
- Likert: 5 customizable labels per question, defaults pre-filled
- Star Rating: fixed 1–5, no customization
- Multiple Choice: supports single and multi-select, optional "Other" write-in
- Yes/No: optional custom label pair, optional "Other" write-in
- Ranking: minimum 2 items, drag-to-order
- Preview: mobile frame (iPhone-style), clearly labeled "Preview mode — responses not recorded"

---

## Epic 03 — Recurring & Event-Triggered Scheduling

**Status:** ⬜ Not Started
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin

**Goal:** Surveys send automatically on a repeating schedule or in response to a clinical event.

**Jira Epic Description:**
Today, every survey send requires manual action. For outcome measures and ongoing check-ins that need to happen consistently over time — weekly, monthly, quarterly — this creates operational burden and introduces gaps in data collection. This epic replaces that manual effort with a configurable, automated scheduling engine.

An administrator configures a schedule once — choosing a recurrence pattern (Google Calendar–style) or tying the survey to a clinical event (post-97156 session completion at MVP). From that point, the system handles all future sends, closes previous instances, and tracks completion across the lifecycle automatically.

**Story Groups:**
| Group | Description | Stories | Status |
|-------|-------------|---------|--------|
| O | Recurring schedule authoring | 3 | ⬜ Ready |
| P | Recurring instance lifecycle | 3 | ⬜ Ready |
| Q | Event-triggered scheduling (post-97156 only) | 3 | ⬜ Ready |
| R | Visibility and admin UX | 3 | ⬜ Ready |

**Total stories: ~12**

**Key constraints from decisions:**
- Recurring: Google Calendar–style RRULE patterns, plus custom interval fallback
- Market-based audience targeting required at MVP
- Manual one-off send supported
- When new instance opens, previous closes regardless of completion status
- Event trigger MVP scope: post-97156 only. Architecture must accommodate intake and auth expiration in Phase 2 without major rework.
- M5.4 (event trigger stories) are **blocked** pending architecture decision (Kerri + Timothy + Emily). M5.1–5.3, 5.5, 5.6 are unblocked.

---

## Epic 04 — Reminders & Notifications

**Status:** ⬜ Not Started
**Jira Epic:** [link]
**Repos:** survey-service, notification-service

**Goal:** Parents receive timely, non-intrusive reminders to complete surveys. Admins configure reminder cadence per survey.

**Jira Epic Description:**
A survey without reminders is a survey that gets forgotten. This epic delivers automated push notification reminders that nudge parents to complete open surveys, while respecting quiet hours and their personal notification preferences. Administrators configure the reminder cadence once per survey. Parents can override their personal preferences. The system stops reminding once a survey is complete.

**Story Groups:**
| Group | Description | Stories | Status |
|-------|-------------|---------|--------|
| — | Reminder cadence configuration | 2 | ⬜ Ready |
| — | Push notification dispatch | 2 | ⬜ Ready |
| — | Quiet hours enforcement | 2 | ⬜ Ready |
| — | Parent override | 1 | ⬜ Ready |
| — | Completion suppression | 1 | ⬜ Ready |

**Total stories: ~8**

**Key constraints from decisions:**
- Default cadence: every 2 days (admin can change)
- Quiet hours: 5pm–8pm parent local timezone (working assumption, pending clinical confirmation)
- Completion suppresses all remaining reminders for that instance
- Push notification only at MVP
- Parent can override personal notification preference

---

## Epic 05 — Gating

**Status:** ⬜ Not Started
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin, flutter-app

**Goal:** Super Admins can require parents to complete a survey before accessing certain app content.

**Jira Epic Description:**
Gating allows a Super Admin to designate a survey as a prerequisite for accessing the app. When a gating-active survey is pending, the main app content is blurred — the parent must complete the survey to proceed. Navigation to calendar, messages, and settings remains accessible. The gate lifts immediately upon completion.

**Story Groups:**
| Group | Description | Stories | Status |
|-------|-------------|---------|--------|
| — | Gating configuration (Super Admin only) | 2 | ⬜ Ready |
| — | Blur overlay UX (Flutter) | 2 | ⬜ Ready |
| — | Gate lift on completion | 1 | ⬜ Ready |
| — | Gating delay model (days after sending) | 1 | ⬜ Ready |

**Total stories: ~6**

**Key constraints from decisions:**
- Super Admin only — VP-level admins cannot manage gating
- Any survey can be gated — no pre-approved list
- Blur overlay (not full-screen takeover) — calendar, messages, settings remain accessible
- Gating model: "days after sending," default 0 = immediate gate
- Gate lifts immediately on completion

---

## Epic 06 — Reporting & Aggregation

**Status:** ⬜ Not Started
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin

**Goal:** Administrators can view survey results inside CareConnect: per-question aggregations, cross-instance trends, completion statistics.

**Key constraints from decisions:**
- CareConnect-native reporting — no PowerBI export at MVP
- Skipped questions (`was_skipped = true`) reported distinctly from unanswered
- Per-question results and cross-instance trends both required

---

## Epic 07 — Mobile App Integration (Flutter)

**Status:** ⬜ Not Started
**Owner:** Separate Flutter developer
**Repos:** flutter-family-app

**Goal:** Parents can receive, complete, and review surveys inside the Family Connect app.

**Dependencies:** API contract from epics 01–06 must be stable and documented before Flutter dev starts.

**Key constraints from decisions:**
- One question per screen, auto-advance on selection
- Branching invisible to parents
- Blur overlay for gating
- Closed surveys show "closed" state, not answerable
- Survey history: pagination or accordion (no unbounded scroll)
- Multi-language: English, Spanish, Arabic (Arabic = RTL, requires specific Flutter work)
