# freelance-skills

**An open-source Claude skills pack for freelance software engineers.**

Freelancing is two jobs: the engineering, and everything around it — learning a stranger's codebase fast, quoting work you haven't done yet, proving deploys landed, keeping clients updated, and taking over systems from developers who are walking out the door. This pack makes Claude genuinely good at the second job.

These skills are distilled from real solo-freelancer practice on live client products — not theory. Each one encodes a discipline that was learned the expensive way.

## The skills

| Skill | What it does |
|---|---|
| [`client-onboarding`](skills/client-onboarding/) | Learn a new client's codebase in hours, not weeks — parallel inventory, feature map, deploy topology, and a project memory file as the deliverable |
| [`quote-job`](skills/quote-job/) | Quote from **evidence, not AI intuition** — mine git history for measured velocity, price by analogy, and never anchor on someone else's number |
| [`scope-check`](skills/scope-check/) | Restate the ask before starting. One round of "here's my read — confirm?" beats three rounds of rework |
| [`bug-triage`](skills/bug-triage/) | Verify the premise before fixing. Roughly a third of bug reports are wrong about the cause — a refuted ticket closed with evidence is a win |
| [`deploy-verify`](skills/deploy-verify/) | The post-deploy ritual: prove the release landed, migrations are even, and the live endpoint answers — log tails lie |
| [`status-update`](skills/status-update/) | Turn commits and tickets into a client-ready update in the client's language: outcomes, not diffs |
| [`invoice-prep`](skills/invoice-prep/) | Assemble the month's billables from work logs into a clean invoice summary the client won't question |
| [`dev-handoff`](skills/dev-handoff/) | Capture everything a departing developer knows **before their last day** — access, rituals, and the questions you don't know to ask yet |

## Install

**Claude Code:** copy any skill folder into your project's `.claude/skills/` (or `~/.claude/skills/` for all projects):

```bash
git clone https://github.com/calelamb/freelance-skills.git
cp -r freelance-skills/skills/quote-job .claude/skills/
```

**Cowork / Claude desktop:** add the skill folder via your skills directory, or zip a skill folder as `<name>.skill` and install it.

Claude picks skills up automatically when a task matches the skill's description — or invoke one directly by name.

## Design principles

1. **Evidence over intuition.** Every skill forces Claude to ground claims in the repo, the history, or the live system — never in what "sounds right." The quote skill exists specifically because AI effort estimates are unanchored guesses until calibrated against *your* measured throughput.
2. **Verify before acting.** Bug premises get reproduced before they get fixed. Deploys get proven, not assumed.
3. **The client sees outcomes.** Client-facing output (updates, invoices, quotes) speaks in features and results, never in commit hashes and refactors.
4. **Error bars are the product.** A quote or estimate without stated assumptions and confidence is worse than none.

## Contributing

PRs welcome. A good skill for this pack: a mundane, recurring freelance task with a *non-obvious discipline* that makes the difference between amateur and professional output. Include the failure mode the skill prevents — that's the part that makes it teachable.

## License

MIT
