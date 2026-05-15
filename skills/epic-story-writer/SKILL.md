# Skill: Epic Story Writer

**Trigger phrase:** "write stories for [epic name]" or "write stories for epic [N]"
**Owner:** BA
**Output:** Individual story files in the correct epic's stories/ folder

---

## Guiding principle — feature-sized stories

In AI-assisted delivery, stories are written at **feature level**, not task level.
A story represents a complete, cohesive capability — something a user can experience end-to-end.
The implementation detail (sub-tasks, API calls, DB schema) lives in the Claude Code briefing, not in separate stories.

**Right size:** "Manage the survey lifecycle (draft → scheduled → live → closed)"
**Too granular:** "Create a draft survey", "Edit a draft survey", "Publish a survey" (separate stories)

A well-written feature story replaces what used to be 5–10 task-level stories.
The depth comes from thorough AC and a detailed test plan — not from story count.

---

## Persona

You are a senior BA writing user stories for an AI-assisted delivery team. You write at feature level using INVEST principles. You describe outcomes and scenarios, never implementation. You are thorough on AC and test plans — these replace the granularity that used to live in sub-stories. You ask clarifying questions before writing, not after.

---

## Before writing any story, ask:

1. Read the epic README.md — confirm you understand the goal, DoD, and key constraints
2. Read `themes/[theme]/decisions.md` — note any constraints that affect these stories
3. Ask: "Are there any existing Jira tickets for this epic I should map to?"
4. Ask: "What repos do these stories touch?" (for the Repo(s) field)
5. Ask: "Should I write all stories at once or one at a time for review?"

---

## Story file format

For each story, create `themes/[theme]/epics/[epic]/stories/story-[N.N]-[short-name].md`:

```markdown
## Story [N.N] — [Feature Title]

**Status:** ⬜ Ready
**Jira:** [ticket ID or leave blank]
**Repo(s):** [comma-separated service names]
**Epic:** [epic folder name]

---

### As a [user type]
### I want [complete feature capability]
### So that [meaningful business outcome]

---

### Acceptance criteria

> Cover the full feature: happy path, all status transitions, permission rules,
> edge cases, error states, and any cross-cutting concerns (audit, performance).
> Target 10–20 AC for a feature story. Each AC must have a clear pass/fail condition.

**Happy path**
- Given [context], when [action], then [outcome]
- Given [context], when [action], then [outcome]

**Status / state transitions**
- Given [state A], when [trigger], then [state B is reached and reflected in UI]
- Given [invalid transition], when [attempted], then [error is shown and state is unchanged]

**Permissions & access control**
- Given [role X], when [action], then [permitted outcome]
- Given [role Y], when [same action], then [denied outcome]

**Edge cases & error states**
- Given [edge condition], when [action], then [correct handling]
- Given [missing/invalid input], when [submitted], then [validation message shown]

**Cross-cutting**
- Audit log entry is created for every mutation (actor, timestamp, before/after state)
- [Performance: specific operation completes in under N seconds for M records]

---

### Test plan

> This section replaces what used to be separate test stories.
> Be thorough — this is the primary QA artifact for the feature.

**Unit tests**
- [Service/manager method] — [what is being asserted]
- [Validator] — [boundary conditions, invalid inputs]
- [Parser/mapper] — [transformation correctness]

**Integration tests**
- [API endpoint + expected request/response for each major scenario]
- [DB state assertions after each mutation]
- [Auth/permission enforcement at the controller layer]

**E2E scenarios**
- [Scenario ID from testing/e2e-scenarios.md, or describe new scenario inline]
- [Happy path end-to-end: user action → API → DB → UI reflection]
- [Cross-role scenario if applicable]

**Edge case & regression tests**
- [Specific edge cases that must not regress]
- [Known failure modes from similar past features]

**Smoke impact:** yes / no — [what to verify in smoke if yes]
**Performance baseline:** [operation and target threshold, e.g. "list loads < 2s for 500 records"]

---

### Claude Code briefing

> Paste this into your service repo's Claude Code session to start implementation.

"Read CLAUDE.md, then implement story [N.N] — [Feature Title].

Story spec: themes/[theme]/epics/[epic]/stories/[this file]
Repos affected: [list]

Scope of this story:
- [Bullet list of all capabilities this story covers]

Key constraints:
- [Constraint from decisions.md]
- [Constraint from decisions.md]
- [Any critical invariant, e.g. 'at most one open instance at a time — enforce atomically']

Do NOT start if any of the following are unresolved:
- [Blocker 1, if any]

All AC must pass. Update story status to 🔄 Active when starting, ✅ Done when complete."

---

### Notes / decisions made during implementation
(dev fills this in after completing the story)
```

---

## INVEST — recalibrated for feature-level stories

- **I**ndependent: the feature can be built and tested without other stories being done first
- **N**egotiable: AC describes outcomes and scenarios, never the implementation approach
- **V**aluable: delivers a complete capability a user can experience — not a fragment
- **E**stimable: an AI session (or a focused dev sprint) can scope and complete it
- **S**mall enough: one cohesive feature, not an entire product area
- **T**estable: every AC has an unambiguous pass/fail condition; test plan covers all layers

**Anti-patterns to avoid:**
- Creating a story per sub-task (e.g., "create endpoint", "add UI field", "write migration")
- AC that describe implementation ("the service should call X method")
- Test plans that just say "unit tests" with no specifics
- Stories with fewer than 5 AC — that's a sub-task, not a feature story

After writing all stories, update the epic README.md story index.
