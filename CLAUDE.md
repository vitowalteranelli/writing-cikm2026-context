# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> Portability note: shared cross-LLM rules are defined in [PROCESS.md](PROCESS.md).
> This file is a Claude-specific adapter and must not conflict with `PROCESS.md`.

## What this repo is

A LaTeX writing workspace for a single top-tier A* computer engineering conference submission. Goal stated in [task.md](task.md): revise the paper with Best Paper quality bar.

This is a **paper repo, not a code repo** — there is no build system, test suite, or runnable code here. The "experiments" and "numerical verification" referenced in the appendix live in a separate, un-versioned `v1/` source tree (paths like `4-experiment/v1/results/e1/` and `v1/paper/sections/`).

### Project-specific LaTeX macros (defined in [overleaf/main.tex](overleaf/main.tex))

When writing or editing, use project macros instead of hardcoding terms:
- `\ours{}` → project method name (always use this, never hardcode the name)
- `\URSp{}` → "U/R/S" (the uniqueness/redundancy/synergy triple)
- `\E`, `\R`, `\Var`, `\Cov`, `\LOCO`, `\STII`, `\FSII`, `\SII`, `\bg`, `\XOR`
- Theorem environments: `theorem`, `lemma`, `proposition`, `corollary`, `assumption` (numbered shared with `theorem`)

## Operating rules

Shared rules are in [PROCESS.md](PROCESS.md). Codex-specific runtime details are in [.agents/CODEX_RULES.md](.agents/CODEX_RULES.md).

- **Conversation language: Italian.** All produced content (paper text, drafts, deliverables): English (American English).
- **"Overleaf" is a read-only directory.**
- **Quality bar**: every edit must meet potential Best Paper standards at a top-tier A* computer engineering venue. No casual prose, no unsupported claims.
- **Before large edits**: provide a short plan first. **After edits**: list changed files (and any tests run, though there are none here).
- Plugin skills present in this repo are required operational knowledge — use them when relevant.
- Act as a Principal Investigator on this work.

## Plugins available in this workspace

Configured via [.agents/plugins/marketplace.json](.agents/plugins/marketplace.json) and [.agents/plugins/marketplace.research-companion.json](.agents/plugins/marketplace.research-companion.json). The submodule [plugins/research-companion/](plugins/research-companion/) provides:

- **Agents**: `brainstormer`, `idea-critic`, `research-strategist` — for evaluating directions, framing contributions, and project triage
- **Skill** `/research-companion` — 6-phase ideation pipeline (Seed → Diverge → Evaluate → Deepen → Frame → Decide), includes Carlini's conclusion-first test

These exist for *which* paper to write / how to frame, not for *how* to typeset. Reach for them when revising framing, contribution claims, or narrative arc; not for routine LaTeX edits.
