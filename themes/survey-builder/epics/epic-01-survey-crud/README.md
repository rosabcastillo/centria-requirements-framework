# Epic 01 — Survey Creation & Status Management

**Status:** 🔵 In Progress (partially ticketed in Jira)
**Jira Epic:** [link]
**Repos:** survey-service, careconnect-admin
**Target:** Weeks 2–3

## Goal
Administrators can create, configure, schedule, monitor, and close surveys across their full lifecycle: Draft → Scheduled → Live → Closed.

## Definition of Done
- [ ] Admin can create a draft survey with title and description
- [ ] All 6 status transitions work and are reflected in the UI
- [ ] Audit trail records every status change with actor and timestamp
- [ ] Cross-creator restriction enforced (only creator or Super Admin can edit)
- [ ] Survey list shows name, status badge, type, last sent, completion %
- [ ] Survey can be duplicated from any status
- [ ] Response seeder works for test environments

## Story index

| Story | Title | Status |
|-------|-------|--------|
| story-1.1-manage-likert-label-library | Manage the Likert label set library | ⬜ Ready |
| story-1.2-default-label-set | Default label set pre-loaded | ⬜ Ready |
| story-1.3-create-survey-draft | Create a new survey draft | ⬜ Ready |
| story-1.4-edit-draft-survey | Edit a draft survey | ⬜ Ready |
| story-1.5-validation-before-publish | See what's missing before I can publish | ⬜ Ready |
| story-1.6-save-work-explicitly | Save my work explicitly | ⬜ Ready |
| story-1.7-discard-draft | Discard a draft | ⬜ Ready |
| story-1.8-configure-one-time-schedule | Configure a one-time schedule | ⬜ Ready |
| story-1.9-set-closing-date | Set a closing date | ⬜ Ready |
| story-1.10-define-survey-audience | Define the survey audience | ⬜ Ready |
| story-1.11-publish-survey | Publish a survey | ⬜ Ready |
| story-1.12-revert-to-draft | Move a scheduled survey back to draft | ⬜ Ready |
| story-1.13-survey-goes-live-automatically | Survey goes live automatically | ⬜ Ready |
| story-1.14-close-live-survey-manually | Close a live survey manually | ⬜ Ready |
| story-1.15-survey-closes-automatically | Survey closes automatically | ⬜ Ready |
| story-1.16-duplicate-survey | Duplicate a survey | ⬜ Ready |
| story-1.17-see-all-surveys | See all surveys in a list | ⬜ Ready |
| story-1.18-recurring-status-at-glance | Understand status at a glance for recurring surveys | ⬜ Ready |
| story-1.19-response-seeder | Simulate parent responses for testing | ⬜ Ready |

## Key constraints
- Status enum: draft / scheduled / live / closed — enforced at DB level
- Status badge colors: teal = Live, amber = Scheduled, gray = Draft and Closed
- Cross-creator restriction: only creator or Super Admin can edit; other VP = read-only
- Audit logging: use existing helper service — never inline
- Open decision #4 (live survey edit behavior) must be confirmed before data model is finalized
- Survey list must load in under 2 seconds for up to 500 surveys
