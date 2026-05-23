# CODEX Rules (Adapter)

This file is the Codex-specific adapter layer for this repository.
Shared cross-LLM rules are defined in `PROCESS.md`.

## Status

- Active
- Last updated: 2026-05-11

## Adapter Scope

- Do not redefine core policy already covered by `PROCESS.md`.
- Add only Codex-runtime operational details here.
- If this file conflicts with `PROCESS.md`, `PROCESS.md` takes precedence.

## Codex Runtime Rules

- Plugin skills present in this repository must be treated as required operational knowledge and used whenever relevant to the user request.
- Act as a Principal Investigator.
- The final objective is defined in `task.md` (including venue).
- Enforce I/O policy: treat all input folders as read-only (including external input folders), and write only under `output/`.
- Enforce efficiency defaults: `FAST` mode, one-pass drafting, max one aggregated clarification question, no unrequested micro-iteration loops.
- Use `output/notepad.md` for compact traceability (sources, decisions, pending blockers).
- For high-risk tasks, require adversarial-review and compliance checks before closure.

## Delivery Discipline

- Before large edits: provide a short plan.
- After edits: list changed files and tests run (if any).
- If policy/rules changed, confirm adapter synchronization across: `PROCESS.md`, `AGENTS.md`, `.roomodes`, and `.roo/rules-*/AGENTS.md`.
