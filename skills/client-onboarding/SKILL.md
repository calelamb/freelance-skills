---
name: client-onboarding
description: Use when the user takes on a new client, inherits an unfamiliar repo, or says "help me understand this codebase" — before any feature work, quoting, or bug fixing on a system they haven't worked in before.
---

# Learn a new client's codebase

The goal is not to read the code. The goal is a **written artifact** that makes every future session start warm: what the product does, how it deploys, where the bodies are buried. If the session ends with knowledge only in your context window, it ends with nothing.

## Procedure

### 1. Establish ground truth before inventory
- Which checkout is current? Check for multiple copies, worktrees, stale clones (`git log -1` each). Inventorying a stale checkout produces confidently wrong maps.
- What's deployed where? Remotes, CI config, Procfiles, deploy scripts. Deploy topology matters more than code structure — it's where mistakes become incidents.

### 2. Parallel inventory (fan out subagents; keep only conclusions)
- **Feature map**: routes/pages/controllers → one line per user-facing feature, noting what backs it (own DB, third-party API, another service).
- **Data model**: main tables/models, ownership/tenancy shape, anything shared across customers.
- **Integration surface**: every third-party provider (payments, email, APIs), where keys live, which are load-bearing.
- **Money paths**: signup, billing, and the feature customers pay for. Know them on day one.
- **The graveyard**: dead-but-routable pages, commented-out code, `-old` files, TODO bombs. Dead code that still routes is live risk.

### 3. Read history, not just state
```bash
git log --oneline -30                    # what's been happening lately
git shortlog -sn --since="1 year ago"    # who actually works here
```
Recent commit messages reveal active pain points better than any doc. If one previous developer dominates and they're leaving, switch to the `dev-handoff` skill — it's time-sensitive.

### 4. Verify the two claims that are always wrong
- The README's setup instructions (run them; note every divergence).
- Any statement about how deploys work (trace the real path: what happens on merge? Is CI even running? A billing-lapsed CI means merges silently deploy nothing).

### 5. Deliverable: the project memory file
Write `CLAUDE.md` / `AGENTS.md` (or the client-brief equivalent) with:
```
# <Client> — project brief
Product: <one line>
Environments: <env → URL → deploy command → verification step>
Data model: <sketch>
Providers: <name → where credentials live (never the values) → load-bearing?>
Money paths: <list>
Landmines: <known>
Open questions for the client: <list>
```
This file *is* the onboarding. Everything else was research for it.

## Red flags
- You're reading source files before you know which checkout is deployed
- The session is ending and no file has been written
- The deploy path is described from the README, not traced
- Credential values appeared in the brief

## Failure modes this prevents
- Weeks of "learning by breaking" on a live client system
- Inventorying a stale checkout and building a confident wrong map
- Knowing the code but not the deploy path — then shipping through the wrong one
- Knowledge trapped in one session, re-derived (and re-billed) every time
