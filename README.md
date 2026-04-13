# brave-problem-solver

A Claude Code skill that pushes Claude to tackle problems head-on instead of taking the easy way out.

Claude has a tendency to suggest workarounds, skip steps, or bail when things get hard. This skill fixes that behavior. When Claude encounters difficulty, it commits to solving the actual problem instead of offering menus of alternatives, recommending "skip," or going hypothetical.

## Installation

### One-liner (npx)

```bash
npx skills add ayushshah31/brave-problem-solver
```

> **Note:** The `npx skills` CLI (by [Vercel Labs](https://github.com/vercel-labs/skills)) installs to `~/agent/skills/`. If Claude Code doesn't pick it up, symlink it:
> ```bash
> ln -s ~/agent/skills/brave-problem-solver ~/.claude/skills/brave-problem-solver
> ```

### Manual install (recommended)

**User-wide** (available in all projects):
```bash
git clone https://github.com/ayushshah31/brave-problem-solver.git ~/.claude/skills/brave-problem-solver
```

**Project-scoped** (available in one project, committable to version control):
```bash
git clone https://github.com/ayushshah31/brave-problem-solver.git .claude/skills/brave-problem-solver
```

### From .skill file

Download [`brave-problem-solver.skill`](./brave-problem-solver.skill) and open it in Claude Code.

## What it does

The skill identifies and corrects **11 cowardly patterns** that Claude falls into when tasks get difficult:

| # | Pattern | What it looks like |
|---|---------|-------------------|
| 1 | **Skip this step** | "This step is complex, so let's skip it for now." |
| 2 | **Workarounds instead of solutions** | "You could manually copy these values..." |
| 3 | **Giving up after one error** | "I got an error. This might not work." |
| 4 | **"Not possible" without trying** | "This might not be possible because of X." |
| 5 | **Three alternatives instead of committing** | "Here are three approaches: A, B, or C." |
| 6 | **Hedging instead of doing** | "You could try adjusting the selector..." |
| 7 | **"Skip" as a solution** | "If the form doesn't work, skip this job." |
| 8 | **Premature simplification** | "Let me simplify this to make it manageable..." |
| 9 | **Invisible scope reduction** | Implements 4 of 6 features, presents as done |
| 10 | **Asking permission you already have** | "Would you like me to debug this?" (you said debug it) |
| 11 | **Error-avoidance theater** | try/catch everything instead of fixing root cause |

### The spicy part

When Claude catches itself slipping into a cowardly pattern, it calls it out in real time:

> *"I was about to suggest skipping this -- that's the coward's way out. Let me actually solve it."*

> *"I am not going to hedge with 'maybe' or 'you could try' -- these are the patterns, and one of them is your bug."*

## Why this exists

Built out of frustration with Claude recommending "skip" when the tool's entire purpose is to do the hard thing. Real example:

> **User builds a job application bot.** Claude encounters a tricky form field. Claude's recommendation: *"If the Next button doesn't advance after 1 try, SKIP this job."*
>
> The entire tool exists to apply to jobs. Skipping is the one thing it must not do.

## Eval results

Tested with 3 realistic scenarios, comparing with-skill vs without-skill responses:

| Eval | With Skill | Without Skill | Key difference |
|------|-----------|--------------|----------------|
| Tricky form field (Selenium bot) | 5/5 | 5/5 | With-skill enforces "never skip" in error handling |
| Multi-step scraping (Cloudflare) | 5/5 | 5/5 | Baseline spent 25% of response on ethical hedging instead of solving |
| Debugging (intermittent crash) | **5/5** | **2/5** | Baseline went hypothetical ("I would..."), with-skill jumped in and debugged |

The skill's impact scales with task difficulty. Easy tasks show marginal difference. Hard tasks show a fundamentally different approach.

## When to use it

Best for:
- Automation and agentic pipelines (bots, scrapers, CI/CD)
- Debugging intermittent or complex bugs
- Multi-step workflows where each step matters
- Any context where "skip it" defeats the tool's purpose

Not needed for:
- Simple one-line fixes
- Explanatory/educational questions
- Tasks with genuinely ambiguous requirements

## License

MIT
