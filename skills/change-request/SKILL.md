---
name: change-request
description: Use when a client asks mid-project for something possibly outside the confirmed scope — a "small addition", a "while you're in there" tweak, a follow-on framed as basically the same code path — especially under deadline pressure, near final payment, or when the client says to trust your judgment and invoice later.
---

# Change request — the delta is a new job

Mid-project asks arrive framed as continuations, never as new work. Each one absorbed free comes out of margin, and the pull to absorb peaks when it costs most: late, mostly paid, tired, wanting the relationship to end well. Only the confirmed written scope separates a change request from work already bought.

## Procedure

### 1. Retrieve the confirmed scope verbatim
Quote the agreed deliverable lines from `scope-check` back exactly — not your memory, not the client's summary. Can't reach the document yourself? Stop and have the freelancer paste the exact lines; never classify, price, or build against a remembered or paraphrased scope. No written scope at all? Establish one (`client-onboarding`) first: there is no delta without a baseline.

### 2. Classify: defect, clarification, or new scope
Three outcomes, three bills. A defect in delivered work is free — confirm via `bug-triage`, don't assume. A clarification of a genuinely ambiguous line is usually absorbed. Anything adding a behavior, surface, state, or integration the scope does not name is billable.

### 3. Name the delta precisely — the client's framing is not evidence
"Basically the same code path" is a claim about implementation, usually wrong at the edges: new states, failure modes, tests, deploy risk. Enumerate what it actually requires against the scope line it falls outside.

### 4. Price it separately
Run `quote-job` on the delta alone: evidence-backed range, its own risks, its own effect on committed dates. Never fold it into the original total — the client must be able to see and decline this item separately.

### 5. Get the written yes before the first commit
Send the note, then wait. A written "approved at $X" is a precondition to starting, not paperwork for later. "Trust your judgment", a thumbs-up, and "we'll sort the invoice later" are approvals to work for free, not to bill. If the deadline can't survive the wait, price both paths — date moves, or date holds and this ships next — and write nothing meanwhile. Offering options is not permission to start "in good faith". A stopgap for a demo (static mock, screenshot) is allowed only where the note names it unbilled, time-boxed, and explicitly not the delta.

### 6. Build exactly the delta
Only what was approved. Anything adjacent you notice becomes a future priced item, never part of this build. Log the amount for `invoice-prep` and its status for the next `status-update`.

## Output template
```
CHANGE REQUEST — <name>

Confirmed scope (<doc>, <date>): "<exact line this falls outside>"
Requested: <the ask, their words>
Classification: new scope | clarification (absorbed) | defect (free)

Adds beyond it:
- <behavior / surface / state / integration not in scope>
- <tests, data, failure modes, deploy risk>

Price: <range> · Evidence: <analog, per quote-job>
Options: (a) approve at <price>, date → <date>
         (b) hold date, ships <later date>
         (c) decline — scope and date unchanged
         (d) stopgap <mock/screenshot> for <date> — unbilled, not the delta

Excluded: <adjacent work, priced later>
Starts on: written approval.
```

## Red flags — STOP, you are absorbing scope
- The addition was described without quoting the scope line it exceeds
- "Same code path" became the scope boundary instead of being tested
- Work began before any price existed, or while the yes was still outstanding
- "Trust your judgment" or a thumbs-up standing in for a written yes
- "Given the timeline, quoting costs more time than building it"
- "We'll sort the invoice later" treated as a decision, not deferred leverage
- Mostly paid, goodwill high, already in there — so this one's free
- You're tired and want final payment released, so you stopped asking
- A delivery date promised before the billable-or-not question was answered
- Extras nobody asked for (proration, tiering, webhooks) got built because you were in there

## Failure modes this prevents
- Unbilled feature creep eating the margin on fixed-price work
- The client's difficulty estimate deciding what is in scope
- Verbal approvals that vanish when the invoice arrives
- Sunk cost, fatigue, and end-of-project goodwill converted into free labor
- Self-initiated expansion compounding work nobody agreed to buy
