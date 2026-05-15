# Epic 06 — Reporting & Aggregation

**Status:** ⬜ Ready
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin
**Target:** Weeks 14–15

## Goal
Administrators can view survey results inside CareConnect: per-question aggregations, cross-instance trends, completion statistics.

## Definition of Done
- [ ] Per-question result distribution visible for any closed or live survey
- [ ] Skipped responses shown separately from answered responses
- [ ] Cross-instance trend view for recurring surveys
- [ ] Completion statistics per instance (sent, completed, %, avg time)
- [ ] No PowerBI export — CareConnect-native only

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-6.1-response-storage | Response data model and storage | ⬜ Ready |
| story-6.2-per-question-aggregation | Per-question result aggregation | ⬜ Ready |
| story-6.3-cross-instance-trends | Cross-instance trend view | ⬜ Ready |
| story-6.4-completion-statistics | Completion statistics per instance | ⬜ Ready |

## Key constraints
- was_skipped = true is DISTINCT from null/unanswered — reporting must distinguish them
- CareConnect-native reporting only — no PowerBI export at MVP
- Responses immutable once submitted
