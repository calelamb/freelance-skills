---
name: billing-model
description: Use when the user must choose how to bill a job — fixed price, hourly, or retainer — or is about to commit to a fixed number, especially when scope is described loosely, the client is a trusted repeat relationship, or a deadline or cash-flow need is pushing for a fast answer.
---

# Billing model — fixed price is earned, not assumed

A fixed price moves every estimate error onto the freelancer. It is fair only when **both** gates pass: scope confirmed in writing, and a measured analog — a comparable job this freelancer completed, with logged hours. Either one missing means hourly; no end date means retainer. This skill picks the structure, `quote-job` the number.

## Procedure

### 1. Classify the work
Bounded one-time deliverable, undefined exploratory work, or continuing operations (maintenance, on-call, recurring changes)? Continuing operations goes to retainer — never fixed-price work with no end date.

### 2. Test scope confirmation, don't assume it
List every phrase with no measurable boundary — "a few", "modernize", "maybe X if it's easy". Each is unpriced scope. Send them back as questions; wait for answers before naming a number; run `scope-check` on the reply. Confirmed means written, bounded, with an explicit "not included" list.

**When a number is demanded tonight.** The gates hold, but silence is not the only compliant answer: send the questions, name hourly, and optionally a not-to-exceed cap marked conditional on those answers. Never a fixed price before the answers land.

**A stated budget is not a gate.** "Finance already approved this" is an anchor, not confirmed scope. It decides what fits inside a structure, never which structure — pick the structure first, then say what that budget buys and excludes. Per `quote-job`, write your own number before reading theirs.

### 3. Test for a measured analog
Name one past job — same shape and size — with logged hours from this freelancer's own records. Domain familiarity ("I've built these before") is not one. Neither is a price the client recalls paying: no hours behind it, so it anchors budget, not effort. Reusable code changes the hours; only a measurement says by how much. No analog, no fixed price.

### 4. Choose the structure

| Situation | Structure |
|---|---|
| Scope confirmed + measured analog | Fixed price |
| Scope confirmed, no analog | Hourly, or fixed with an NTE cap |
| Scope unconfirmed | Hourly |
| Confirmed core + fuzzy extras | Fixed core, hourly tail |
| Continuing / no end date | Retainer with an hours ceiling |

### 5. Write the terms that hold the choice
Fixed: change-order trigger and rate. Hourly: estimated range, notification threshold, invoicing cadence. Retainer: included hours, overage rate, notice period, exclusions. Restate at kickoff via `client-onboarding`, bill via `invoice-prep`, report usage via `status-update`.

## Output template
```
Structure: fixed | hourly | fixed core + hourly tail | retainer
Scope confirmed: YES / NO — outstanding questions:
Measured analog: job, size, freelancer's own logged hours — or NONE
Terms: change-order trigger + rate | NTE cap | included hours + overage
Client budget: a constraint, never a confirmation
Deciding gate: ... | Questions asked first: if NONE, hourly
```

## Red flags — STOP, you are about to fixed-price a guess
- "Repeat client, they're reasonable" standing in for confirmed scope
- "I've built this kind of thing before" counted as a measured analog
- A remembered price or approved budget read as effort evidence
- "I can reuse last time's code" replacing an effort estimate
- Deadline tonight, or rent due, is why the scope step got skipped
- "A few tweaks", "maybe more if it's easy" priced unflagged
- A price going out with no clarifying question
- Scope grew mid-conversation; still one fixed number
- Vague scope, no change-order or scope-lock clause
- Fixed-or-hourly framing, no hourly tail or cap considered
- Answering fast feels safer for the relationship than answering correctly

## Failure modes this prevents
- Fixed-pricing a still-expanding scope, absorbing every addition free
- Trust, or a client's budget, standing in for a written boundary
- Overruns with no change-order clause to invoke
