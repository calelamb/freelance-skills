---
name: context-switch
description: Use when the user returns to a client after days or weeks away, resumes a paused engagement, or moves between concurrent clients — especially when a deploy is expected, the situation is urgent or revenue-affecting, or the client says everything is already set up from last time.
---

# Context switch — reload the client, don't recall them

What you remember about this client is a snapshot: branches merged, remotes changed, env vars appeared while you were gone. And the state you reach for first belongs to whichever client you worked on last. Urgency is when muscle memory ships to the wrong place.

## Procedure

### 0. Confirm you can reach the systems
The reload needs live access: repo, board, deploy targets. If any is missing, name the blocker and ask for the one thing needed (repo path, board URL, target list). That is a legitimate stop, not a clarifying question to skip. Never fabricate command output, guess a path, or let the client's assurance substitute for a check you couldn't run.

### 1. Reload the brief before the code
Re-read the brief and repo docs: deploy topology, environment naming, branch model, protected files. Never rebuild these from memory — memory holds the other client's conventions. No brief? Don't pause to author one; run steps 2–5, let the live systems be the source, then write up the result for `client-onboarding`.

### 2. Diff the world against your last session
What changed while you were gone — from the systems, not the client's summary:
```bash
git fetch --all --prune
git log --oneline --all --since="<date of last session>"
git branch -r --sort=-committerdate | head
```
Then the board, open PRs, incidents, and each environment's deploy history: what landed changes what your branch means.

### 3. Re-verify deploy topology from the live system
List the actual remotes/targets and the branch each environment tracks. Confirm which name is production and which staging — that mapping differs per client and is the easiest thing to carry over wrong. Check env-var presence (names only, never values) and migration state per environment. "It was this last time" and "they said it's set up" are hearsay; the remote list is evidence. What ships goes through `deploy-verify`.

### 4. Re-establish scope
Identify the branch and commit for the agreed work and confirm it still matches; weeks of drift means other changes may ride along. Work accumulated since goes through `scope-check`, not this deploy.

### 5. Capture rollback state before changing anything
Record each environment's deployed commit, env-var names, and migration status. That snapshot is the rollback plan — the only thing between a bad deploy and an outage.

### 6. Verify the real flow, then report
Prove the specific broken or changed path works end to end in the live environment, not a homepage 200. Then send the summary through `status-update`, naming what changed in the gap.

## Output template
```
Client: <name> · gap since <date>: <N days>
Access: <confirmed | BLOCKED: what is missing>
Changed since: <commits · PRs · tickets · incidents>
Topology today: prod = <target/branch> · staging = <target/branch>
Env + migrations: <in sync | drift> · rollback: <env: sha @ HH:MM>
Scope: <branch @ sha> · matches agreement: yes/no
Verifying: <the exact flow, not the homepage>
```

## Red flags — STOP, you are on another client's memory
- Deploy target assumed from last time; remotes never listed today
- Brief unread because the client's message suggested no change
- No idea what landed in the repo, board, or production during the gap
- Env-var or prod-vs-staging checks waived as "redundant" under time pressure
- "You already have everything set up, right?" taken as confirmation
- Another client's deploy commands or service names reached for by reflex
- Homepage 200 treated as proof; the broken flow never exercised
- "It's live" sent before that flow was proven end to end
- Production push with no state captured and no rollback path
- Unsure whether the merged branch is the scope agreed
- A check you couldn't run written up as though it ran, or a path guessed instead of asked for

## Failure modes this prevents
- One client's code deployed to another's remembered target
- A branch that quietly accumulated someone else's changes
- Code shipped without its migration or env var, onto an assumed environment
- "It's live" reported to a client whose broken flow is still broken
