# PROCESS.md - Core Workflow for A* Paper Writing (LLM-neutral)

These rules are model- and runner-agnostic (Codex, Claude, Gemini, and others).

## Objective

Produce submission-ready paper deliverables for a top-tier A* computer engineering conference, with a Best Paper quality bar.

Minimize turns and token cost while preserving correctness and quality.

## Source Hierarchy

1. This file (`PROCESS.md`) is the single source of truth for shared process rules.
2. `task.md` defines project goal and the target venue.
3. Runner-specific adapters (for example `AGENTS.md`, `CLAUDE.md`, `.agents/CODEX_RULES.md`) may add execution details but must not conflict with this file.

## Sync Governance (Mandatory)

- Whenever operational rules change, update all relevant adapter files in the same change set.
- Minimum sync set: `PROCESS.md`, `AGENTS.md`, `.agents/CODEX_RULES.md`, `.roomodes`, and `.roo/rules-*/AGENTS.md`.
- If an adapter is intentionally not updated, explicitly state why in the delivery note.

## Language Policy

- Conversation language: Italian.
- Produced content and deliverables: English (American English).

## Execution Modes

- `FAST` (default): one complete draft + one final refinement (max 2 full passes).
- `PRECISION`: one draft + one specialist review + one final integration (max 3 full passes).
- If user does not specify mode, use `FAST`.

## Core Writing Policy

- Scope honesty is mandatory: do not overclaim, hide mixed results, or present unsupported conclusions.
- Preserve anonymous submission constraints required by the target venue.
- Use project macros defined in `overleaf/main.tex`; do not hardcode method-specific names or notation if macros exist.
- Bibliography standard is BibTeX.
- Before adding any new reference, include donor metadata and DBLP-extracted content according to project rules.

## Operational Efficiency

- Default execution mode: single-agent.
- Multi-agent workflow is allowed only when explicitly requested by the user or when a substantial blocker cannot be resolved by one agent.
- Keep clarification overhead minimal: ask at most one aggregated clarification question per turn when needed.
- Avoid unnecessary micro-iterations (`v2`, `v3`, `v4`) unless explicitly requested.
- One-pass drafting by default: produce near-final quality on first delivery.
- Diff-first reading: inspect targeted sections, headings, indexes, and relevant snippets before full-file scans.
- Chunking for large inputs: process in blocks and checkpoint concise findings.
- No full-copy handoffs: pass compact deltas, references, and decisions, not whole documents.
- Reuse existing drafts with targeted patches instead of full rewrites when feasible.
- Default external research policy: off, unless explicitly requested or risk is high.

## Risk Triage

- `Low`: style polishing, small rewrites, local consistency checks. QA: self-check.
- `Medium`: full-section drafting, positioning edits, evidence synthesis. QA: self-check + one focused specialist check.
- `High`: claim-sensitive rewrites, method/theory changes, experimental interpretation, submission compliance. QA: strict adversarial review + compliance check.

## Done Definition

A task is complete when:
- requested deliverable exists in `output/`,
- blocking unknowns are listed briefly,
- no unrequested polish loops remain open.

## Validation and Delivery

- For substantial edits: provide a short plan before editing.
- After edits: report changed files and validations performed.
- For this repository, validation is document-oriented (for example, LaTeX build and consistency checks), not software test-suite oriented.

## Repository Constraints

- This is a paper repository, not a software repository.
- `overleaf/` is synchronized with Overleaf and treated as source of truth.
- Unless explicitly requested, do not introduce workflow assumptions that require non-existent software CI/test infrastructure.

## I/O Data Policy (Mandatory)

- Input sources may come from `input/` and from user-provided external folders.
- All input folders are read-only by policy and must never be modified.
- Writing is allowed only under `output/` (or its subfolders).
- If a task would require writing outside `output/`, stop and request explicit user approval first.
- Use `output/notepad.md` as compact shared scratchpad for decisions, sources, and pending items.
