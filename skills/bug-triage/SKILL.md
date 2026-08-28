---
name: bug-triage
description: Diagnose a reported bug by verifying its premise before writing any fix — reproduce first, refute with evidence when the report is wrong. Use when the user has a bug report, error, or customer complaint to investigate.
---

# Bug triage — verify the premise before the fix

In practice, roughly **a third of bug reports are wrong about something important**: the cause, the location, sometimes whether the bug exists at all. A fix built on a wrong premise ships confidently and fixes nothing — or worse, changes correct behavior to match a mistaken report. The discipline: no code until the defect is reproduced on the current code.

## Procedure

### 1. Reproduce or refute — nothing else first
- Reproduce the symptom on the **current** version. Not the version from when the report was filed — bugs get fixed incidentally by unrelated work.
- If it doesn't reproduce: say so with evidence (what you ran, what you observed) and stop. **A refuted report closed with evidence is a completed job**, and clients respect "this was already fixed on [date]" far more than a phantom fix.

### 2. Distrust the report's diagnosis, keep its symptom
The symptom (what the user saw) is nearly always real. The explanation (why they think it happened) is where reports go wrong. Investigate the symptom fresh; treat the reporter's theory as one hypothesis among several.

### 3. Locate the actual divergence
- Find where expected and actual behavior split. Two data sources disagreeing? Fetch both for the same input and diff — the divergence point identifies the owner.
- Check data age. "The number is wrong" is often "the number was right when computed, months ago, and nothing refreshes it." Stale-but-once-true is its own bug class with a different fix (bound the evidence age) than wrong-computation.
- Check the boundaries: the third-party API's actual response versus what the code assumes (read the provider's docs for the endpoint — the response you observed once is not the contract), null/empty handling, unit and scale mismatches.

### 4. Fix with a test that pins the symptom
Write the failing test first, at the level the user experienced it: if the report was "the button does nothing," the test clicks the button. Then fix. Then **mutation-check the test** — revert the fix and confirm the test goes red. A test that passes either way is worse than none: it manufactures false confidence.

### 5. Close with evidence
The close-out states: what was reported, what was actually true, the fix (or the refutation), and proof from the live environment — the reproduction failing where it used to succeed. Separate the forward fix from any data cleanup for already-affected records; they're different deliverables with different risks.

## Failure modes this prevents
- Fixing the reporter's theory instead of the bug
- "Fixed" tickets for bugs that were already gone (billed hours for nothing)
- Correct behavior changed to match a mistaken report
- Regression tests that assert nothing and rot green
