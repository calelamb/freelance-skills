---
name: proposal-write
description: Use when a price or timeline is about to be sent to a client — especially when the number will be forwarded to a board, partner, or anyone not on the thread, when the client says "just send the number," or when it's late and a one-line reply is tempting.
---

# Write the proposal, not the number

A bare price is a price you will negotiate against. Forwarded, pasted into a deck, read cold by whoever decides, it is the only thing on the table — and every discussion moves it one direction. `quote-job` produces the number; this skill packages it to survive the forward.

## Rules that override your defaults

1. **All seven elements ship; length is what flexes.** Floor: one sentence of problem, one of approach, one row per `quote-job` milestone group, a range plus billing frame, one clause per assumption, every adjacent exclusion named, a next step with owner, date, expiry. Approach and milestones are elements, not padding; thinner is deletion.
2. **Never invent a per-milestone number.** Carry the real `quote-job` line items across. Holding only a total? Re-run `quote-job`, or list milestones unpriced beneath it. An invented split is a fabricated commitment.
3. **Trust is not framing.** Years of goodwill — "they'd never nickel-and-dime me" — don't reach the person reading the forward. Framing protects a long relationship; skipping it starts the renegotiation that damages one.

## Procedure

### 1. Restate the problem in their words
Open with the outcome they described, in their vocabulary, before any number — the boundary every later dispute is measured against. Can't write two sentences of it? Ask before you price.

### 2. Approach, in outcomes not tasks
Three to five sentences on why the work happens in this order — enough that a skeptical third party sees the reasoning without you there.

### 3. Milestones with client-visible deliverables
Each milestone is something they can *see*, never "backend work" — grouped `quote-job` line items if brevity demands. These become `invoice-prep`'s payment schedule and `status-update`'s checkpoints.

### 4. Price as a range, per milestone and total
Never a point estimate — it reads as a fixed-price promise. Name the frame once: fixed-scope, time-and-materials, or capped.

### 5. Assumptions — each one a renegotiation trigger
Every condition the price depends on: docs accurate, no new auth provider, access on day one, third parties responsive. State: "if an assumption proves false, we re-price that milestone before continuing."

### 6. Exclusions — what a cold reader would assume is included
Mobile changes, data migration, ongoing support, training, hosting, anything adjacent. Unlisted reads as included; when they later ask, that's `scope-check`, not a favor.

### 7. Next step with a date
One action, one owner, one date, plus an expiry on the price. "Let me know" is not a next step.

## Output template
```
The problem: <their words, 2 sentences>
Approach: <3–5 sentences, why this order>

| # | Milestone (client-visible) | Range | Timing |
|---|---|---|---|
| 1 | <what they can see> | <low–high> | <week n> |

Total: <range> · <fixed-scope | T&M | capped> · <billing frame>
Assumptions (if false, we re-price that milestone): <list>
Not included: <list>
Next step: <action, owner, date> · Quote valid until <date>
```

## Red flags — STOP, you are sending a naked number
- A price and a date, and no sentence describing the problem in their words
- You dropped the approach or the milestones because they asked for "just the number"
- Per-milestone figures you reasoned to just now instead of carrying from `quote-job`
- No assumptions listed — when the docs turn out wrong mid-build, nothing anchors a re-price
- No exclusions listed — the reader assumes migration and mobile are in the number
- The close is "let me know if you want to start": no document, no decision date, no expiry
- "They said framing isn't necessary," "we've worked together for years" — the client isn't the audience; whoever they forward it to is, and sees only the figure
- It's late, you've lost a day, and speed is the real reason you're trimming — compression costs 90 seconds
- You can see this being approved as a fixed-scope commitment and aren't flagging that

## Failure modes this prevents
- A forwarded figure becoming a fixed-scope commitment nobody agreed to
- Negotiating downward against your own number with nothing anchoring it
- Invented milestone splits quoted back as agreed prices
- Scope creep with no paper trail
