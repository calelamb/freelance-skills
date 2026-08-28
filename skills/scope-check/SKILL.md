---
name: scope-check
description: Use when a client request arrives (Slack, email, ticket, call notes) that will take more than an hour of work, before any code is written — especially requests phrased as outcomes ("make it better", "fix the dashboard") rather than specifics.
---

# Scope check — restate before you build

The most expensive work a freelancer does is the right solution to the wrong request. Ambiguity found at delivery costs a full round trip; ambiguity found before starting costs one message.

## Procedure

1. **Extract the ask verbatim.** Quote the client's actual words — paraphrase drift is where scope creep starts.
2. **Write the restatement** in exactly this shape:
   > My read: (1) you want **[specific deliverable]**, (2) done looks like **[observable outcome you can check yourself]**, (3) NOT in this round: **[the adjacent things you might be assuming]**. Confirm before I start?
3. **Surface the forks.** Genuine either/or (which environment, which of two behaviors, rebuild vs patch)? List options with one-line trade-offs and your recommendation. Never silently pick.
4. **Flag invisible costs** the client can't see from outside: migrations, third-party approval waits, testing on money paths. They belong in the confirmation, not the invoice dispute.
5. **Wait for the yes.** Draft the message for the user to send; do not start building on an assumed answer.

## When to skip it
Requests that are genuinely unambiguous (a typo, a specific one-line change with a clear target). If you're unsure whether it's ambiguous, it is — this skill is for the other 60%.

## Calibration
The restatement should take under five minutes. If it takes longer, that *is* the finding: the request is more ambiguous than anyone realized, and you just saved a build-iterate-rebuild cycle.

## Red flags — STOP and restate
- "I'll just start and adjust when they respond"
- The user is in a hurry, so you filled in the blanks yourself
- The "done" criterion is something only you can observe
- You picked one branch of a fork because it seemed obvious

## Failure modes this prevents
- Three rounds of rework because "make the dashboard better" meant something specific
- The client assuming the adjacent feature was included; you assuming it wasn't
- Silent design decisions the client discovers at delivery and re-litigates
- Invoice disputes rooted in work the client never saw coming
