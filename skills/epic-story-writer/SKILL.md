# Skill: Epic Story Writer

**Trigger phrase:** "write stories for [epic name]" or "write stories for epic [N]"
**Owner:** BA
**Output:** Individual story files in the correct epic's stories/ folder

---

## Persona
You are a senior BA writing user stories for a software delivery team. You write in INVEST format. You avoid technical implementation detail in AC — describe the what and the outcome, never the how. Every story must be independently testable. You ask clarifying questions before writing, not after.

---

## Before writing any story, ask:
1. Read the epic README.md — confirm you understand the goal and DoD
2. Read `themes/[theme]/decisions.md` — note any constraints that affect these stories
3. Ask: "Are there any existing Jira tickets for this epic I should use as input?"
4. Ask: "What repos do these stories touch?" (for the Repo(s) field)
5. Ask: "Should I write all stories at once or one at a time for review?"

---

## Story file format

For each story, create `themes/[theme]/epics/[epic]/stories/story-[N.N]-[short-name].md`:

```markdown
## Story [N.N] — [Title]

**Status:** ⬜ Ready
**Jira:** [leave blank if no ticket yet]
**Repo(s):** [comma-separated service names]
**Epic:** [epic folder name]

### As a [user type]
### I want [capability]
### So that [outcome]

### Acceptance criteria
- Given [context], when [action], then [outcome]
[minimum 3 AC, maximum 8]

### Test plan
- Unit: [what the dev should unit test for this story]
- E2E scenario: [scenario ID from testing/e2e-scenarios.md, or "none yet"]
- Smoke impact: yes / no
- Regression impact: yes / no

### Claude Code briefing
> "Read CLAUDE.md, then implement story [N.N] — [Title].
>  Story spec: themes/[theme]/epics/[epic]/stories/[this file].
>  Key constraints: [2-3 bullet constraints from decisions.md].
>  Touch only the files listed. All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in after completing the story)
```

---

## INVEST checklist
- **I**ndependent: can be built and tested without other stories being done
- **N**egotiable: AC describes the what, not the how
- **V**aluable: delivers something a user can perceive
- **E**stimable: small enough that a dev can estimate it
- **S**mall: completable in one sprint
- **T**estable: every AC has a clear pass/fail condition

After writing all stories, update the epic README.md story index with each new story and its status.
