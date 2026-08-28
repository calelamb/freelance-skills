---
name: incident-response-solo
description: Use when production is down or degraded for a live client, the user is the only engineer on it, and the client is asking for updates — including out-of-hours outages, a suspect recent deploy, or pressure not to roll back because the broken release contains paid-for work.
---

# Solo incident response: communicate first, restore second, diagnose third

An outage is two incidents: the technical one, and the client's experience of it, which silence destroys: forty minutes of nothing reads as abandonment. Restoring service is not understanding the failure: roll back first, diagnose on a healthy system.

## Procedure

### 1. Client message within 10 minutes, before debugging
Three parts: **known / next / when**. Promise the next update, never a cause or an ETA. Draft the text yourself; never hand that obligation back while you debug. Nothing known yet? That is the message.

### 2. Restore before you understand
Default first move: **rollback to the last known-good release**, cause known or not. Rollback is reversible; a live patch under pressure is not. State it out loud and get an explicit yes or no. Never silently adopt patch-forward.

### 3. No access? Hand over, never substitute
When the user holds prod access and the only client channel, the artifact changes, not the order: deliver a verbatim client message plus the exact rollback ask, marked send now, then stop. Never substitute log reading for the blocked step; never run a prod-mutating command without explicit go-ahead.

### 4. Name the sunk cost, then ask and wait
"That release has a weekend of work in it" is sunk cost, not a technical argument. The code loses nothing by redeploying in an hour; revenue lost meanwhile never returns. Tired operators pick the reversible option. Never assume the refusal, or concede it before it is given.

### 5. If the refusal stands
A documented no is recorded, not re-litigated. Log who refused and when, state the cost in one line, then patch forward under constraints: smallest reversible change, no destructive migration, backup before any schema write, update cadence halved. Reoffer rollback the moment a patch attempt fails.

### 6. Timeline as you go, not from memory
Open a scratch file at minute one; append a timestamped line per event: first symptom, first report, updates sent, rollback proposed and answered, hypotheses and results, fix shipped. A reconstructed timeline is a guess; this one is the postmortem, the billing record, and the evidence if fault is disputed.

### 7. Once restored: diagnose, then account for it
Hand the defect to `bug-triage`, reproduce before theorising, and ship through `deploy-verify`. Within 48 hours send a short, blameless postmortem: what broke, why, customer impact, what prevents recurrence. Prevention work bigger than a test goes through `scope-check`, priced with `quote-job`; resume cadence with `status-update`.

## Output template

```
CLIENT UPDATE — <time>  (send verbatim, now)
Known: <symptom> affecting <who> since ~<time>.
Next:  <rolling back to release X> / <awaiting your go-ahead to roll back>.
When:  next update by <time, ≤30 min out>, progress or not.

DO NOW — <who acts>: <exact command or ask>

TIMELINE (append live)
<hh:mm> first symptom · <hh:mm> client reported · <hh:mm> update sent
<hh:mm> rollback proposed, approved/refused by <who>
<hh:mm> restored, verified by <check>
<hh:mm> hypothesis <one line>, confirmed/refuted
```

## Red flags — STOP

- Reading logs with no client message drafted
- "I'll update them once we know what's wrong"
- "Do NOT roll back" accepted without proposing it and naming the tradeoff
- Refusal assumed, or dropped after one soft no
- Unshipped work steering the restore, nobody saying "sunk cost"
- Patch-forward planned, rollback never offered as safer
- Late, operator tired, change underway irreversible
- Missing access used as licence to debug rather than hand over
- Timeline to be written afterwards, from memory
- No "known / next / when" at any checkpoint
- No postmortem, no 48-hour commitment
- You handed the client off and kept the code

## Failure modes this prevents

- Silent debugging that the client reads as abandonment
- Diagnosing on a burning system when rollback would have bought an hour
- Sunk-cost pressure dressed up as a technical argument
