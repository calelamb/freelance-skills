---
name: access-request
description: Use when the user is starting a client engagement, needs repo, environment, dashboard, or account access, is blocked waiting on something the client hasn't provided, or is drafting a message asking a client for logins, keys, or permissions.
---

# Access request — one message, not twelve

Access arrives at the speed it is asked for. Asking piecemeal — repo today, staging tomorrow, the payment dashboard Thursday — turns a one-day setup into a week of unbillable drip-fed unblocking. Send one comprehensive request before the first billable hour, with a named owner on every line.

## Rules that override your defaults

1. **Credentials never travel through chat, email, or ticket comments.** Name one mechanism and require it — a password-manager share (1Password, Bitwarden, whatever they run) or an invite to their vault. "Whatever's easiest" is how a live key lands in a searchable forty-person channel; reading one aloud on a call is the same failure, not a fallback.
2. **Named accounts beat shared secrets.** Your own identity with 2FA wherever the tool supports it; a shared password is a per-item exception, never the default. Named accounts are also cleanly revocable at the end — see `dev-handoff`.
3. **Every line has an owner and a date.** A list with no person beside each item is a wish, not a request.
4. **Name the one person who can say yes** — authorize spend, grant admin, override an IT policy. Without a named approver the request sits in a queue nobody owns.
5. **Send the whole list.** A long list is an accurate list, not a rude one. Trimming it to seem considerate *is* the drip-feed failure, delayed by a week.
6. **Urgency moves dates, never rules.** A launch date, weeks already lost, or a client offering to work all night compresses the by-when column and nothing else. Rules 1 and 2 have no emergency exception and sunk cost is not one; "just this once" is what precedes the leak.
7. **A secret sent the wrong way is burned.** If one arrives by a banned channel anyway, don't use it — ask for a rotation, redelivery through the named mechanism, and the message deleted. Using it once ratifies that channel.

## Procedure

### 1. Sweep every category before writing
Code (repos, branch permissions, CI). Environments (staging, prod, SSH/VPN, database read). Infrastructure (hosting, logs, error monitoring). Domain and DNS (registrar, DNS host, certs, email records). Third-party accounts (payment processor and its billing owner, email/SMS, analytics, auth, storage, every API the app calls). Design assets (source files, brand kit, font licenses). Comms tools. People (approver, technical contact, escalation and after-hours path). A skipped category is next week's blocker.

### 2. Split required-to-start from required-later
Two tiers let the client sequence the work without shortening the list. A deadline sets the dates inside each tier; it never demotes an item or drops one. "We'll sort that nearer the time" is how a category goes missing.

### 3. State the reason and the level per item
"Read access to analytics to verify the funnel numbers" is approved faster than "analytics access," and stops you asking for admin where read is enough.

### 4. Track what actually arrives
Keep the list as a live checklist. Mark an item only after using it — clone the repo, log into the dashboard — never on the client's word. Report what is outstanding to the approver on a stated date, and log each delay as a dated schedule risk while it is still a scheduling note, not a missed deadline.

Broader kickoff work — scope, contract, comms cadence — belongs to `client-onboarding`.

## Output template
```
Subject: Access needed to start — <project>

Approver (can grant / authorize spend): <name>
Technical contact: <name> · Escalation + after-hours: <name>
Credential delivery: <one named mechanism, e.g. 1Password share to me@x>.
Please don't send secrets by chat, email, or ticket, or read them out on a call —
anything sent that way I'll ask you to rotate before I use it.

NEEDED TO START — blocks day one
| # | Access | Level | Why | Owner | By |
|---|---|---|---|---|---|
| 1 | Repo <name> | write + branch perms | <reason> | <name> | <date> |
| 2 | Staging env + deploy rights | deploy | <reason> | <name> | <date> |
| 3 | Error monitoring / logs | read | <reason> | <name> | <date> |

NEEDED BY <milestone>
| 4 | Payment processor (test mode) + billing owner | <level> | <reason> | <name> | <date> |
| 5 | Domain registrar + DNS host | <level> | <reason> | <name> | <date> |
| 6 | Design source files, brand kit, font licenses | <level> | <reason> | <name> | <date> |
| 7 | Analytics / email / auth / storage accounts | <level> | <reason> | <name> | <date> |

Preference: add me as a named user with my own login and 2FA wherever the tool
supports it; shared credentials only where it doesn't.
I'll confirm each item as it lands and flag whatever is still outstanding on <date>.
```

## Red flags — STOP, you are rebuilding the drip-feed
- Credentials pasted into chat "just this once, I'll keep them safe"
- A screen-share or read-it-aloud call offered as an alternative
- A key that arrived the wrong way got used instead of rotated
- Delivery left as "whatever's easiest for you"
- A deadline, or time already lost, moved an item off the day-one list
- Addressed to a group; nobody can approve it alone
- Items cut to keep the message short
- A category missing: payment processor, domain/DNS, third-party accounts, design assets, escalation contact
- Lines with no owner or date, or no check that items arrived

## Failure modes this prevents
- A week of half-access where nothing is billable and nothing finishable
- Live secrets sitting permanently in a chat archive or inbox
- A shared login nobody can revoke when the engagement ends
- A request that stalls because no named person owned it
- Second and third rounds of asking, from a list trimmed to look polite or shortened by a deadline
