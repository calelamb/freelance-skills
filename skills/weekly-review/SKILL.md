---
name: weekly-review
description: Use when the user is wrapping up a work week, deciding what to send clients Monday, or preparing a status update or invoice — especially when hours are untracked, an estimate feels tight, a client has gone quiet, or the user says to keep it upbeat and skip the hours.
---

# Weekly review — reconcile before sending

An overrun surfaced Friday is a conversation; at invoice time it is a dispute the freelancer eats. Reconcile hours against every open quote and name what is blocked on clients before drafting anything client-facing.

## Procedure

### 1. Pull the actual numbers first
Time tracker, commit log, calendar — real logged hours per client, never memory. No tracking? Reconstruct from `git log --since="1 week ago"` plus calendar blocks, labelled `RECONSTRUCTED`.

### 2. Hours vs. quote, per client
Quoted, logged, percent consumed, percent of scope delivered. Past ~75% consumed with scope remaining is a **surface-this-week item**, not an invoice-time item. Express the overrun in dollars.

Hourly work uses the contracted rate. **Flat-fee work has no rate, so derive one:** fee ÷ quoted hours = implied rate, × overrun hours = exposure. Show the arithmetic, label it `IMPLIED RATE (derived)`, and frame it as margin absorbed, never as an amount to bill.

### 3. Separate delivered from claimed
Done needs evidence: tests passing, deployed, demoable. "I finished it" is In Review. Route deploy claims through `deploy-verify`.

**If evidence cannot be checked right now** — no repo, tracker, or deploy access — do not guess and do not lower the bar. Mark it `UNVERIFIED`, name the one check that settles it, keep it out of client-facing claims until it runs, and list it as a Monday blocker.

### 4. Name what is blocked on the client
Every item waiting on someone else — approvals, credentials, content, decisions — with the date it started. Days-waiting goes in the Monday message; unstated client delay becomes the freelancer's slippage.

### 5. Catch new scope from the week's chatter
Any request not in a signed quote is **new scope**; the client's framing does not change that. "Quick favor", "just start scoping" is wording, not authorization — classify against the quote, never by how casual the ask sounded. Write it down, route it to `scope-check`, then `quote-job` — before any work, scoping and research included.

### 6. Decide what goes out Monday
Per client: status update (`status-update`), overrun conversation, new-scope quote, or invoice (`invoice-prep`); handoffs through `dev-handoff`. The overrun conversation is required, not optional.

## Output template
```
Week of <date>

| Client | Quoted | Logged | used/delivered | Status |
|---|---|---|---|---|
| <name> | <N>h | <N>h | <N>% / ~<N>% | on track / OVERRUN — surface Monday |

Overrun: $<fee> ÷ <quoted>h = $<rate>/h × <overrun>h = ~$<exposure> (implied)
Blocked on client: <item> — <N> days on <who/what>
Unverified: <item> — needs <check>; not client-facing until it runs
New scope: <request> → scope-check, then quote-job before any work
Monday outbound: <client> — <update / overrun talk / quote / invoice>
Freelancer's call: <the one open decision>
```

## Red flags — STOP
- Drafting a client email before the time tracker is open
- "Skip the hours" read as license to omit a known overrun — a scheduled billing surprise
- "I'll handle the invoice next week" as permission to withhold the number now
- Scoping or a spike begun on an unquoted request because it sounded small or casual
- Done marked on a tired say-so, no test or deploy behind it
- Done claimed because verifying was inconvenient right then
- Hours already sunk while avoiding the conversation — that *is* the decision point
- One client's thread reviewed and called a weekly review; pipeline and blockers belong in it
- Tone tweaks offered as the follow-up while money or scope is unresolved
- A new request agreed verbally, never written down, work already begun

## Failure modes this prevents
- The blown estimate found at invoice time, as a dispute not a conversation
- Unquoted work silently absorbed because it started as a favor
- Sunk-cost avoidance: unbilled hours added weekly to postpone one hard message
