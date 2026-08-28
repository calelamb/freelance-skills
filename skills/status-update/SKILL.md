---
name: status-update
description: Turn commits, tickets, and work logs into a client-ready status update written in outcomes, not implementation details. Use when the user needs to update a client on progress, answer "where are we at?", or summarize a work period.
---

# Client status update — outcomes, not diffs

Clients don't buy commits; they buy outcomes. A status update full of "refactored the serializer, fixed the N+1" tells a non-technical client nothing and invites the question "so… is the thing done?" This skill translates engineering activity into what the client actually cares about: what works now that didn't, what it means for their users, and what's blocked on them.

## Procedure

### 1. Gather the raw material
Commits since the last update (`git log --oneline --since=...`), tickets moved, deploys shipped, and — importantly — investigation work that produced knowledge but no code (a diagnosed root cause, a refuted bug). Investigation is real billable progress; report it as such.

### 2. Translate every item to the client's frame
- "Fixed BacklinkStat serializer nil handling" → "The authority score on your dashboard now shows when it was last updated."
- "Refuted PAI-736 premise" → "Investigated the SERP error you reported — it was caused by the provider outage on June 19 and has been resolved since; nothing is currently broken."
- Group by **feature the client knows**, never by codebase area. If an item can't be expressed as a user-visible outcome or a risk retired, it's probably internal work — bundle it as one honest line ("ongoing stability and test-coverage work") rather than itemizing invisible things.

### 3. Structure
1. **Shipped** — live and verified, with where to see it. Only include what's actually deployed and checked; "done but not deployed" goes in the next section, honestly labeled.
2. **In progress** — with expected landing, stated as a range.
3. **Blocked on you** — decisions, access, approvals the client owes. Make this impossible to miss; buried asks become "why didn't you tell me" later.
4. **Heads-up** — risks, costs, or scope changes on the horizon. Bad news ages terribly; it goes in the update where it's small, not the invoice where it's a dispute.

### 4. Calibrate length and register
Match the client's medium and energy — a Slack client gets six tight bullets, an email client gets three short paragraphs. Never pad: a strong two-item week reads better than a strong two-item week wrapped in filler. Numbers beat adjectives ("audit success rate 62% → 97%" beats "significantly improved reliability").

## Failure modes this prevents
- The update that's technically detailed and communicates nothing
- Investigation weeks that look like "nothing happened" because nothing merged
- Client asks buried mid-paragraph, unanswered for a month
- "Done" claimed for things that weren't deployed, discovered by the client
