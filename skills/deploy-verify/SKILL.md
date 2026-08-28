---
name: deploy-verify
description: Use when a deploy has just been run, on any platform (Heroku, Vercel, PM2/SSH, Docker, CI-driven), or when the user asks whether a deploy worked, before reporting "deployed" or "shipped" to anyone.
---

# Deploy verification — deploys are claims until proven

The worst deploy failures are silent: the push to the wrong remote, the billing-lapsed CI that runs nothing on merge, the migration that never ran, the build that landed while the git client printed a connection error. "I deployed it" is a claim. This ritual converts it to a fact.

## The ritual

### 1. Prove the release landed
Confirm the platform registered a **new** release with the expected commit — the platform's release list is the truth, not the git client's output (a connection-reset error can print after the build succeeded; a "successful" push to the wrong remote deploys nothing).

| Platform | Check |
|---|---|
| Heroku | `heroku releases --app <app> \| head -3` |
| Vercel / Netlify | `vercel ls <project>` / deploy dashboard → SHA |
| PM2 on a VPS | `ssh <host> 'cd <app> && git log -1 --format=%H && pm2 list'` |
| Docker / k8s | image tag or `kubectl rollout status` |
| GitHub Actions | the workflow run for this SHA is green *and actually ran a deploy step* |

### 2. Migrations even with code
E.g. `heroku run rails db:migrate:status --app <app> | tail -5`, `npx prisma migrate status`, or the framework equivalent. Code that references a column the DB doesn't have crashes at request time, not deploy time. If the platform doesn't auto-migrate (many don't), run migrations **now**.

### 3. The endpoint is authoritative; logs are not
```bash
curl -s https://<live-url>/<changed-page> | grep '<the-new-pattern>'
```
Grep the **rendered output** for the thing you changed — this catches the wrong-file fix that passed every test. Log tails are supplementary only: buffered logs routinely replay errors from *before* the fix landed. Never conclude failure from a log tail alone.

### 4. Smoke the money path
Whatever this client's users pay for — signup, checkout, the core report — exercise it once on the live environment. Tests passing and the customer flow working are different facts.

### 5. Watch, briefly and honestly
10–30 minutes proportional to risk: error rates, queue depths, 5xx counts. Write down the rollback command **before** you need it — if you can't state how to undo the deploy, it wasn't ready. On a real signal: roll back first, diagnose after. That's correct behavior, not failure.

### 6. Record it
One line wherever this client tracks work:
```
Deployed + verified: v128 · abc1234 · migrations even · live check: grep matched · money path OK
```

## Red flags — you have not verified
- "The push succeeded, so it's live"
- Checked logs but never hit the URL
- Migration "will run on the next deploy"
- Can't say what the rollback command is
- Reported "shipped" to the client before step 3

## Failure modes this prevents
- The push that went to the wrong remote while everyone believed it shipped
- Merges silently deploying nothing because CI is broken or billing-lapsed
- Deployed code + un-run migration = crash discovered by a customer
- Reverting a good deploy because a stale log tail replayed old errors
- The wrong-file fix that passed tests but never reached the rendered page
