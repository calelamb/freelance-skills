---
name: deploy-verify
description: Post-deploy verification ritual — prove the release actually landed, migrations are even with code, and the live endpoint serves the change. Use after any deploy, or when the user asks whether a deploy worked.
---

# Deploy verification — deploys are claims until proven

The worst deploy failures are silent: the push that went to the wrong remote, the CI that's billing-lapsed and runs nothing on merge, the migration that never ran, the build that landed while the git client printed a connection error. "I deployed it" is a claim. This ritual converts it to a fact.

## The ritual

### 1. Prove the release landed
Confirm the platform registered a NEW release with the expected commit:
```bash
heroku releases --app <app> | head -3        # or your platform's equivalent
```
Match the SHA to what you pushed. **Do not trust the git client's output in either direction** — a connection-reset error can print after the build already succeeded, and a "successful" push to the wrong remote deploys nothing. The platform's release list is the truth.

### 2. Migrations even with code
```bash
heroku run rails db:migrate:status --app <app> | tail -5
```
Code that references a column its database doesn't have yet crashes at request time, not deploy time. If the platform doesn't auto-migrate (many don't, and some auto-deploy setups skip it), run migrations NOW, not "when someone notices."

### 3. The endpoint is authoritative; logs are not
Hit the real environment and confirm the actual change:
```bash
curl -s https://<the-live-url> | grep '<the-new-pattern>'
```
Grep the **rendered output** for the thing you changed — this catches the wrong-file fix that passed every test. Log tails are supplementary only: buffered logs routinely replay errors from BEFORE the fix landed and have burned real hours twice in recorded history. Never conclude failure from a log tail alone.

### 4. Smoke the money path
Whatever this client's users pay for — signup, checkout, the core report — exercise it once in the browser on the live environment. Tests passing and the customer flow working are different facts.

### 5. Watch, briefly and honestly
10–30 minutes proportional to risk: error rates, queue depths, 5xx counts. Capture the rollback command **before** you need it — if you can't state how to undo the deploy, the deploy wasn't ready. If a real signal appears, roll back first and diagnose after; a rollback on a real signal is correct behavior, not failure.

### 6. Record it
Wherever this client tracks work: release number, SHA, migration status, the verification evidence. "Deployed and verified: v128, abc1234, migrations even, live check passed" is one line, and it's the difference between a record and a memory.

## Failure modes this prevents
- The push that went to the wrong remote while everyone believed it shipped
- Merges silently deploying nothing because CI is broken or billing-lapsed
- Deployed code + un-run migration = crash discovered by a customer
- Reverting a good deploy because a stale log tail replayed old errors
- The wrong-file fix that passed tests but never reached the rendered page
