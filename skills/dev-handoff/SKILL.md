---
name: dev-handoff
description: Capture everything a departing developer knows before their last day — access inventory, deploy rituals, tribal knowledge, and the questions you don't know to ask. Use when the user is taking over systems from a developer who is leaving, was fired, or is being offboarded.
---

# Dev handoff — capture it before it walks out the door

When a developer leaves, the code stays and everything else leaves with them: which dashboard has the billing webhooks, why deploys have that one weird step, which customer's account is special. This knowledge has a hard expiry date — their last day — and every question you fail to ask before it costs 10× to rediscover after. This skill is a race, run in priority order.

## Priority order (highest expiry-cost first)

### 1. Access inventory — do this first, it gates everything
Build the checklist by walking the actual systems, not memory:
- Server access: SSH keys, server user accounts, which machines exist at which IPs (verify against live DNS — documented IPs drift from real ones)
- Third-party dashboards: payments (Stripe/PayPal), email (SendGrid etc.), DNS registrar, hosting, monitoring, error tracking
- **Marketplace/developer accounts** — app-store and plugin-marketplace accounts (Webflow, Framer, Shopify, Chrome Web Store). These are the most-forgotten and least-recoverable: if the listing lives under the departing dev's personal email, your distribution channel dies with their access. Transfer ownership, not just credentials.
- Repo hosting: org membership, deploy keys, CI secrets, webhook configs
- For each: transfer to owner-controlled accounts. **Never store or paste credential values in chat or notes** — the departing dev rotates or transfers through each service's own mechanism; you record only *what exists and where*.

### 2. The rituals — watch, don't ask
Have them perform one full deploy end-to-end while you record every step, including the ones they do without thinking — the pre-build patch script, the cache clear, the service name that's different in prod, the "always check X after." Ritual steps live in muscle memory, not docs, and the undocumented step is always the one that breaks the first solo deploy. Same for: DB backup + restore (actually restore one — an unverified backup is a hope, not a backup), cron/scheduled-job inventory (what runs, when, what happens if it doesn't), and any release process for the marketplace apps.

### 3. The questions you don't know to ask
Work through these with them verbatim:
- "What breaks most often, and what do you do when it does?"
- "What would you never touch, and why?"
- "Which customers/accounts are special-cased anywhere?"
- "What's half-finished right now, on what branch?"
- "What do you know is wrong but never got to?"
- "If the system pages at 2am, what's it most likely to be?"
- "What does nobody else know they'd need to know?"

### 4. Environment truth
Diff documented config against reality: `.env` files on each box vs. examples in the repo; DNS records vs. documented IPs; PM2/systemd service names per environment (dev and prod names often differ — using the wrong one silently no-ops). Capture the real ones.

### 5. Deliverable
A handoff document (in the repo, e.g. `docs/HANDOFF-<name>-<date>.md`): access inventory with transfer status per item · verified rituals as copy-paste runbooks · the Q&A answers verbatim · environment truth · a red-flag list of everything that couldn't be verified before they left. That last list is the honest residue — it's next month's incident forecast, and pretending it's empty helps no one.

## Failure modes this prevents
- The marketplace listing orphaned under a departed dev's personal email
- The first solo deploy failing on the ritual step nobody wrote down
- Backups that were never once restored, discovered during the incident
- "Why is this customer special-cased?" archaeology, twelve billable hours at a time
- Paying to rediscover, one outage at a time, what one afternoon of questions would have captured
