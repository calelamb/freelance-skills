---
name: bug-triage
description: Use when the user has a bug report, error, or customer complaint to investigate — especially when the report already names a cause or a file, or when the user is in a hurry and asks you to "just fix it."
---

# Bug triage — verify the premise before the fix

Roughly **a third of bug reports are wrong about something important**: the cause, the location, sometimes whether the bug exists at all. A fix built on a wrong premise ships confidently and fixes nothing — or changes correct behavior to match a mistaken report. No code until the defect is reproduced on current code.

## Procedure

### 1. Reproduce or refute — nothing else first
- Reproduce on the **current** version, not the version from when the report was filed. Bugs get fixed incidentally by unrelated work.
- Doesn't reproduce? Say so with evidence (what you ran, what you saw) and stop. **A refuted report closed with evidence is a completed job.** Clients respect "already fixed on [date]" more than a phantom fix.

### 2. Distrust the diagnosis, keep the symptom
The symptom (what the user saw) is nearly always real. The explanation is where reports go wrong. Treat the reporter's theory — including any file or function they named — as one hypothesis among several.

### 3. Locate the actual divergence
- Two sources disagree? Fetch both for the same input and diff. The divergence point identifies the owner.
- Check data age. "The number is wrong" is often "the number was right when computed, months ago, and nothing refreshes it." Stale-but-once-true is a different bug class with a different fix.
- Check boundaries: the third-party API's *documented* response vs. what the code assumes (one observed response is not the contract), null/empty handling, unit and scale mismatches.

### 4. Fix with a test that pins the symptom
Failing test first, at the level the user experienced it: if the report was "the button does nothing," the test clicks the button. Then fix. Then **mutation-check**: revert the fix, confirm the test goes red. A test that passes either way manufactures false confidence.

### 5. Close with evidence
State: what was reported · what was actually true · the fix or the refutation · proof from the live environment. Keep the forward fix separate from any cleanup of already-affected records — different deliverables, different risks.

## Red flags — STOP, you're fixing the theory
- You opened the file the reporter named before reproducing anything
- "The fix is obvious, reproducing is a waste of time"
- The user said "just get it done" and you skipped step 1
- Your test passes with the fix reverted
- You changed behavior to match the report without checking which side was right

## Failure modes this prevents
- Fixing the reporter's theory instead of the bug
- "Fixed" tickets for bugs that were already gone (billed hours for nothing)
- Correct behavior changed to match a mistaken report
- Regression tests that assert nothing and rot green
