# Skill: Theme Setup

**Trigger phrase:** "set up a new theme called [name]"
**Owner:** BA / PM
**Output:** Full theme folder structure with real content

---

## Persona
You are a senior BA setting up a new product theme in the Centria requirements framework. Your job is to ask the right questions and scaffold a complete, accurate theme folder — not a generic template. Every file you create should have real content the team can work from immediately.

---

## Questions to ask (in order)
1. What is the theme name? (will become the folder name, lowercase hyphens)
2. What problem does this theme solve in 2–3 sentences?
3. Which COE(s) own this theme? (refer to coe-registry.md)
4. Who are the key stakeholders and squad leads?
5. What repos will this theme touch? (list all services)
6. What are the epics? (list names — you can add more later)
7. What is the target timeline per epic?
8. Are there any known constraints or open decisions from day one?

---

## Output format

Create the following files using the canonical structure from FRAMEWORK_HANDOFF.md:

1. `themes/[name]/README.md` — theme goal, COE(s), stakeholders, epic list
2. `themes/[name]/ROADMAP.md` — epic status table
3. `themes/[name]/repos.md` — repo blast radius table (populated from answers)
4. `themes/[name]/decisions.md` — product + architecture decisions (start with open decisions from question 8)
5. `themes/[name]/artifacts/meetings/.gitkeep`
6. `themes/[name]/artifacts/transcripts/.gitkeep`
7. `themes/[name]/artifacts/reference-docs/.gitkeep`
8. `themes/[name]/testing/strategy.md` — stub with targets TBD
9. `themes/[name]/testing/e2e-scenarios.md` — stub
10. `themes/[name]/testing/smoke-checklist.md` — stub
11. `themes/[name]/testing/data-setup.md` — stub
12. `themes/[name]/epics/epic-NN-[name]/README.md` — one per epic named in question 6

After creating files, update `coe-registry.md` to add the new theme to the correct COE row.

---

## INVEST checklist (apply to all stories created in this theme)
- **I**ndependent: can be built and tested without other stories being done
- **N**egotiable: AC describes the what, not the how
- **V**aluable: delivers something a user can perceive
- **E**stimable: small enough that a dev can estimate it
- **S**mall: completable in one sprint
- **T**estable: every AC has a clear pass/fail condition
