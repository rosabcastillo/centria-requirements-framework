# Claude Code Handoff — Survey Builder

> **How to use this file in Claude Code:**
> Open Claude Code in your project repo and say:
> *"Read FRAMEWORK_HANDOFF.md first, then read CLAUDE_CODE_HANDOFF.md and the files in /docs/requirements/ in order. Tell me what you understand about both the framework and the survey builder project, then wait for my instructions."*
>
> **Two documents to read:**
> - `FRAMEWORK_HANDOFF.md` — the reusable delivery framework this project is being transitioned into
> - This file — the survey builder project specifics

---

## 1. About this project

**What:** Survey Builder — a self-service feature inside CareConnect that lets administrators create, schedule, and distribute surveys to families. Captures structured parent-reported outcome data for payer reporting and clinical accountability.

**Part of:** Family Connect App Phase 2 (alongside Parent Data Collection and Monthly Progress Summary — those are separate workstreams).

**Why:** Parent-reported outcome data is the #1 gap in payer meetings. No systematic way currently exists to trend parent satisfaction or engagement.

---

## 2. Team and scope

- **1 developer** (new to Claude Code — stories must be detailed and self-contained)
- **Your scope:** Backend + CareConnect admin UI
- **Not your scope:** Flutter parent app (separate developer, starts after API contract is stable)
- **PM/BA:** Driving requirements, writes story files
- **QA:** Owns testing strategy and e2e scenarios

---

## 3. Status right now

| Area | Status |
|------|--------|
| Milestone 0 — Foundation | 🔵 In Progress |
| Milestone 1 — Survey CRUD | 🔵 Partially ticketed in Jira, transitioning to Git |
| Milestone 2 — Question authoring | 🔵 Partially ticketed in Jira, transitioning to Git |
| Milestones 3–8 | ⬜ Not started |
| User stories — Epic 01 (Survey lifecycle) | ✅ Fully written |
| User stories — Epic 03 (Scheduling) | ✅ Fully written |
| User stories — Epics 04–06 | ⬜ Planned, not yet detailed |

---

## 4. Reference documents in this repo

Read these in order when starting a session:

| File | What it contains |
|------|-----------------|
| `docs/requirements/01-PRD-v1.1.md` | Full product requirements, scope, users, constraints |
| `docs/requirements/02-decisions-log.md` | All resolved decisions + open decisions with owners |
| `docs/requirements/03-epic-index.md` | All epics, story counts, constraints per epic |
| `docs/requirements/04-user-stories.md` | All user stories in INVEST format with AC |
| `docs/requirements/05-milestone-plan-dev-reference.md` | Technical milestone plan with Claude Code briefings |
| `docs/architecture/auth-roles.md` | Existing CareConnect role system (write this in M0.3) |
| `docs/architecture/data-model.md` | Survey data model |
| `docs/api/openapi.yaml` | API contract (generate and maintain each milestone) |

---

## 5. How to work on a story

1. Find your assigned story in the ROADMAP or epic index
2. Read the full story file — AC, test plan, Claude Code briefing
3. Read any referenced architecture docs
4. Implement, checking off AC as you go
5. Update the story status to ✅ Done
6. Fill in the Notes section with any implementation decisions
7. Commit story file alongside code
8. Open PR with Jira ticket ID in the description

---

## 6. Decisions you must know before writing code

### Hard rules — never violate these
- **Audit logging:** Always use the existing audit log helper service. Never write audit rows inline.
- **Survey Builder Likert ≠ Feature 1 Likert.** Survey Builder Likert has 5 customizable labels per question. Feature 1 data collection Likert uses fixed templates. These are different.
- **section_id is NOT NULL on questions.** Every question must belong to a section. A default section is auto-created when a new survey is created.
- **Gating UI = blur overlay, not full-screen takeover.** Calendar, messages, settings remain accessible.
- **Auto-advance = no Proceed button.** Selecting an answer advances the screen automatically.
- **Do not start M5.4 (event trigger handler).** Blocked pending architecture decision. M5.1–5.3, 5.5–5.7 are unblocked.
- **Cross-creator restriction:** Only the creator or Super Admin can edit. Other VP-level users are read-only.

### Key decisions for data model
- Status enum: draft / scheduled / live / closed
- Skipped questions: `was_skipped = true` — distinct from null/unanswered
- Recurring instance behavior: new instance opening closes previous instance regardless of completion
- Market-based audience targeting required — survey has a market_id
- Survey history: must use pagination or accordion — never unbounded scroll

### Open decisions (check before touching these areas)
| # | Topic | Blocks |
|---|-------|--------|
| 1 | Final quiet hours | M6 notification timing |
| 2 | Default confirmation message text | M3.2 |
| 3 | Audit trail retention period | M8 |
| 4 | Live survey edit behavior | M1 data model (versioning) |
| 5 | Event trigger architecture | M5.4 only |
| 6 | Survey history UI pattern | Flutter app |

---

## 7. Jira ticket mapping

When transitioning existing Jira tickets to story files, record the Jira ID in the story frontmatter:

```
**Jira:** SURV-142
```

When opening a PR, include the Jira ID in the PR description so the ticket auto-links.

---

## 8. Anti-patterns — things that have been explicitly decided against

Do not implement these, even if they seem reasonable:

- Full-screen survey takeover for gating (decided: blur overlay)
- "Proceed" button after answering a question (decided: auto-advance)
- Unbounded scroll for survey history (decided: pagination or accordion)
- Inline audit log writes (decided: use helper service)
- Batch multi-market scheduling UI (decided: handle via instance duplication)
- File attachments as question type (out of scope MVP)
- Question-level branching (decided: section-level only)
- PowerBI integration (decided: CareConnect-native reporting only)

---

## 9. Milestone 0 checklist (if starting fresh)

- [ ] Repo created, folder structure matches /docs/requirements/05-milestone-plan-dev-reference.md
- [ ] Surveys nav entry visible to VP+ only, hidden/403 for DCS/OD
- [ ] Auth roles documented in /docs/architecture/auth-roles.md
- [ ] CI pipeline: lint, type check, build, tests on every push
- [ ] Playwright E2E framework installed with first two tests (VP sees nav, DCS gets 403)
