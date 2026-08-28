---
name: scope-check
description: Restate a client's request back to them before starting multi-step work — what they want, what "done" looks like, what's explicitly out. Use when the user receives a client ask (Slack/email/ticket) that will take more than an hour, or before starting any ambiguous request.
---

# Scope check — restate before you build

The most expensive work a freelancer does is the right solution to the wrong request. Ambiguity discovered at delivery costs a full round trip; ambiguity discovered before starting costs one message. This skill turns every multi-step client ask into a confirmation message first.

## Procedure

1. **Extract the ask** from wherever it arrived (Slack thread, email, ticket). Quote the client's actual words — paraphrase drift is where scope creep starts.
2. **Write the restatement** in exactly this shape:
   > My read: (1) you want **[specific deliverable]**, (2) done looks like **[observable outcome the client can check]**, (3) NOT in scope this round: **[the adjacent things they might be assuming]**. Confirm before I start?
3. **Surface the forks.** If the request has a genuine either/or (which environment, which of two behaviors, rebuild vs patch), list the options with one-line trade-offs and your recommendation. Don't silently pick.
4. **Flag the invisible costs** the client can't see from outside: migrations, third-party approval waits, testing time on money paths. If done right, these appear in the confirmation, not the invoice dispute.
5. **Wait for the yes** on anything ambiguous. For requests that are genuinely unambiguous, skip the ceremony — this skill is for the other 60%.

## Calibration
The restatement should take under five minutes to produce. If writing it takes longer, that itself is the signal: the request is more ambiguous than anyone realized, and you just saved a build-iterate-rebuild cycle.

## Failure modes this prevents
- Three rounds of rework because "make the dashboard better" meant something specific
- The client assuming the adjacent feature was included; you assuming it wasn't
- Silent design decisions the client discovers at delivery and re-litigates
- Invoice disputes rooted in work the client never saw coming
