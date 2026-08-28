---
name: estimate-postmortem
description: Use when a client job, milestone, or fixed-bid deliverable has just shipped, been invoiced, or been closed out — especially when it ran over the quoted hours, when the client has said not to reopen the quote, or when the freelancer is tired and moving on.
---

# Estimate postmortem — record the miss

The estimate stays open until the variance is written down. An unexamined overrun is not a one-time loss but a pricing rule that stays wrong — the same line item misses the same way next job. "Don't reopen the quote" is a *client* instruction about the invoice, never permission to skip the internal record; tired is a reason to write a rough table tonight, not to defer.

**Timing.** Ship and invoice first under a live deadline; write the record that same session — before sleep, before the next job. A day after shipping is the ceiling, not the target. Ten minutes.

## Procedure

### 1. Reconstruct actuals from artifacts, not recall
Commit timestamps, session logs, threads — first-to-last elapsed per work area, minus gaps. Recalled hours skew low. Never enter a remembered figure as measured: with no artifacts reachable, mark that actual `RECALLED`, treat it as a floor, and call the table provisional until timestamps confirm it.

### 2. Rebuild the quoted line items verbatim
Copy the original rows as sent; re-cutting them to fit what happened hides the miss.

### 3. Compute variance per line — hours and percent
Quoted, actual, delta, percent, every row. "Ran long" is not a variance. Record unders too, or the next quote biases upward.

### 4. Name a cause category per miss
A repeatable class, not a restatement: undocumented third-party/API discovery · brief wrong about the code · wall-clock work priced as compressible · scope added mid-job (`scope-check`) · unverified-deploy rework (`deploy-verify`) · unplanned debugging (`bug-triage`).

### 5. Separate billed from absorbed
Hours invoiced vs. hours worked. Absorbed time gets a line naming what the client got free — input to `invoice-prep` and the next quote's risk lines. An agreed invoice total is not the whole financial story: write the absorbed line even after invoicing.

### 6. Log tradeoffs taken under pressure
Manual smoke test instead of automated coverage, skipped review, deferred cleanup — unlogged, these return as unpaid work. Log only a shortcut you can name concretely; one merely inferred from the pressure gets `UNCONFIRMED` until an artifact confirms it. Never invent one.

### 7. Write the calibration rule back
One imperative sentence per cause, worded so `quote-job` can apply it to a future line item. This step is the product.

## Output template
```
| Line item | Quoted | Actual | Δ | % | Cause category |
|---|---|---|---|---|---|
| <item> | 8h | 15h | +7h | +87% | undocumented third-party API discovery |
| <item> | 3h | 2h | -1h | -33% | analog held |

Quoted 11h · actual 17h · +55% · billed 11h · absorbed 6h (API discovery)
Tradeoff: manual smoke test replaced automated coverage — debt open

Calibration for quote-job:
- Undocumented third-party API → its own LOW-CONFIDENCE discovery line, 1–2× the integration estimate.
```

## Red flags — STOP, the miss is going unrecorded
- Ended at "shipped and invoiced," no variance table
- Reading "don't relitigate the quote" as permission to skip the internal record
- "Ran long" written without quoted vs. actual vs. percent
- Cause column restates the symptom — "took longer than expected"
- "Look at it tomorrow" / "get some sleep first" — the record dies here
- Testing cut for a deadline, logged nowhere
- "Closed the loop" / "on to the next" before the record exists
- Every sentence serves client comfort, none the freelancer's margin
- Hours absorbed silently, nothing naming what was given away
- Actuals from memory, unlabelled, with the repo right there
- Nothing written back in a form `quote-job` can read next time

## Failure modes this prevents
- The identical miss repeating on the next job of this shape
- Discovery on unfamiliar third-party APIs priced as implementation
- Overruns absorbed invisibly until the effective hourly rate collapses
