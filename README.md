# freelance-skills

**An open-source agent skills pack for freelance software engineers.** Works with Claude Code, Cursor, Codex, and any tool that reads the [Agent Skills](https://agentskills.io) format.

Freelancing is two jobs: the engineering, and everything around it — learning a stranger's codebase fast, quoting work you haven't done yet, proving deploys landed, keeping clients updated, and taking over systems from developers who are walking out the door. This pack makes your coding agent genuinely good at the second job.

These skills are distilled from real solo-freelancer practice on live client products — not theory. Each one encodes a discipline that was learned the expensive way, and each ends with the failure modes it exists to prevent.

## The skills

| Skill | Triggers when… | The discipline |
|---|---|---|
| [`client-onboarding`](skills/client-onboarding/) | you take on a new client or inherit an unfamiliar repo | Parallel inventory → a written project brief. Knowledge that only lives in one session is knowledge you'll re-bill for |
| [`quote-job`](skills/quote-job/) | you need to quote, estimate, or answer "how long will this take?" | **Evidence, not AI intuition** — calibrate from git history, price by analogy, split parallelizable from wall-clock-bound, never anchor on someone else's number |
| [`scope-check`](skills/scope-check/) | a client ask arrives that will take more than an hour | Restate the ask before starting. One "here's my read — confirm?" beats three rounds of rework |
| [`bug-triage`](skills/bug-triage/) | you have a bug report, error, or complaint to investigate | Verify the premise before the fix. A third of reports are wrong about the cause — a refuted ticket closed with evidence is a win |
| [`deploy-verify`](skills/deploy-verify/) | right after any deploy | Prove the release landed, migrations are even, and the live endpoint serves the change. Log tails lie |
| [`status-update`](skills/status-update/) | a client asks "where are we at?" | Outcomes, not diffs. Investigation weeks are real progress; "blocked on you" is its own section |
| [`invoice-prep`](skills/invoice-prep/) | it's time to bill | Reconcile time log × git × tickets; explain variance before the client finds it |
| [`dev-handoff`](skills/dev-handoff/) | you're taking over from a departing developer | Capture access, rituals, and the questions you don't know to ask — **before their last day** |

## Install

### Claude Code

**As a plugin (recommended — auto-updates, all eight skills):**

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
