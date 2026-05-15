# E2E Scenarios — Survey Builder

**Owner:** QA
**Format:** E2E-[epic number]-[sequence]
**Tools:** Playwright

Stories reference scenario IDs from this file. When a new story ships that adds a new journey, QA adds the scenario here.

---

## E2E-01 — Survey Lifecycle (full admin journey)

### E2E-01-01: Create, publish, and close a one-time survey
**Stories covered:** B1, C1, D1, D4
**Steps:**
1. Log in as VP-level admin
2. Click "Create Survey"
3. Add title "Q2 Parent Satisfaction"
4. Add one Likert question
5. Set one-time schedule 2 minutes in the future, select a market
6. Click Publish → confirm status = Scheduled
7. Wait for send time → confirm status = Live
8. Click "Close Survey" → confirm status = Closed
**Expected:** Status transitions correct, audit trail has entries for each transition

### E2E-01-02: Cross-creator read-only enforcement
**Stories covered:** B1, B2
**Steps:**
1. Log in as Admin A, create a survey
2. Log in as Admin B (different VP-level user)
3. Navigate to Admin A's survey
4. Verify edit controls are disabled
5. Verify "View only" indicator is present
**Expected:** Admin B cannot edit Admin A's survey

### E2E-01-03: Duplicate and republish a closed survey
**Stories covered:** D6, D1
**Steps:**
1. Find a Closed survey
2. Click Duplicate
3. Verify new draft created with "Copy of" prefix, no audience, no send date
4. Set audience and schedule on duplicate
5. Publish duplicate
**Expected:** Duplicate is independent, original responses not included

---

## E2E-02 — Question Authoring

### E2E-02-01: Build a survey with all 6 question types
**Stories covered:** 2.4–2.9
**Steps:**
1. Create a new survey
2. Add one question of each type (Likert, Star Rating, Multiple Choice, Yes/No, Short Answer, Ranking)
3. Save and open preview mode
4. Navigate through all questions in preview
**Expected:** All question types render correctly in preview, "Preview mode — responses not recorded" banner visible

---

## E2E-03 — Scheduling

### E2E-03-01: Configure and observe a recurring weekly survey
**Stories covered:** O1, O2, P1
**Steps:**
1. Create a survey with a recurring weekly (Monday) schedule
2. Confirm "next 5 dates" preview shows correct Mondays
3. (With mocked clock) advance to Monday — confirm new instance created and previous closed
**Expected:** Instance lifecycle correct, previous instance closed regardless of completion

---

## E2E-04 — Gating (stub)
*To be written when Epic 05 stories are detailed*

---

## E2E-05 — Reporting (stub)
*To be written when Epic 06 stories are detailed*
