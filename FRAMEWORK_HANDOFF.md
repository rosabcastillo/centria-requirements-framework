# AI-Assisted Delivery Framework — Claude Code Handoff

> **How to start in Claude Code:**
> *"Read this file completely. Tell me what you understand about the framework and the survey builder project. Then wait for my instructions."*

---

## 1. What this is

Two parallel things are being built and documented here:

1. **A reusable AI-assisted delivery framework** — a lightweight, team-adoptable structure using Claude Code that BAs, PMs, QAs, and Devs can all use. Designed to be replicated across teams and projects.

2. **The Survey Builder project** — a specific product being built inside CareConnect. It is the first real implementation of this framework. Mid-way through Jira ticket creation, transitioning to Git-based requirements.

This document covers the **framework** in full. The survey builder project is documented separately in `docs/requirements/`.

---

## 2. The problem this framework solves

Current state across most teams:
- Specs live in Jira tickets — Claude Code cannot read Jira
- Every Claude Code session starts with zero context — the dev has to re-explain the project
- BAs write tickets, devs implement them, QAs test separately — no shared artifact that all three roles work from
- In a microservices architecture with 10+ repos, there's no single place to see which repos a feature touches
- Decisions made in meetings disappear — no durable, searchable record

The framework replaces Jira as the **spec source of truth** with markdown files in Git. Jira stays for status tracking and stakeholder visibility only. All requirements, decisions, and test plans live in a `requirements-repo` that Claude Code can read directly.

---

## 3. The hierarchy

```
Theme → Epic → Story
```

- **Theme** is the top planning unit (e.g., "patient-engagement," "provider-management")
- **Epic** is a feature slice within a theme (e.g., "survey-crud," "notifications")
- **Story** is a single user-facing capability within an epic

No "initiative" level. Theme is the highest level.

---

## 4. Canonical folder structure

```
requirements-repo/
  docs/
    decisions.md              # cross-theme architecture decisions
  CLAUDE.md                   # how Claude Code orients itself in this repo
  themes/
    [theme-name]/
      README.md               # theme goal, owning squad, key stakeholders
      ROADMAP.md              # epic-level status for THIS theme only
      repos.md                # all repos this theme touches (blast radius view)
      testing/
        strategy.md           # smoke + regression + e2e strategy, coverage targets
        e2e-scenarios.md      # scenario library, cross-epic, QA owns
        smoke-checklist.md    # fast gate, runs on every deploy, max 15 min
      epics/
        epic-01-[name]/
          README.md           # epic goal, DoD, jira epic link, story index
          stories/
            story-1.1-[name].md
            story-1.2-[name].md
        epic-02-[name]/
          README.md
          stories/
            story-2.1-[name].md
```

### Key placement rules — never violate these

- `repos.md` lives at **theme level only** — not epic level. It is the full blast radius view for the theme.
- `ROADMAP.md` lives at **theme level** — each theme has its own. No global roadmap.
- `testing/` lives at **theme level** — smoke/regression/e2e are cross-epic concerns.
- Epic README lives **inside** the epic folder — not as a sibling file alongside it.
- Stories declare their own repo(s) — `repos.md` is the rollup of all story declarations.

---

## 5. The repos.md file

In a microservices architecture, a single theme can touch 10+ repos simultaneously. The `repos.md` at theme level tracks this:

```markdown
## Repos involved in this theme

| Repo | Teams | Stories |
|------|-------|---------|
| survey-service | Team Alpha | 1.1, 1.2, 1.3 |
| auth-service | Team Beta | 1.3 |
| notification-service | Team Beta | 2.1, 2.2 |
| frontend-app | Team Gamma | 3.1, 3.2 |
| api-gateway | Platform | 1.1, 2.1 |
```

This file is derived from story declarations — each story file declares its own repo(s). `repos.md` is the rollup. A PM can open it and instantly see the full blast radius. It can eventually be auto-generated from story files.

---

## 6. Canonical story file format

```markdown
## Story [N.N] — [Title]

**Status:** ⬜ Ready | 🔵 In Progress (Name) | ✅ Done | 🚫 Blocked
**Jira:** [TICKET-ID]
**Repo(s):** [service-name] (comma-separated if cross-service)
**Epic:** [epic folder name]

### As a [user type]
### I want [capability]
### So that [outcome]

### Acceptance criteria
- Given... When... Then...
- Given... When... Then...

### Test plan
- Unit: ...
- E2E scenario: [scenario ID from testing/e2e-scenarios.md]
- Smoke impact: yes / no
- Regression impact: yes / no

### Claude Code briefing
> Paste this into Claude Code to start implementation:
> "Read CLAUDE.md, then implement story N.N. 
>  Story spec: [path to this file].
>  Touch only the files listed. All AC must pass before marking done."

### Notes / decisions made during implementation
(dev fills this in — becomes the audit trail)
```

---

## 7. The ROADMAP.md format (per theme)

```markdown
# Roadmap — [Theme Name]

| Epic | Status | Owner | Target |
|------|--------|-------|--------|
| epic-01-survey-crud | 🔵 In Progress | Team Alpha | Week 3 |
| epic-02-notifications | ⬜ Ready | Team Beta | Week 5 |
| epic-03-scheduling | ⬜ Ready | Team Alpha | Week 7 |

## Story status key
⬜ Ready  🔵 In Progress (Name)  ✅ Done  🚫 Blocked
```

---

## 8. How a developer picks their next story

1. Open `themes/[theme]/ROADMAP.md` — find next `⬜ Ready` story
2. Assign themselves in Jira → status = In Progress (collision guard)
3. Update the story file status to `🔵 In Progress (Name)`
4. Paste the Claude Code briefing from the story file into Claude Code
5. Implement, check off AC, update the notes section
6. Mark `✅ Done`, commit story file alongside code, open PR with Jira link

The story status in Git and the Jira assignment together prevent two developers picking the same story. The story file status is visible to Claude Code; the Jira status is visible to PMs and stakeholders.

---

## 9. Multi-repo setup — the CLAUDE.md bridge

Each service repo gets its own `CLAUDE.md` that points back to the requirements repo:

```markdown
# CLAUDE.md — [service-name]

## Requirements location
Stories for this service: ../requirements-repo/themes/[theme]/epics/

## Decisions log
../requirements-repo/docs/decisions.md

## Before starting any story
1. Check ROADMAP.md for your assigned story
2. Confirm status is 🔵 In Progress with your name
3. Read the full story file before writing any code
4. Read any referenced architecture docs

## After finishing
1. Update story.md to ✅ Done
2. Fill in the Notes section with implementation decisions
3. Open PR, link Jira ticket in description

## Tech stack
[Fill in per service — stack, test framework, API style, conventions]
```

Developers clone both repos side by side:

```
/workspace/
  requirements-repo/        ← BA/PM writes here
  survey-service/           ← CLAUDE.md points to ../requirements-repo/...
  auth-service/
  notification-service/
```

---

## 10. Who owns what

| Role | Owns |
|------|------|
| BA / PM | Theme README, ROADMAP, repos.md, Epic README, story files (AC + briefing) |
| QA | testing/strategy.md, testing/e2e-scenarios.md, testing/smoke-checklist.md |
| Dev | CLAUDE.md in each service repo, story status field, notes section after implementation |
| Everyone | Story test plan section (unit notes = dev, e2e links = QA, smoke/regression flags = BA+QA) |

---

## 11. Testing strategy (theme level)

Three files live in `themes/[name]/testing/`:

**`strategy.md`** — QA owns. Covers:
- Test pyramid targets (unit %, integration %, e2e %)
- What runs on every deploy (smoke)
- What runs on every PR (regression subset)
- What runs on release (full suite)
- Tooling decisions (Playwright, Vitest, etc.)
- Coverage targets per epic

**`e2e-scenarios.md`** — QA owns. The living library of end-to-end journeys that span multiple epics. Stories reference specific scenario IDs here. When a new story ships that adds a new journey, QA adds the scenario here.

**`smoke-checklist.md`** — QA owns. The fast gate that runs on every deploy. Never more than 15 minutes. A prioritized list of the most critical user actions that must work before anything else matters.

The story-level test plan is lightweight — it just declares:
- Unit test notes (what the dev should unit test)
- Links to relevant e2e scenario IDs
- Whether this story affects smoke (yes/no)
- Whether this story affects regression (yes/no)

---

## 12. Jira integration

**No official Jira MCP exists** in the registry. Three options:

**Option A — Jira REST API scripts (do this now)**
Add a `jira-helpers.sh` script to the requirements repo:
- `./jira-helpers.sh transition SURV-142 "In Progress"`
- `./jira-helpers.sh assign SURV-142 alex@company.com`
- `./jira-helpers.sh comment SURV-142 "Story file updated to In Progress"`

Claude Code can run bash scripts natively. API token stored in `.env` (gitignored). ~30 minutes of setup, works immediately.

**Option B — Switch to Linear (if team migrates)**
Linear MCP is already connected. Claude Code can natively assign issues, transition status, and create sub-issues. Zero scripts needed. Requires team migration decision.

**Option C — Custom MCP server (best long-term on Jira)**
Build a small Node/Python MCP server wrapping Jira REST API. Expose `transition_ticket()`, `assign_ticket()`, `add_comment()` as MCP tools. Configure via `.mcp.json` in each repo. Medium effort but frictionless for all teams permanently.

**Recommended sequence:** Option A this week → Option C when the team has bandwidth → Option B if migration ever happens.

---

## 13. The four Claude Code skills (to be built)

Skills are SKILL.md files that Claude Code reads automatically when triggered. They travel with the requirements repo — any team that clones the repo gets the skills.

| Skill file | Trigger phrase | Owner | What it does |
|-----------|----------------|-------|-------------|
| `skills/theme-setup/SKILL.md` | "set up a new theme" | BA/PM | Asks ~8 questions, scaffolds full theme folder structure with real content |
| `skills/epic-story-writer/SKILL.md` | "write stories for [epic]" | BA | Walks through story creation one by one, enforces INVEST, outputs story files |
| `skills/testing-strategy/SKILL.md` | "write testing strategy for [theme]" | QA | Reads existing epics, generates strategy.md + e2e-scenarios.md + smoke-checklist.md |
| `skills/dev-session-start/SKILL.md` | "start working on story N" or "what should I pick next" | Dev | Finds next Ready story, updates status, prints Claude Code briefing ready to paste |

**Status: Not yet built.** Building these is the next major output needed.

### What makes a good skill file

Each SKILL.md has three sections:
1. **Persona** — "You are acting as a senior BA writing user stories. Prioritize vertical slices, avoid technical implementation detail in AC, ensure each story is independently testable."
2. **Trigger and inputs** — what phrase triggers this skill, what questions to ask the user
3. **Output format** — exactly what files to create, in what structure, with what content

Skills also embed relevant checklists from BMAD (borrowed, not the whole framework):
- INVEST checklist for story quality
- PRD completeness checklist
- Decision record completeness checklist

---

## 14. What to borrow from BMAD

BMAD (https://github.com/bmad-code-org/BMAD-METHOD) has a multi-agent model that is too complex for broad adoption — BAs and QAs will not learn agent names and workflows. However, two things from BMAD are worth borrowing directly:

1. **Role-specific context injection** — embed a persona at the top of each skill file ("You are a senior BA..."). This is what BMAD does with agent personas but in a single file rather than a whole system.

2. **Checklists** — BMAD has good ready-made checklists for story quality (INVEST), PRD completeness, and architecture decision records. Lift these verbatim into skill files. They are just markdown.

Everything else in BMAD (orchestrator agents, separate config files, complex state management) is skipped. The value is captured; the complexity is not.

---

## 15. How to share this framework with other teams

**For teams using Claude Code:**
1. Clone the requirements repo template (once built)
2. Each service repo adds a `CLAUDE.md` pointing to the requirements repo
3. Skills are already there — they travel with the requirements repo

**For teams not yet on Claude Code:**
The same skill files work as plain prompts in claude.ai — they paste the trigger phrase. Same output, no tooling required. This is the adoption path for BAs and QAs who are not developers.

**The one-page README:**
The requirements repo root should have a README.md that explains the framework in two paragraphs. The CLAUDE.md and story template are the only two things people need to learn. Everything else is structure.

---

## 16. Immediate next steps

In priority order:

### Step 1 — Transition Survey Builder to the framework (do first)
The survey builder already has requirements written (in `docs/requirements/`). The transition maps these to the new structure:

```
Current                          →    New location
docs/requirements/01-PRD.md      →    themes/survey-builder/README.md
docs/requirements/02-decisions.md →   themes/survey-builder/ (+ docs/decisions.md)
docs/requirements/03-epic-index.md →  themes/survey-builder/ROADMAP.md
docs/requirements/04-user-stories.md → themes/survey-builder/epics/[epic]/stories/
docs/requirements/05-milestone-plan.md → themes/survey-builder/epics/[epic]/README.md
```

Tell Claude Code:
> *"Read this handoff file. I want to set up the requirements-repo structure for the survey builder theme. Create `themes/survey-builder/` with README, ROADMAP, repos.md, and testing/ stubs. Then create the epic folders for epics 00 through 03 with their README files. Use the content from docs/requirements/ to populate them. Ask me anything you need to fill in the gaps."*

### Step 2 — Import existing Jira tickets as story files
Tell Claude Code:
> *"I have existing Jira tickets for epics 01 and 02 that are partially written. Here are the ticket details: [paste Jira export or list of tickets]. Convert each ticket into a story file using the canonical story template in section 6 of this handoff file. Preserve the Jira ticket ID in each story's frontmatter. Place them in the correct epic folder."*

### Step 3 — Add jira-helpers.sh
Tell Claude Code:
> *"Create a jira-helpers.sh script in the requirements repo root. It should support three commands: transition [ticket-id] [status], assign [ticket-id] [email], comment [ticket-id] [message]. Use Jira REST API v3. Read the API token and base URL from a .env file. Add a .env.example with the required variable names."*

### Step 4 — Build the theme-setup skill
Tell Claude Code:
> *"Using the framework in this handoff file, create a SKILL.md file at skills/theme-setup/SKILL.md. It should ask ~8 questions and scaffold the full theme folder structure with real content. Follow the canonical folder structure in section 4 of this handoff. The skill should include a BA persona, INVEST checklist reference, and produce all required files."*

### Step 5 — Build remaining skills
Build `epic-story-writer`, `testing-strategy`, and `dev-session-start` in that order.

---

## 17. Anti-patterns — things explicitly decided against

Do not implement these, even if they seem reasonable:

- **Global ROADMAP at repo root** — roadmap lives inside each theme folder
- **repos.md at epic level** — theme level only
- **Testing strategy inside epic folders** — theme level only
- **Story files without a Claude Code briefing section** — this is the key unlock for devs
- **Multi-agent system (full BMAD)** — too complex for BA/QA adoption; use skills instead
- **Jira as the spec** — Jira is status only; spec lives in Git
- **Duplicating specs between Jira and Git** — Jira ticket description links to the story file path; the story file is the spec

---

## 18. CLAUDE.md for the requirements repo itself

When Claude Code is used inside the requirements repo (by a BA building story files or by the dev-session-start skill), it needs its own CLAUDE.md:

```markdown
# CLAUDE.md — requirements-repo

## What this repo is
This is the central requirements repository for [org name].
All product requirements, decisions, and test plans live here.
Service repos point to this repo for their specs.

## Structure
See FRAMEWORK_HANDOFF.md for the complete folder structure and rules.

## How to work here

### If you are a BA/PM
- To set up a new theme: say "set up a new theme called [name]"
- To write stories for an epic: say "write stories for [epic name]"
- Skills in skills/ will guide you through both

### If you are a QA
- To write a testing strategy: say "write testing strategy for [theme name]"
- The skill will read existing epics and generate all three testing files

### If you are a Dev
- To find your next story: say "what should I pick next"
- To start a story: say "start working on story [N.N]"
- The skill will update the status and give you the briefing to paste into your service repo

## Rules
- Never put roadmaps at the repo root — they belong in each theme folder
- Never put repos.md at epic level — theme level only
- Never create stories without a Claude Code briefing section
- Every story must declare its repo(s) in the frontmatter
```
