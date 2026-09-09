# Awesome Agent Loops [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Loops, not prompts. A curated list of patterns, tools, templates and writing on **loop engineering** — designing systems that prompt your AI agents for you.

In June 2026, the way people work with coding agents shifted: instead of prompting an agent turn by turn, you design a loop that discovers work, hands it to agents, verifies the result, persists state, and decides what happens next. This list collects everything worth reading and running on that shift.

Maintained by [agentloophub.com](https://agentloophub.com) — the loop template library. *This list updates itself via an agent loop; humans approve every merge.*

## Contents

- [Concepts & Guides](#concepts--guides)
- [Origin Posts & Talks](#origin-posts--talks)
- [Loop Patterns](#loop-patterns)
- [Templates](#templates)
- [Runtimes & Harnesses](#runtimes--harnesses)
- [Scheduling & Triggers](#scheduling--triggers)
- [Verification & Guardrails](#verification--guardrails)
- [State & Memory](#state--memory)
- [Cost Control](#cost-control)
- [Related Lists](#related-lists)
- [Communities](#communities)

## Concepts & Guides

- [What Is Loop Engineering?](https://www.mindstudio.ai/blog/what-is-loop-engineering-ai-coding-agents) - Plain-language introduction: act, observe, decide, repeat — and when loops beat single-shot prompting.
- [Loop Engineering: The Complete Guide](https://linas.substack.com/p/loop-engineering-complete-guide) - Long-form walkthrough written for both engineers and non-engineers.
- [Loop Engineering: Design Coding Agent Loops That Run While You Sleep](https://explainx.ai/blog/loop-engineering-coding-agents-claude-code-guide-2026) - From ReAct and ralph to `/goal` and `/loop` in Claude Code, with cron-driven examples.
- [Loop Engineering: The Guide for AI Agents](https://lushbinary.com/blog/loop-engineering-ai-coding-agents-guide/) - The five building blocks of a loop (plus memory), mapped to Claude Code and Codex.
- [Loop Engineering (Cobus Greyling)](https://cobusgreyling.medium.com/loop-engineering-62926dd6991c) - How loops relate to prompt, context and harness engineering.
- [Loop Engineering (Addy Osmani)](https://addyosmani.com/blog/loop-engineering/) - The definitive long-form piece: a loop's five building blocks (automations, worktrees, skills, connectors, sub-agents) plus memory, mapped onto both Claude Code and Codex — and why verification and token cost stay your job.
## Origin Posts & Talks

- [Peter Steinberger's loop tweet](https://x.com/steipete/status/2063697162748260627) - The two sentences that named the trend: you should be designing loops that prompt your agents.
- [Boris Cherny on loops](https://x.com/0xMovez/status/2064047579499770218) - "I don't prompt Claude anymore. I create loops — and the loops do the work. My job is to create loops."
- [What agent looping actually is (@shannholmberg)](https://x.com/shannholmberg/status/2063924108535197842) - The most-shared primer from the original thread.
- [One-off loops vs forever loops (@kunchenguid)](https://x.com/kunchenguid/status/2064039033152692323) - A no-BS taxonomy of loops from real production use.

## Loop Patterns

- **Ralph loop** - The brute-force `while true` pattern: same prompt, fresh agent, until the verify step passes.
- **Maker–checker loop** - One agent acts, a separate model judges whether the goal is met; Claude Code's `/goal` applies this at the exit condition.
- **Queue-drain loop** - Discover tasks into a queue (issues, briefs, failing tests), pop one per cycle, exit when empty.
- **Cron refresh loop** - Scheduled wake-up, diff current state against desired state, act only on drift.
- **Subagent fan-out loop** - A coordinator loop that spawns scoped subagents per task and merges verified results.

## Templates

- [Agent Loop Hub templates](https://agentloophub.com) - Copy-paste loops in a seven-field format (goal, trigger, discover, act, verify, persist, exit) with measured token cost per cycle.
- Test-fix loop, content refresh loop, dependency upgrade loop, scrape-and-validate loop - see the library for runnable specs.

## Runtimes & Harnesses

- [Claude Code](https://code.claude.com/docs/en/goal) - Agentic CLI with built-in `/goal` condition loops; the reference runtime for most loop writing today.
- [OpenClaw](https://github.com/openclaw/openclaw) - Open-source personal agent runtime by the author of the tweet that named the trend.
- [obra/superpowers](https://github.com/obra/superpowers) - Composable skills that give loops engineering discipline: TDD, subagent review, git worktrees.
- [openclaw-code-agent](https://github.com/goldmar/openclaw-code-agent) - Runs Claude Code, Codex and OpenCode as managed background sessions with plan approval, worktree isolation and merge/PR follow-through.
- [Open Agent Relay](https://github.com/ShakespeareLabs/open-agent-relay) - Exposes bounded local Claude Code, Codex, or automation capabilities to teammates and agents over a trusted LAN.
- [fractal](https://github.com/plasma-ai/fractal) - Runs hierarchical coding-agent loops in per-node Git worktrees, with recursive child delegation, SQLite-backed run state, and configurable limits on iterations, depth, children, time, and cost.
- [YYLO](https://github.com/yylo-dev/yylo) - Command-line orchestrator for coding-agent loops: task start opens a dedicated branch and worktree per task, edits and tests happen there, and a risk-based merge queue verifies and lands each change with receipts stored in the repository.

## Scheduling & Triggers

- [Claude Code Routines](https://claudeapi.com/en/blog/dev-guides/claude-code-routines-cloud-automation-2026/) - Cloud loops (research preview, April 2026): schedule, API and GitHub-webhook triggers run on Anthropic's infra even with your laptop closed.
- [Claude Code `/loop` and `/schedule`](https://code.claude.com/docs/en/scheduled-tasks) - Session-scoped interval loops in the terminal; `/schedule` now creates cloud Routines.
- [`/loop` vs Desktop vs Cloud vs cron](https://wmedia.es/en/tips/claude-code-schedule-vs-loop-vs-cron) - When to reach for each: open-session, machine-on, or fully hosted.
- [Headless `claude -p` on system cron](https://www.verdent.ai/guides/claude-code-loop-command) - Let the OS drive the agent on a timer with `--allowedTools` for unattended runs.
- CI triggers (on push / on schedule) - Loops that live in GitHub Actions.
- Event triggers - Webhooks, new-issue events, GSC data drops.

## Verification & Guardrails

- Test suites as verify steps - The strongest signal: exit 0 or loop again.
- Second-model judges - A separate model evaluating "is the goal met?" to avoid self-grading.
- Diff budgets & change caps - Bounding how much a single cycle is allowed to touch.

## State & Memory

- Markdown state files - A `state.md` the loop reads and rewrites each cycle; agents forget, the repo doesn't.
- Issue/board-backed state - Linear, GitHub Projects or a plain table as the loop's queue and memory.

## Cost Control

- Token budgets per cycle - Declare expected cost up front; kill cycles that exceed it.
- Exit conditions - No exit, no loop — just a bill.

## Related Lists

- [serenakeyitan/awesome-agent-loops](https://github.com/serenakeyitan/awesome-agent-loops) - Copy-paste `/loop`, `/goal` and `/schedule` commands sourced from X power users.
- [loops!](https://loops.elorm.xyz/loops) - Searchable catalog of 40+ ready-to-copy loops for Claude Code, Cursor and Codex.

## Communities

- r/ClaudeAI - Loop threads and Claude Code automation discussion.
- Hacker News - Search "loop engineering" for the ongoing debate.

## Contributing

One line is enough. Open a PR adding a resource in the format `- [Name](link) - One-sentence description.` See [CONTRIBUTING.md](CONTRIBUTING.md). Self-promotion is fine if the thing is genuinely useful and runnable.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
