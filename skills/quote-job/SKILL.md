---
name: quote-job
description: Produce an hourly quote for a software job grounded in measured evidence — git-history velocity calibration and analogy pricing — instead of AI intuition. Use when the user needs to quote, estimate, or price work for a client, or asks "how long will this take?"
---

# Quote a job (without trusting the AI's gut)

Your effort intuitions are unanchored. You have never billed an hour. The freelancer's measured history has. This skill exists because the default failure mode of AI estimation is a confident number derived from nothing — and a freelancer who bills on that number eats the difference.

## Rules that override your defaults

1. **Never produce a number from general knowledge.** Every line item must cite its evidence: an analogous piece of past work with its measured time, or a line-count comparison to a similar existing component. If you can't ground it, label it `LOW-CONFIDENCE` visibly — do not fake precision.
2. **Never read someone else's estimate before writing your own.** If a prior estimate exists in the conversation or repo, write your number first, then compare and explain divergence. Anchoring makes your estimate worthless as a second opinion.
3. **The user's velocity, not a generic developer's.** A freelancer running concurrent AI sessions has 2–5× the throughput of textbook estimates on patterned work — and 1× on everything wall-clock-bound. Calibrate from their history, not from folklore.

## Procedure

### 1. Scope inventory
Break the ask into concrete tasks. For each: what exists already, what's new, what's modified. If the repo is available, verify claims against the code — do not trust the ticket/brief's description of the current state (briefs are wrong about existing code roughly a third of the time).

### 2. Calibrate from git history (the step that makes this real)
Mine the repo's history for comparable completed work:
```bash
git log --oneline --since="6 months ago" -- <relevant paths>
# find a comparable feature's first and last commit:
git log --reverse --format="%ad %s" --date=short -- <feature path> | head -5
git log --format="%ad %s" --date=short -- <feature path> | head -5
```
Compute observed rates: features/week, endpoints/week, elapsed days per comparable unit. This is THIS person's throughput with THEIR tooling. Use it as the unit price.

### 3. Price by analogy
For each new task, find the closest shipped analog: same shape, same layer, similar surface area (compare line counts of implementation + tests). New endpoint ≈ measured cost of the last similar endpoint. New page ≈ the last similar page. State the analog next to every number.

### 4. Split compressible from wall-clock-bound
Two categories, priced differently:
- **Compressible** (AI-parallelizable): patterned code, CRUD, tests-on-a-template, bulk rewiring. Apply the measured accelerated rate.
- **Wall-clock-bound** (does not compress): verification and QA passes, deploy/cutover rehearsals, design-review rounds with a human, third-party approval waits, meetings, monitoring windows, data-migration dry runs. Price these at human pace no matter how fast the code writes.

Mislabeling category 2 as category 1 is the single biggest source of blown quotes.

### 5. Risk as explicit line items
Contingency is not padding hidden inside tasks. Name each risk (unproven integration, data migration with no rollback, dependency on a third party's schedule) and give it its own priced line. The client can then choose which risks to fund.

### 6. Output format
A table per phase: task · hours (range, never a point) · evidence for the number. Then: total range, midpoint, calendar time at observed velocity, earliest client-visible milestone, and a stated-assumptions list (design readiness, access, decisions pending). End with the billing-frame note: if the freelancer bills attention-hours while running parallel sessions, say so — output-equivalent and hours-at-desk are different numbers, and mixing frames mid-project is the only wrong choice.

## Failure modes this prevents
- The confident generic number (40h for "add auth") with no basis
- Anchoring on the client's hoped-for budget or a prior estimate
- Uniform "AI makes everything 3× faster" discounts that ignore wall-clock-bound work
- Contingency smeared invisibly across tasks so nothing can be negotiated
- Point estimates that read as promises
