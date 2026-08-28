# freelance-skills

**An open-source agent skills pack for freelance software engineers.** Works with Claude Code, Cursor, Codex, and any tool that reads the [Agent Skills](https://agentskills.io) format.

Freelancing is two jobs: the engineering, and everything around it — learning a stranger's codebase fast, quoting work you haven't done yet, proving deploys landed, keeping clients updated, and taking over systems from developers who are walking out the door. This pack makes your coding agent genuinely good at the second job.

These skills are distilled from real solo-freelancer practice on live client products — not theory. Each one encodes a discipline that was learned the expensive way, and each ends with the failure modes it exists to prevent.

## The skills

Twenty-four skills covering the whole engagement lifecycle. Each is a single `SKILL.md`: a core principle, a procedure, an output template where there's a deliverable, a **Red flags — STOP** list of the rationalizations an agent reaches for under pressure, and the failure modes it exists to prevent.

### Before the engagement

| Skill | Use when… | The discipline |
|---|---|---|
| [`client-vetting`](skills/client-vetting/) | evaluating a prospect, before any call, repo look, or "quick estimate" | Score the red flags (previous dev vanished, no budget stated, work before paperwork). Need changes the terms you accept, never the threshold |
| [`quote-job`](skills/quote-job/) | you need to quote, estimate, or answer "how long will this take?" | **Evidence, not AI intuition** — calibrate from git history, price by analogy, split parallelizable from wall-clock-bound, never anchor on someone else's number |
| [`billing-model`](skills/billing-model/) | choosing fixed-price vs hourly vs retainer | Fixed price only with confirmed scope *and* a measured analog; a stated budget is an anchor, not evidence |
| [`proposal-write`](skills/proposal-write/) | turning a quote into something the client signs | Problem in their words, approach, milestones, ranges, assumptions, explicit exclusions — never a bare number |
| [`contract-review`](skills/contract-review/) | a SOW/MSA lands in your inbox | The seven clauses that bite: IP over your own tooling, unlimited revisions, net-60+, acceptance with no deadline, restraints, indemnity, termination |

### Starting

| Skill | Use when… | The discipline |
|---|---|---|
| [`access-request`](skills/access-request/) | day one, before billable work | One message listing every repo, env, dashboard, and decision-maker you need — credentials via a proper mechanism, never chat |
| [`client-onboarding`](skills/client-onboarding/) | you take on a new client or inherit an unfamiliar repo | Parallel inventory → a written project brief. Knowledge that lives only in one session gets re-billed |
| [`dev-handoff`](skills/dev-handoff/) | taking over from a departing developer | Capture access, rituals, and the questions you don't know to ask — **before their last day** |
| [`security-baseline-audit`](skills/security-baseline-audit/) | first week on an inherited system | Secrets in history, exposed admin routes, untested backups, single points of failure → a prioritized memo the client can fund. Identify and report; never exploit |
| [`context-switch`](skills/context-switch/) | first session on client B after days on client A | Reload the brief, diff what changed on their remotes/prod/tickets, re-verify env names before touching anything |

### Building

| Skill | Use when… | The discipline |
|---|---|---|
| [`scope-check`](skills/scope-check/) | a client ask arrives that will take more than an hour | Restate the ask before starting. One "here's my read — confirm?" beats three rounds of rework |
| [`change-request`](skills/change-request/) | the ask grows mid-project | Quote the original confirmed scope, name the delta, price it separately, get a written yes before building |
| [`bug-triage`](skills/bug-triage/) | you have a bug report, error, or complaint to investigate | Verify the premise before the fix. A third of reports are wrong about the cause — a refuted ticket closed with evidence is a win |
| [`deploy-verify`](skills/deploy-verify/) | right after any deploy | Prove the release landed, migrations are even, and the live endpoint serves the change. Log tails lie |
| [`incident-response-solo`](skills/incident-response-solo/) | prod is down and you're the only engineer | First client message within 10 minutes, rollback before diagnosis, timeline as you go, postmortem within 48h |
| [`subcontractor-brief`](skills/subcontractor-brief/) | bringing another developer onto your client's work | Scope, their own access, a review gate before anything reaches the client under your name |

### Communicating and billing

| Skill | Use when… | The discipline |
|---|---|---|
| [`status-update`](skills/status-update/) | a client asks "where are we at?" | Outcomes, not diffs. Investigation weeks are real progress; "blocked on you" is its own section |
| [`client-education`](skills/client-education/) | explaining a technical decision or a delay to a non-technical client | Trade-offs as business outcomes, one decision at a time, no jargon and no condescension |
| [`weekly-review`](skills/weekly-review/) | your own Friday ritual | Hours vs quote per client, pipeline, what's blocked on clients, what to send Monday — catch the blown estimate before invoice day |
| [`expense-and-time-tagging`](skills/expense-and-time-tagging/) | logging time and expenses as they happen | A taxonomy that maps straight to invoice lines and tax categories; reconstruction undercounts |
| [`invoice-prep`](skills/invoice-prep/) | it's time to bill | Reconcile time log × git × tickets; explain variance before the client finds it |
| [`late-payment-followup`](skills/late-payment-followup/) | an invoice is overdue | Friendly → firm → work-pause → formal, with day offsets and drafts, so the second email actually gets sent |

### Closing the loop

| Skill | Use when… | The discipline |
|---|---|---|
| [`estimate-postmortem`](skills/estimate-postmortem/) | a job ships | Quoted vs actual per line, and *why* each missed — the feedback loop that makes `quote-job` real |
| [`project-closeout`](skills/project-closeout/) | an engagement ends | Transfer every account and ownership, hand off a runbook, remove your own access, tie the final invoice to written acceptance |

## Install

### Claude Code

**As a plugin (recommended — auto-updates, all 24 skills):**

```
/plugin marketplace add calelamb/freelance-skills
/plugin install freelance-skills@freelance-skills
```

Or from the shell: `claude plugin marketplace add calelamb/freelance-skills && claude plugin install freelance-skills@freelance-skills`.

**Manual (pick individual skills):**

```bash
git clone https://github.com/calelamb/freelance-skills.git
cp -r freelance-skills/skills/quote-job .claude/skills/      # this project only
cp -r freelance-skills/skills/quote-job ~/.claude/skills/     # every project
```

Claude loads a skill automatically when a task matches its description, or you can name it: *"use the quote-job skill for this."*

### Cursor

Cursor reads skills from `.cursor/skills/` (project) or `~/.cursor/skills/` (global). Easiest path is the [`skills`](https://skills.sh) CLI:

```bash
npx skills add calelamb/freelance-skills --agent cursor            # pick skills interactively
npx skills add calelamb/freelance-skills --agent cursor --all -g   # all skills, globally
```

Or copy folders by hand:

```bash
git clone https://github.com/calelamb/freelance-skills.git
mkdir -p .cursor/skills && cp -r freelance-skills/skills/* .cursor/skills/
```

The agent picks them up on the next chat; mention the skill name to invoke one explicitly.

### Codex (OpenAI Codex CLI)

Codex reads skills from `~/.agents/skills/` (global) or `.agents/skills/` in the repo:

```bash
npx skills add calelamb/freelance-skills --agent codex --all -g
```

Or by hand:

```bash
git clone https://github.com/calelamb/freelance-skills.git
mkdir -p ~/.agents/skills && cp -r freelance-skills/skills/* ~/.agents/skills/
```

Restart Codex; skills appear in `/skills` and are invoked by name or matched from your prompt.

### Everything else (Copilot, Gemini CLI, Windsurf, Cline, …)

```bash
npx skills add calelamb/freelance-skills --all      # installs into every detected agent
```

Or copy any `skills/<name>/` folder into your tool's skills directory. Each skill is a single self-contained `SKILL.md` — no scripts, no dependencies.

## Design principles

1. **Evidence over intuition.** Every skill forces the agent to ground claims in the repo, the history, or the live system — never in what "sounds right." `quote-job` exists specifically because AI effort estimates are unanchored guesses until calibrated against *your* measured throughput.
2. **Verify before acting.** Bug premises get reproduced before they get fixed. Deploys get proven, not assumed.
3. **The client sees outcomes.** Client-facing output (updates, invoices, quotes) speaks in features and results, never in commit hashes and refactors.
4. **Error bars are the product.** A quote or estimate without stated assumptions and confidence is worse than none.
5. **Red flags over rules.** Each skill lists the rationalizations an agent reaches for under time pressure ("just get it done", "the fix is obvious") so it can catch itself mid-shortcut.

## Contributing

PRs welcome. A good skill for this pack: a mundane, recurring freelance task with a *non-obvious discipline* that makes the difference between amateur and professional output. Include the failure mode the skill prevents — that's the part that makes it teachable. Descriptions start with "Use when…" and describe triggers, not the workflow.

## License

MIT
