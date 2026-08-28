---
name: status-update
description: Use when the user needs to update a client on progress, answer "where are we at?", or summarize a week/sprint/month of work for a non-technical reader — including weeks where most of the work was investigation rather than shipped code.
---

# Client status update — outcomes, not diffs

Clients don't buy commits; they buy outcomes. "Refactored the serializer, fixed the N+1" tells a non-technical client nothing and invites "so… is the thing done?" Translate engineering activity into what works now that didn't, what it means for their users, and what's blocked on them.

## Procedure

### 1. Gather the raw material
Commits since the last update (`git log --oneline --since=<date>`), tickets moved, deploys shipped, and — importantly — investigation that produced knowledge but no code (a diagnosed root cause, a refuted bug). Investigation is real progress; report it as such.

### 2. Translate every item to the client's frame
- "Fixed serializer nil handling" → "The authority score on your dashboard now shows when it was last updated."
- "Refuted ticket #412" → "Investigated the error you reported — it came from the provider outage on the 19th and has been resolved since; nothing is currently broken."
- Group by **feature the client knows**, never by codebase area. If an item can't be stated as a user-visible outcome or a retired risk, bundle it into one honest line ("ongoing stability and test-coverage work") rather than itemizing invisible things.

### 3. Structure
1. **Shipped** — live *and verified*, with where to see it. "Done but not deployed" goes in the next section, labeled honestly.
2. **In progress** — with an expected landing, as a range.
3. **Blocked on you** — decisions, access, approvals the client owes. Make this impossible to miss.
4. **Heads-up** — risks, costs, scope changes on the horizon. Bad news belongs in the update where it's small, not the invoice where it's a dispute.

### 4. Calibrate length and register
Match the client's medium: a Slack client gets six tight bullets, an email client gets three short paragraphs. Never pad — a two-item week reads better unwrapped. Numbers beat adjectives ("audit success rate 62% → 97%" beats "significantly improved reliability").

## Red flags
- A commit hash, ticket ID, or class name appears in the draft
- "Shipped" contains something you haven't seen on the live site
- The client's action item is mid-paragraph rather than its own section
- Bad news is missing because it's "not final yet"

## Failure modes this prevents
- The update that's technically detailed and communicates nothing
- Investigation weeks that look like "nothing happened" because nothing merged
- Client asks buried mid-paragraph, unanswered for a month
- "Done" claimed for things that weren't deployed, discovered by the client
