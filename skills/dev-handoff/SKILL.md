---
name: dev-handoff
description: Use when the user is taking over systems from a developer who is leaving, was let go, or is being offboarded — or when a client says "our last dev is gone" — while that developer is still reachable, since every day of delay is lost knowledge.
---

# Dev handoff — capture it before it walks out the door

When a developer leaves, the code stays and everything else leaves with them: which dashboard has the billing webhooks, why deploys have that one weird step, which customer's account is special. This knowledge expires on their last day, and every question not asked before costs 10× to rediscover after. This is a race, run in priority order.

## Priority order (highest expiry-cost first)

### 1. Access inventory — first, it gates everything
Build the checklist by walking the actual systems, not memory:
- Servers: SSH keys, user accounts, which machines at which IPs (verify against live DNS — documented IPs drift)
- Third-party dashboards: payments, email, DNS registrar, hosting, monitoring, error tracking
- **Marketplace/developer accounts** (app stores, plugin marketplaces, Chrome Web Store, Shopify/Webflow/Framer). Most-forgotten and least-recoverable: if the listing lives under the departing dev's personal email, the distribution channel dies with their access. **Transfer ownership, not just credentials.**
- Repo hosting: org membership, deploy keys, CI secrets, webhook configs
- For each: transfer to owner-controlled accounts. **Never store or paste credential values in chat or notes** — rotate/transfer through each service's own mechanism; record only *what exists and where*.

### 2. The rituals — watch, don't ask
Have them perform one full deploy end-to-end while you record every step, including the ones done without thinking — the pre-build patch script, the cache clear, the service name that differs in prod. The undocumented step is always the one that breaks the first solo deploy. Same for: DB backup **and restore** (actually restore one — an unverified backup is a hope), cron/scheduled-job inventory, and any marketplace release process.

### 3. The questions you don't know to ask
Ask verbatim, record verbatim:
- "What breaks most often, and what do you do when it does?"
- "What would you never touch, and why?"
- "Which customers/accounts are special-cased anywhere?"
- "What's half-finished right now, on what branch?"
- "What do you know is wrong but never got to?"
- "If the system pages at 2am, what's it most likely to be?"
- "What does nobody else know they'd need to know?"

### 4. Environment truth
Diff documented config against reality: `.env` on each box vs. examples in the repo; DNS vs. documented IPs; PM2/systemd service names per environment (dev and prod names often differ — the wrong one silently no-ops).

### 5. Deliverable
`docs/HANDOFF-<name>-<date>.md` in the repo: access inventory with transfer status per item · verified rituals as copy-paste runbooks · Q&A verbatim · environment truth · **a red-flag list of everything that couldn't be verified before they left.** That last list is next month's incident forecast; pretending it's empty helps no one.

## Red flags
- You're reading code while the departing dev is still available to answer questions
- An access item is "transferred" but the owner can't log in without the old dev
- A backup exists but has never been restored
- A credential value is in the handoff doc

## Failure modes this prevents
- The marketplace listing orphaned under a departed dev's personal email
- The first solo deploy failing on the ritual step nobody wrote down
- Backups that were never once restored, discovered during the incident
- "Why is this customer special-cased?" archaeology, twelve billable hours at a time
