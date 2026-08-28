---
name: project-closeout
description: Use when an engagement is ending, winding down, paused indefinitely, or a final invoice is going out — especially when a last fix is treated as the finish line, when either side wants to skip the process, or when a deadline, fatigue, or same-day payment pushes toward wrapping up tonight.
---

# Project closeout — shipping is not ending

Finishing the work and ending the engagement are different events; only one is technical. Until every account sits with the client and your access is verified gone, you remain an admin on someone else's production. Closeout is `dev-handoff` for keys, not code.

## Rules that override your defaults

1. **A skip request from your own side is pressure, not permission.** Fatigue, sunk hours, and tonight's payment are motives, not a waiver. Only the client can decline a transfer, in writing.
2. **Compression is fine; omission is not.** A 24-hour closeout is real closure if every step was performed and evidenced — elapsed time is never the criterion. What you cannot evidence ships as a named open item, never as complete.

## Procedure

### 1. Separate the final task from closeout
The last fix (`bug-triage`) and the closeout are different deliverables. Send two messages — fix confirmation first, closeout second — so neither reads as closing the other.

### 2. Inventory every account you touch
Each with your role: **owner / admin / member / none**. Payments, hosting, source control, DNS, error tracking, CI, secret stores — everything from `client-onboarding`. Sole owner or admin anywhere is a live liability; a payment processor is a security-review trigger — flag it, don't patch past it.

### 3. Transfer ownership before removing anything
The client takes an owner seat on each system, confirmed by their login. Then rotate every secret you held, scheduled so production doesn't break — resignation does not revoke possession. Never put credential values in chat or docs; use the provider's invite flow.

### 4. Hand off a runbook
What runs where, deploy and rollback (`deploy-verify`), scheduled jobs, alert routing, gotchas, recurring costs and renewal dates, what changed. Code walkthrough is `dev-handoff`; this is the operating manual.

### 5. Get written acceptance
Ask for an explicit reply to the closeout record — a sentence you can quote later, not an assumed yes or a deploy thumbs-up. When anyone wants to skip it is exactly when you need it. Later asks are new work: `scope-check`, then `quote-job`.

### 6. Remove your access, then verify it
Remove yourself, attempt to log in, confirm denial, record the evidence. Intent to remove is not removal.

### 7. Invoice against acceptance
Via `invoice-prep`, citing the acceptance message and date. No acceptance yet? Send a `status-update`, not an invoice.

## Output template
```
CLOSEOUT — <engagement>

| System | Role | Transferred | Secrets rotated | Access removed |
|---|---|---|---|---|
| <name> | <role> | <Y, date> | <Y, date> | <Y — login denied, date> |

Runbook: <link>
Delivered: <list> · Left open: <list>
Reply "accepted" to confirm handoff complete. Invoice follows acceptance.
```

## Red flags — STOP, the engagement is still open
- "The bug is fixed, so we're done" — no transfer step between fix and finish
- Invoice tied to the work landing, not written acceptance
- No inventory, or still sole owner of payments, DNS, hosting
- No runbook — nothing written on how to run what you built
- Access removal promised but not performed and re-tested
- "Don't bother with the checklist, I trust you" — trust is not a transfer
- You are the one arguing to skip it: tired, owed money, months in
- Demo tomorrow, payment tonight, sunk hours — transfer collapsing into a same-night send
- A step marked done because the deadline passed, not because it was evidenced
- A payment or credential surface never flagged as security-sensitive
- "Glad we closed this out cleanly" without checking transfer, runbook, acceptance

## Failure modes this prevents
- Paged a year later as the only admin on the client's payment account
- Invoice disputed because "done" was never defined in writing
- Operating knowledge left in your head, re-billed later as emergency support
