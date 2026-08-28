---
name: security-baseline-audit
description: Use when the user takes over an inherited system, codebase, server, or cloud account from a prior developer — or when leaked secrets, open admin routes, stale dependencies, or missing backups surface mid-task, especially under demo pressure or when the client calls security "a later problem."
---

# Security baseline audit — identify and report, never exploit

Inheriting a system means inheriting the blame for its breach. The deliverable is a **written, prioritized findings memo the client can read and fund** — not a pile of quiet fixes. Enumerate, confirm, rate, report. Never exploit, pivot, or dump data to "prove impact," and never touch what the client did not grant access to — out-of-scope surfaces are memo lines, not commands you run.

## Procedure

### 1. Sweep the whole surface, timeboxed — not the reported issue
One leaked key is a sample, not the surface. **Cap enumeration at 90 minutes, or 15% of the clock before a live deadline, whichever is smaller** — then triage. Anything unreached is logged `unknown`, never assumed clean. Mark each present / absent / unknown:
- secrets in the working tree **and** git history, CI logs, built images
- admin, debug, and unauthenticated routes; public buckets
- dependency and platform patch level (read advisories; do not upgrade yet)
- backups: age, encryption, whether a restore has **ever** been tested
- single points of failure: one server, one key, no staging, no rollback
- IAM: wildcard roles, shared logins, ex-contractor access still live

### 2. Treat any exposed credential as already compromised
A key committed at any point is compromised for the repo's life; deleting it from current files changes nothing. Capture triage evidence first — when it landed, who had clone access, whether provider logs show use. Then **rotate → revoke → purge history** (filter-repo/BFG, on client go-ahead, coordinated with every clone holder). Record findings, never values.

**Once rotated and revoked the old key is dead** — keep working in and handing off the repo normally before the purge. Purge is its own ticket, named owner and date, carried in the memo as open until it lands.

### 3. Rate by exposure, not by how interesting the bug is
Severity = internet-reachable? × credential and data blast radius × compensating controls. **No tested restore and no rollback path are critical findings in their own right**, independent of any demo date.

### 4. Separate "fix now" from "fund next" — never blind-upgrade
A bulk upgrade before a launch is an outage dressed as a security fix. Patch only reachable advisories, one at a time, breaking changes read, rollback ready, verified with `deploy-verify`. **No staging is never a reason to skip verification**: substitute a feature-flagged or canary rollout, revert command tested and in hand before the push, then verify on prod. The rest are funded line items — price with `quote-job`; beyond agreed scope, run `scope-check`.

### 5. Deliver the memo; put every deferral in writing
"Later problem" is the client's call to make, not yours to absorb silently. The memo ships regardless, deferrals recorded as accepted risk, named owner, date. Send via `status-update`; feed access gaps into `client-onboarding` or `dev-handoff`.

## Output template
```
SECURITY BASELINE — <system> · <date> · <hours spent>
Audited: <repos, envs, accounts> · Not audited: <what, why>
Method: read-only enumeration; no exploitation performed.

| # | Finding | Severity | Exposure | Effort | Status |
|---|---|---|---|---|---|
| 1 | <finding> | Critical | <blast radius> | <hours> | <fixed / open / deferred> |
| 2 | <finding> | High | <blast radius> | <hours> | <fixed / open / deferred> |

Fixed during audit: <item — commit SHA, how verified>
Recommended now (funded): <item — cost, why it can't wait>
Deferred at client request: <item> — accepted risk, owner <client>, <date>
Unknown / not reached in timebox: <area — what it would take to check>
```

## Red flags — STOP, you are absorbing someone else's liability
- Remediation started before one prioritized finding was written down
- Untested change to prod — no staging, no rollback, "the demo is tomorrow" — and no 15-minute compromise offered (flag, canary, revert)
- A secret deleted from current files and called handled — never rotated, history never purged
- "Backups and restore testing are a later problem"
- `audit fix --force` or a whole-tree upgrade whose breaking changes you never read
- You checked the one endpoint named and swept no other routes, roles, or accounts
- The client waved off the review and you agreed without writing down the residual risk
- You remediated without noting who else had access or whether the key was used
- Nothing in your output says what remains open and who owns it
- "Don't overthink it" ended the discussion instead of starting a written one

## Failure modes this prevents
- Blamed for a breach on the system you inherited and never audited
- Secrets "removed" but still live in history forever
- The security fix that becomes the outage
- One reported issue mistaken for the whole attack surface
- A verbal deferral converted into the freelancer's liability
- The first restore test happening during a real disaster
