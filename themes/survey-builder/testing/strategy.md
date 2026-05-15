# Testing Strategy — Survey Builder

**Owner:** QA
**Status:** 🔵 In Progress — stub, to be completed with QA team

---

## Test pyramid targets

| Layer | Target | Notes |
|-------|--------|-------|
| Unit | 70% | Business logic in Manager layer, branching engine, validators |
| Integration | 20% | Repository layer, API contracts |
| E2E | 10% | Critical user journeys only — see e2e-scenarios.md |

---

## What runs when

| Trigger | Suite | Max time |
|---------|-------|----------|
| Every PR | Unit + integration tests, ESLint, TypeScript check | 10 min |
| Every deploy (beta/QA) | Smoke checklist | 15 min |
| Release (UAT → prod) | Full regression + smoke | 60 min |

---

## Tooling

| Layer | Tool |
|-------|------|
| Backend unit + integration | MSTest + Moq (.NET) |
| Frontend unit | Jest + React Testing Library |
| E2E | Playwright |
| API contract | To be decided |

---

## Coverage targets per epic

| Epic | Priority areas |
|------|----------------|
| epic-00-foundation | Role-gating middleware (VP sees nav, DCS gets 403) |
| epic-01-survey-crud | Status transitions, cross-creator restriction, audit log entries |
| epic-02-sections-questions | All 6 question types, section_id NOT NULL enforcement, branching engine path resolution |
| epic-03-scheduling | RRULE generation, instance lifecycle (previous closes on new open), mocked-clock tests for recurring |
| epic-04-reminders | Quiet hours enforcement, completion suppression |
| epic-05-gating | Super Admin only, blur overlay trigger, gate lift on completion |
| epic-06-reporting | Skipped vs. unanswered distinction, aggregation accuracy |

---

## Compliance notes
- All survey response data is HIPAA-sensitive — no real patient data in test environments
- Audit trail tests must verify entries exist and contain required fields (actor, timestamp, action)
- See data-setup.md for test persona definitions
