---
name: subcontractor-brief
description: Use when another developer, contractor, or agency is being brought onto the user's client work, or when subcontracted work is coming back to be merged, deployed, invoiced, or reported to the client — especially under deadline pressure, fatigue, or when the subcontractor is trusted and says it is done.
---

# Subcontractor brief — your name is on their work

The client bought your judgment, not the subcontractor's. Their "done and tested" is a **claim**, not a verification; unreviewed, it becomes your verified deliverable and your liability. Past good work sets your risk tolerance; it never replaces checking this specific piece. Nothing reaches the client that you have not checked yourself.

## Procedure

### 1. Write the brief before they start
Name the deliverable, the branch, and what is **out** of scope. Write the review gate in as an acceptance condition, not a courtesy. Price their piece with `quote-job`; hold the boundary against client scope with `scope-check`.

### 2. Grant access without sharing your credentials
Their own named accounts, least privilege, expiry. Never your SSH key, your logins, or a raw secrets file — a shared `.env` hands over every credential you hold, permanently and unrevocably. No deploy rights to client-facing environments. `dev-handoff` for context, `client-onboarding` for issuing credentials properly. Bad access that already exists gets flagged in writing immediately — that flag never blocks starting the review, it rides alongside it. Name the fix (rotate those secrets, reissue least-privilege access) as required before their next work ships, and leave executing it to the user; never change credentials yourself.

### 3. Keep the communication boundary
They report to you; you report to the client — a side channel makes you responsible for statements you never made. If they have spoken to the client directly, name it back as a boundary correction: one factual line, no blame, fixing the channel going forward. That correction does not pause work in flight, but anything they told the client that you have not verified gets corrected with the client before your gate closes.

### 4. Run the review gate yourself
Read the diff line by line. Independently reproduce what they claim — your own run, at the level the client sees it. `bug-triage` if the work was a fix, `deploy-verify` after any deploy. Under deadline or exhaustion the gate is **scoped down** (diff read plus one targeted smoke test), never skipped. If even that will not fit before a hard external deadline, the work does not ship: tell the client before the deadline that it is unverified and what that risks, then let them choose — move the date, ship the last known-good version, or accept unverified work in writing.

### 5. Separate the irreversible actions
Merge, deploy, client message, invoice approval: four decisions, not one batch. Checkpoint between each.

### 6. Report what you verified, in your words
Use `status-update`: what you checked, and what remains unverified — never forward their self-report as fact. Then check the invoice's hours and scope against work you reviewed and accepted before approving it with `invoice-prep`.

## Output template
```
BRIEF — <scope id>
Deliverable: <what, which branch> · Out of scope: <what they must not touch>
Access: <named account, least privilege, expiry> · NOT granted: <prod, client envs, secrets files>
Comms: to me only · Bill: <rate/cap>, invoice references this brief

REVIEW GATE (me, before anything moves)
Diff read: <files, date> · Reproduced independently: <what I ran, what I saw>
Access/secrets check: <no new creds> · Verdict: accept / rework <what>

RELEASE
Merged <sha> → <env> · Deploy verified: <proof>
Client told: <what I verified> · Unverified: <what, and the client's decision on it>
Invoice: <hours vs. accepted work> · approved <y/n>
```

## Red flags — STOP, you are lending your name
- Code merged or deployed before you read the diff line by line
- "Done" reported to the client on their self-report — their claim repeated as your fact
- "They've done fine work before" standing in for checking *this* piece
- An invoice approved without checking hours and scope against reviewed work
- They hold your SSH key or a raw secrets file and you never flagged it
- "Client wants it live" + "they say it's ready" collapsed into "push now"
- Fatigue or a penalty clause used to skip the gate instead of shrinking it
- The gate would not fit the deadline, so it shipped unverified instead of the client being told
- The client heard it from them, not you, and you let it pass
- Merge, deploy, client message, and invoice approval in one batch

## Failure modes this prevents
- Subcontractor work reaching the client unreviewed under your name
- An unverified claim laundered into your verified deliverable
- Permanent, unrevocable credential access with no audit trail
- A bad or malicious change deploying straight into a client-facing environment
