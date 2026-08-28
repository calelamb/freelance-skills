---
name: invoice-prep
description: Assemble a billing period's work into a clean, dispute-proof invoice summary from time logs, commits, and tickets. Use when the user needs to prepare an invoice, summarize billables, or reconcile hours for a client.
---

# Invoice prep — the invoice nobody questions

An invoice gets paid without friction when every line answers "what did I get for this?" before the client asks. The work here is reconciliation and translation: match hours to outcomes, in the client's language, with the surprises already explained.

## Procedure

### 1. Reconcile three sources
Time log (spreadsheet/tracker), git history, and the ticket board for the period. They should tell one story. Where they diverge — logged hours with no visible output, or shipped work with no logged hours — resolve it NOW: unlogged shipped work is money left on the table; logged hours with nothing visible need a defensible line (investigation, meetings, ops) before the client asks.

### 2. Build line items by outcome
Group hours into client-legible units: features shipped, bugs fixed (named the way the client knows them — "the dashboard error Payton reported," not a ticket number), investigations concluded, ops/maintenance. Per line: short outcome description · hours · evidence available on request (deploy record, before/after). Keep internal jargon out entirely.

### 3. Handle the honest awkward categories
- **Investigation that refuted a bug**: bill it, describe it as the diagnosis it was ("verified the reported X was already resolved; confirmed on production"). Finding out nothing is broken is a deliverable.
- **Rework of your own bug**: the professional default is not billing to re-fix your own recent error; a consistent policy stated once builds more trust than any single invoice.
- **Blocked/waiting time**: bill only what was actively worked. "Waiting on client" hours that appear as billables are the fastest route to a dispute.

### 4. Flag variance before the client does
If this period is notably above the usual range, add one sentence up top explaining why ("heavier month: the migration project's cutover, as scoped in the July estimate"). Variance the client discovers by comparing invoices feels like a problem; variance you announce feels like transparency.

### 5. Output
A summary block (period, total hours, rate, total) + the line-item table + a two-line "what changed for you this month" narrative that echoes the status updates already sent. If the client received status updates all month, the invoice should read like their recap — an invoice that surprises the client is the failure mode, and it means the status updates failed too. Export to the user's actual invoice format (PDF/spreadsheet) on request.

## Failure modes this prevents
- Hours that don't map to anything the client remembers agreeing to
- Shipped work forgotten and never billed
- The month-over-month variance discovered by the client instead of explained by you
- Disputes rooted in jargon line items the client couldn't evaluate
