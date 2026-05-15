# Cross-Theme Architecture Decisions

Decisions that apply to all themes and teams. Theme-specific decisions live in `themes/[name]/decisions.md`.

---

## Resolved

### 2026-04 — Audit logging via existing helper service
**Decided:** All mutations across all services use the existing audit log helper service. No inline audit log writes anywhere.
**Decided by:** PM / Engineering
**Why:** Consistency, single point of control, compliance auditability.
**Applies to:** All themes that write mutations.

### 2026-04 — CareConnect role system is the auth source of truth
**Decided:** No new role types created. Reuse existing CareConnect role and user-based permission system across all features.
**Decided by:** Pawanjit, PM
**Why:** CC already has a well-defined permission system. New roles create redundancy and migration overhead.

### 2026-04 — Reporting surface: CareConnect-native, no PowerBI
**Decided:** Results and aggregations live inside CareConnect. PowerBI export deferred.
**Decided by:** PM + Pawanjit
**Why:** Reduces external dependency. CareConnect is where clinical staff already work.

### 2026-05 — Requirements live in Git, not Jira
**Decided:** All specs, decisions, and test plans live in markdown files in the requirements repo. Jira is for status tracking and stakeholder visibility only. Jira ticket descriptions link to the story file path.
**Decided by:** Rosa (BA/PM)
**Why:** Claude Code cannot read Jira. Every session starting from zero is unsustainable at scale.

---

## Open

| # | Decision | Owner | Blocks |
|---|----------|-------|--------|
| — | Date/time library standard across all frontend packages | Engineering | Any feature with scheduling UI |
