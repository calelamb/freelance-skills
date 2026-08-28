---
name: expense-and-time-tagging
description: Use when the user is logging, totaling, or reconstructing time and expenses for client work — especially at month-end under invoice pressure, when the tracker export covers only part of the period, when a client asks for one lump-sum number or says "trust your number," or when a reimbursable cost is being deferred.
---

# Expense and time tagging — tag at the moment, not at month-end

Untagged time and money get rebuilt from memory, and memory only rounds down. Tags go on at creation, so month-end is arithmetic over a complete ledger, not recall. Reconstruction is a recovery procedure that runs on timestamps.

## Rules that override your defaults

1. **Never produce an hours figure from recollection.** Not under deadline, not as "roughly three long days." A recalled number is always low and becomes the permanent record the moment it is sent. No timestamps means the hours are unknown — say that.
2. **A deadline changes what you send, not how you get the number.** If a gap can't be reconstructed in time, invoice the reconstructed portion and add a `PROVISIONAL` line naming the uncovered dates and the true-up date.
3. **"Trust your number" waives client-side detail, not verification.** Bill only what you reconstructed; bill the gap next cycle. "Good-faith figure tonight, true it up later" is the memory number renamed.
4. **Log a reimbursable immediately; bill it when it fits.** The entry gets made the day the charge lands, always. Which invoice it rides on is a choice available only once the entry exists.

## Procedure

### 1. Fix the taxonomy once, per engagement
Set at kickoff (during `client-onboarding`), never per entry. Five fields: **client · project · category · billable (yes / no / reimbursable) · tax category**. Categories map 1:1 to invoice line items so `invoice-prep` groups rather than rewrites; one invented mid-month breaks that mapping.

### 2. Tag at the moment of work
Start the timer with its tags already on. Non-obvious billables — calls, code review, deploy babysitting, chat debugging, scope talk — each get an entry; they are what memory drops. Out-of-scope work routes to `scope-check`.

### 3. Log expenses the day they are incurred
Reimbursables (cloud bills, API credits, travel) get an entry the day the charge lands: amount, date, vendor, receipt ref, client, flag. Unbillable this cycle? Log it now, marked deferred.

### 4. Check coverage, then reconstruct from timestamps
A partial export is not a source of truth: compare its range against the billing period. Name the uncovered dates, then rebuild each from commits, calendar entries, message timestamps, call logs, ticket transitions, deploys. Reconcile against tracked entries so nothing is double-counted. Tag with the five fields, mark `RECONSTRUCTED`, cite the source. Round only to the tracker's precision.

### 5. Keep the internal ledger broken out
A client may want one invoice line; that's fine. The internal record stays categorized regardless — it feeds tax categories, calibrates the next `quote-job`, settles disputes.

## Output template
```
<date> · <client> · <project> · <category> · <h.hh>h · <yes|no|reimbursable> · <tax cat> · <tracker|RECONSTRUCTED: source>

Coverage: export <range> vs. period <range>; GAP <dates>
Reconstructed: <h.hh>h from <sources>
Provisional: <dates> not reconstructed, not billed, true-up by <date>
Expense: <vendor> <amt> <date> — reimbursable, receipt <ref>, bill <this|next> cycle
Unrounded total: <h.hh>h · <category> <h.hh> · <category> <h.hh>
Client-facing: <lump sum|broken out>; internal always broken out
```

## Red flags — STOP, you are losing billables
- A partial export got totaled, its missing weeks never flagged as missing billables
- An untracked stretch got its number from memory, not commits, messages, or logs
- Deadline pressure became a reason to estimate rather than to invoice provisionally
- You rounded to a clean number, discarding minutes you earned
- A lump-sum request produced a lump-sum internal record too
- A reimbursable was pushed to "next month" with no entry, ticket, or receipt
- "Starting on X" messages were never reconciled against the tracker before totaling
- "Trust your number" read as skipping verification rather than requiring an accurate record
- Reconstructed hours carry no client / project / category tag
- Distinct work types — calls, fixes, migration — sit in one bucket the sources separated
- Nobody warned that an unbroken-out invoice under month-end pressure permanently undercounts billables

## Failure modes this prevents
- Month-end reconstruction from memory, which undercounts
- Partial exports accepted as the whole period
- Reimbursables deferred into nonexistence
- Lump sums that destroy the entry → line item → tax mapping
