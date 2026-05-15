# Epic 02 — Sections, Questions & Branching

**Status:** 🔵 In Progress (partially ticketed in Jira)
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin
**Target:** Weeks 4–7

## Goal
Administrators can build surveys with typed questions organized into sections, with conditional branching at the section level.

## Definition of Done
- [ ] All 6 question types can be added, edited, deleted, and reordered
- [ ] Questions require a section (default section auto-created on survey creation)
- [ ] Sections can be created, renamed, reordered, and deleted (with orphan handling)
- [ ] Drag-and-drop reordering works for both questions and sections
- [ ] Section-level branching can be configured (skip to section or end survey)
- [ ] Preview mode renders all question types in a mobile frame
- [ ] Preview mode uses the branching engine
- [ ] Branching engine has full unit test coverage

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-2.1-section-data-model | Section data model and API | ⬜ Ready |
| story-2.2-section-ui | Section UI in builder | ⬜ Ready |
| story-2.3-question-shared-controls | Question editor — shared controls | ⬜ Ready |
| story-2.4-question-likert | Question editor — Likert (customizable labels) | ⬜ Ready |
| story-2.5-question-multiple-choice | Question editor — Multiple Choice | ⬜ Ready |
| story-2.6-question-yes-no | Question editor — Yes/No | ⬜ Ready |
| story-2.7-question-short-answer | Question editor — Short Answer | ⬜ Ready |
| story-2.8-question-ranking | Question editor — Ranking | ⬜ Ready |
| story-2.9-question-star-rating | Question editor — Star Rating | ⬜ Ready |
| story-2.10-preview-mode | Preview mode (mobile frame, no branching) | ⬜ Ready |
| story-2.11-confirmation-message | Default confirmation message stub | ⬜ Ready |
| story-2.12-branching-data-model | Branching data model and API | ⬜ Ready |
| story-2.13-branching-ui | Branching UI in question editor | ⬜ Ready |
| story-2.14-branching-engine | Branching engine (server-side path resolver) | ⬜ Ready |
| story-2.15-preview-with-branching | Preview mode with branching | ⬜ Ready |

## Key constraints
- section_id is NOT NULL on questions — no orphan questions ever
- Default section auto-created when survey is created
- Survey Builder Likert: 5 customizable labels per question — DIFFERENT from Feature 1 data collection Likert (fixed)
- Star Rating: fixed 1–5, no customization
- Branching: section-level only — no question-level branching at MVP
- Preview: clearly labeled "Preview mode — responses not recorded"
- Branching engine must handle multi-level nesting and back-navigation recalculation
- Open decision #2 (default confirmation message text) blocks story 2.11
