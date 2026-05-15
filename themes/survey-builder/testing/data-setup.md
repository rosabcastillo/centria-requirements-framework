# Test Data Setup — Survey Builder

**QA owns:** What test data is needed (personas, states, edge cases)
**Dev owns:** How to create it (seeders, factories, fixtures)
**Location of seeder code:** survey-service/src/seeders/ (to be created in Epic 00)

---

## Test personas

| Persona | Role | Market | Notes |
|---------|------|--------|-------|
| Admin A | VP-level (Survey Administrator) | Market 01 — Chicago | Primary creator in cross-creator tests |
| Admin B | VP-level (Survey Administrator) | Market 01 — Chicago | Secondary admin — must see Admin A's surveys as read-only |
| Super Admin | Super Admin (IT-granted) | All markets | Can manage gating, can edit any survey |
| DCS User | DCS | Market 01 | Must be blocked from /surveys entirely |
| Parent 01 | Respondent | Market 01 | Active family, English-speaking |
| Parent 02 | Respondent | Market 01 | Active family, Spanish-speaking |
| Parent 03 | Respondent | Market 02 — Dallas | Used for market targeting tests |

---

## Required base data per epic

### Epic 00 — Foundation
- All 4 test personas provisioned in test environment
- /surveys route exists and returns 200 for VP+, 403 for DCS

### Epic 01 — Survey CRUD
- At least 1 survey in each status: Draft, Scheduled, Live, Closed
- At least 2 admins (Admin A and Admin B) with surveys to test cross-creator restriction
- Default Likert label set pre-seeded

### Epic 02 — Questions
- 1 survey with all 6 question types configured
- 1 survey with sections and questions in each section
- 1 branching survey with at least 2 section-level rules

### Epic 03 — Scheduling
- Mocked clock infrastructure available for recurring instance tests
- 1 recurring survey with at least 3 historical instances

### Epic 04 — Reminders
- Parent personas with timezone data set (for quiet hours tests)
- 1 survey with reminders enabled, 1 with reminders disabled

### Epic 05 — Gating
- 1 gating-enabled survey with delay = 0 (immediate)
- 1 gating-enabled survey with delay = 3 days

### Epic 06 — Reporting
- Seeded responses for at least 2 completed survey instances
- Include responses with was_skipped = true to test skipped vs. unanswered distinction

---

## Data cleanup strategy
- Test environments reset every Sunday at 2am
- Seeders are idempotent — safe to re-run
- Never use production data in test environments
- Seeder entrypoint: `dotnet run --project src/Centria.Survey.DbUp -- "<conn>" "Test"`
