---
name: client-vetting
description: Use when the user is weighing whether to take on a prospect — an inbound inquiry, a referral, a rescue of code an earlier developer abandoned — and especially when the prospect is urgent, vague about money, wants work started before paperwork, or the user needs the income.
---

# Client vetting — score the prospect, don't read the vibe

The unpaid three months begins with a warm referral and a freelancer who needed work. Every signal that predicts it is visible *before* work starts — score them, let the threshold decide.

## Rule that overrides your defaults

**Score only what the prospect actually said.** Invent nothing — not for the card, not for the reply you draft. Name the facts you need (the budget answer, why the last developer left) and stop. An unasked question is **unscored**, not 0: only *asked plainly, still no number* scores 3. A total with unscored lines is provisional — no verdict until they close.

## Procedure

### 1. Score the known signals

| Signal | Points |
|---|---|
| Previous developer left, was fired, or went dark | 3 |
| No budget number after being asked plainly | 3 |
| Work starts before a signed contract or deposit | 3 |
| Equity, revenue share, or exposure instead of a rate | 3 |
| Scope described as a feeling — "modern", "cleaner" | 2 |
| "Should be quick" about work nobody has scoped | 2 |

### 2. Probe the highest scorer
- **Previous developer:** was their last invoice paid? An unpaid predecessor is an automatic no, whatever the total. Paid, left cleanly → 1; run `dev-handoff`.
- **No budget:** "What range have you set aside?" No number means no budget, not a private one.
- **Work before contract:** offer paid discovery. Refusal to pay for a day previews refusal to pay for a month.
- **Equity:** say its cash equivalent out loud. If the number embarrasses them, it was exposure.
- **Feeling-scope:** hand to `scope-check` before quoting.

### 3. Verify one claim independently
Five minutes in public sources: does the company exist, did the product ship. "Well funded" is not a budget; an unverified claim never counts in their favor.

### 4. Decide by threshold
- **0–2 → go.** Standard terms → `quote-job`.
- **3–5 → go-with-deposit.** Deposit up front, milestone billing, pause on a late invoice — `client-onboarding` + `invoice-prep`.
- **6+ → no.** Decline in writing, or counter with a prepaid fixed-fee discovery — unbounded risk made into one paid job.

### 5. Write the decision before replying
Record score and terms first. Terms are lost by concession, never by decision — a softening must be a deliberate re-score.

## Output template
```
Signals: previous dev went dark (3) · no budget (3)
Unscored: <signal — the question that settles it>
Total: 8 → NO (or GO / GO-WITH-DEPOSIT / PROVISIONAL — facts missing)
Terms: <deposit % · milestone billing · pause at N days past due>
Next: <missing facts / decline / prepaid discovery / quote-job>
```

## Red flags — STOP, you're talking yourself into it
- A thin brief filled with plausible signals, or scored after accepting the job
- A verdict issued while lines remain unscored
- "Tight but doable" — their launch date adopted before scope existed. Their urgency is not your deadline: a same-day call is fine, a same-day yes is not
- "Just a quick look at the repo before paperwork" — reading their code to estimate is the work; repo access is a contract term, not a favor
- "A small paid test" / "a free task to prove myself" — a trial is work: same deposit, scope, terms; unpaid, it's the three months in miniature
- "I'll ask about budget once they see the value", or any probe held back to keep the tone warm — no question gets easier after they like you
- "The last developer was just bad" — the client's uncorroborated account
- A 3-point signal scored 0 because the prospect seemed embarrassed, or your month was slow — need changes the terms you accept, never the threshold
