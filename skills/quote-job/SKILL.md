---
name: quote-job
description: Use when the user needs to quote, estimate, price, or answer "how long will this take?" for client software work — especially when a prior estimate or client budget is already on the table, or the request comes with deadline pressure.
---

# Quote a job (without trusting the AI's gut)

Your effort intuitions are unanchored — you have never billed an hour. The freelancer's measured history has. The default failure mode of AI estimation is a confident number derived from nothing; a freelancer who bills on that number eats the difference.

## Rules that override your defaults

1. **No number without evidence.** Every line item cites its source: an analogous piece of past work with its measured time, or a size comparison to an existing component. Can't ground it? Label it `LOW-CONFIDENCE` in the table — never fake precision.
2. **Write your number before reading theirs.** If a client budget or prior estimate is in the conversation, produce your estimate first, *then* compare and explain the divergence. Anchoring makes a second opinion worthless.
3. **This freelancer's velocity, not a generic developer's.** Someone running parallel AI sessions ships patterned work 2–5× faster than textbook rates — and exactly 1× on anything wall-clock-bound. Calibrate from their history.
4. **No repo? Calibrate from the freelancer instead.** Ask for repo access, and in the same message ask: "What's the closest thing you've built to this, and how long did it take you?" Their answer is evidence; use it. If neither is available by the deadline, still deliver a range — every line marked `LOW-CONFIDENCE`, with a one-line note that the number tightens once the repo is in hand. A late quote is a lost job; a labeled provisional quote is honest.

## Procedure

### 1. Scope inventory
Break the ask into concrete tasks: exists / new / modified. Verify the brief's claims about current state against the code — briefs are wrong about existing code roughly a third of the time.

### 2. Calibrate from git history
```bash
git log --oneline --since="6 months ago" -- <relevant paths>
# elapsed time for a comparable feature: first and last commit
git log --reverse --format="%ad %s" --date=short -- <feature path> | head -3
git log --format="%ad %s" --date=short -- <feature path> | head -3
```
Derive observed rates (endpoints/week, elapsed days per comparable unit). That is the unit price.

### 3. Price by analogy
For each new task, name the closest shipped analog — same shape, same layer, similar size (compare implementation + test line counts). The analog goes in the evidence column next to the number.

### 4. Split compressible from wall-clock-bound
- **Compressible** (parallelizable): patterned code, CRUD, template tests, bulk rewiring → measured accelerated rate.
- **Wall-clock-bound**: QA passes, deploy rehearsals, human design-review rounds, third-party approval waits, meetings, monitoring windows, migration dry runs → human pace, regardless of how fast the code writes.

Mislabeling the second as the first is the single biggest source of blown quotes.

### 5. Risk as its own line items
Contingency is not padding hidden inside tasks. Name each risk (unproven integration, migration without rollback, third-party schedule) and price it separately so the client can choose which risks to fund.

## Output template
```
| Task | Hours (range) | Evidence |
|---|---|---|
| New billing page | 4–6 | analog: settings page, 5.2h logged, 310 LoC |
| Webhook handler  | 6–9 | LOW-CONFIDENCE: no analog in repo |
| Risk: Stripe test-mode approval wait | 0–4 (wall-clock) | third-party |

Total: 22–31h · midpoint 26h · calendar: ~2 weeks at observed velocity
First client-visible milestone: <what, when>
Assumptions: <design ready / access granted / decisions pending>
Billing frame: <attention-hours vs. hours-at-desk — state it once, never mix>
Divergence from prior estimate (if any): <theirs vs. yours, and why>
```

## Red flags — STOP, you are guessing
- A number appeared before you looked at any history
- "A typical Stripe integration is about…"
- You read the client's budget first and are now "sanity-checking" it
- Every task got the same AI-speedup discount
- A point estimate instead of a range
- Contingency is a percentage, not named risks

## Failure modes this prevents
- The confident generic number (40h for "add auth") with no basis
- Anchoring on the client's hoped-for budget or a prior estimate
- Uniform "AI makes everything 3× faster" discounts on wall-clock-bound work
- Contingency smeared across tasks so nothing can be negotiated
- Point estimates that read as promises
