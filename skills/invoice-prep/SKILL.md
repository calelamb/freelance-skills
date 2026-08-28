---
name: invoice-prep
description: Use when the user needs to prepare an invoice, summarize a billing period, or reconcile logged hours against shipped work for a client — especially when the period is unusually heavy or light, or includes investigation, rework, or waiting time.
---

# Invoice prep — the invoice nobody questions

An invoice gets paid without friction when every line answers "what did I get for this?" before the client asks. The work is reconciliation and translation: match hours to outcomes, in the client's language, with the surprises already explained.

## Procedure

### 1. Reconcile three sources
Time log, git history, and the ticket board for the period should tell one story. Where they diverge, resolve it **now**: shipped work with no logged hours is money left on the table; logged hours with nothing visible need a defensible line (investigation, meetings, ops) before the client asks. If only one source exists, say so and note the gap.

### 2. Build line items by outcome
Group hours into client-legible units: features shipped, bugs fixed (named the way the client knows them — "the dashboard error your designer reported," not a ticket number), investigations concluded, ops/maintenance. Per line: outcome · hours · evidence available on request. No internal jargon.

### 3. Handle the honest awkward categories
- **Investigation that refuted a bug**: bill it, describe the diagnosis ("verified the reported X was already resolved; confirmed on production"). Finding out nothing is broken is a deliverable.
- **Rework of your own recent bug**: the professional default is not billing it; a consistent policy stated once builds more trust than any single invoice.
- **Blocked/waiting time**: bill only what was actively worked. "Waiting on client" as a billable line is the fastest route to a dispute.

### 4. Flag variance before the client does
If the period is notably above or below the usual range, one sentence up top explains why ("heavier month: the migration cutover, as scoped in the July estimate"). Variance the client discovers feels like a problem; variance you announce feels like transparency.

## Output template
```
Period: <dates> · Hours: <n> · Rate: <r> · Total: <t>
<one-line variance note if applicable>

| Outcome | Hours | Evidence on request |
|---|---|---|
| Billing page live on production | 6.5 | release v128, screenshots |
| Investigated + refuted reported score error | 1.5 | comparison snapshot |
| Ongoing stability / test coverage | 2.0 | test count 140 → 162 |

What changed for you this month: <two lines, echoing the status updates already sent>
```
If the client got status updates all month, the invoice should read like their recap. An invoice that surprises the client means the status updates failed too. Export to the user's real invoice format on request.

## Failure modes this prevents
- Hours that don't map to anything the client remembers agreeing to
- Shipped work forgotten and never billed
- Month-over-month variance discovered by the client instead of explained by you
- Disputes rooted in jargon line items the client couldn't evaluate
