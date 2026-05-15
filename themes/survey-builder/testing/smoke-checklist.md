# Smoke Checklist — Survey Builder

**Owner:** QA
**Target:** Completes in under 15 minutes
**Runs on:** Every deploy to beta and QA environments

---

## Checklist (run in order)

| # | Check | Role | Pass condition |
|---|-------|------|----------------|
| 1 | VP-level admin can see Surveys in nav | Admin | Nav entry visible |
| 2 | DCS user cannot access /surveys | DCS | 403 returned |
| 3 | Create a new survey draft | Admin | Survey appears in list with status "Draft" |
| 4 | Add a Likert question to the draft | Admin | Question saved and visible in builder |
| 5 | Publish the survey (one-time, future date) | Admin | Status changes to "Scheduled" |
| 6 | Survey list loads in under 2 seconds | Admin | Performance check |
| 7 | Non-creator VP admin sees survey as read-only | Other Admin | Edit controls disabled |
| 8 | Duplicate a survey | Admin | "Copy of" draft created, no audience/date |
| 9 | Audit trail shows publish event | Admin | Entry visible with actor + timestamp |
| 10 | Close a live survey | Admin | Status changes to "Closed" |

**If only 5 minutes available, run items: 1, 2, 3, 5, 6**
