# CLAUDE.md — centria-requirements-framework

## What this repo is
Central requirements repository for the Centria AI Delivery COE.
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

## Rules — never violate these
- Roadmaps live inside each theme folder — never at repo root
- repos.md lives at theme level only — not epic level
- testing/ lives at theme level only — not inside epics
- Every story must have a Claude Code briefing section
- Every story must declare its repo(s) in the frontmatter
- Jira is for status tracking only — the story file is the spec
