# Theme: Survey Builder

**COE:** Operations — Field, Clinical & Client
**COE Lead:** Rosa Batista (Client Engagement)
**Squad:** TBD (1 developer assigned)
**Product Manager:** Emily Rueber
**Designer:** Rosa Batista
**BA:** Kerri Milyko
**Approvers:** Timothy Yeager, Kerri Milyko
**Part of:** Family Connect App Phase 2 (alongside Parent Data Collection and Monthly Progress Summary — separate workstreams)

---

## Goal
Enable survey administrators to build, schedule, and distribute surveys to families without engineering support. Capture structured parent-reported outcome data to support payer reporting, measurement-based care, and organizational accountability.

**The problem:** Parent-reported outcome data is the #1 gap in payer meetings. No systematic way currently exists to trend parent satisfaction or engagement. Every survey send today requires manual intervention.

---

## Users

| Role | Access |
|------|--------|
| Survey Administrator (VP-level) | Create, edit, publish, schedule, close surveys. View results. |
| Super Admin (IT-granted) | All admin capabilities + gating management |
| Parent / Respondent | Receives and completes surveys in Family Connect app (Flutter, separate dev) |
| Clinical Staff (SC/BT) | Not direct users — their clinical actions can trigger event-based survey sends |
| DCS / OD | **No access** — not even read-only |

---

## Epic index

| Epic | Name | Status | Owner | Target |
|------|------|--------|-------|--------|
| epic-00-foundation | Foundation & Scaffolding | 🔵 In Progress | Dev | Week 1 |
| epic-01-survey-crud | Survey Creation & Status Management | 🔵 In Progress | Dev | Weeks 2–3 |
| epic-02-sections-questions-branching | Sections, Questions & Branching | ⬜ Ready | Dev | Weeks 4–7 |
| epic-03-scheduling | Recurring & Event-Triggered Scheduling | ⬜ Ready | Dev | Weeks 8–9 |
| epic-04-reminders-notifications | Reminders & Notifications | ⬜ Ready | Dev | Weeks 10–11 |
| epic-05-gating | Survey Gating | ⬜ Ready | Dev | Weeks 12–13 |
| epic-06-reporting | Reporting & Aggregation | ⬜ Ready | Dev | Weeks 14–15 |
| epic-07-mobile-integration | Flutter Respondent App | ⬜ Ready | Flutter Dev | After API contract stable |

---

## Scope

**In:** Survey creation (6 question types), sections, section-level branching, scheduling (one-time, recurring, event-triggered), reminders, gating, CareConnect-native reporting, audit logging.

**Out (MVP):** DCS/OD access, multi-editor, image/video in questions, file upload responses, question-level branching, AI-assisted question generation, PowerBI export, multi-language admin UI, approval workflow, multi-market batch scheduling, event triggers beyond post-97156.

---

## Non-functional requirements
- HIPAA compliance for all survey response data
- Audit trail for all admin mutations
- Performance: survey list loads under 2 seconds for up to 500 surveys
- Accessibility: WCAG 2.1 AA on CareConnect admin UI

---

## Repos touched

See [repos.md](repos.md) for the full blast radius.

---

## Key constraints (see decisions.md for full log)
- Audit logging: always use existing helper service — never inline
- Survey Builder Likert ≠ Feature 1 Likert (customizable vs. fixed)
- Every question must belong to a section (section_id NOT NULL)
- Gating UI = blur overlay, not full-screen takeover
- Auto-advance = no Proceed button
- Do NOT start M5.4 (event trigger) — blocked pending architecture decision
- Cross-creator restriction: only creator or Super Admin can edit
