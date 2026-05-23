# AGENTS.md — Debug Mode

Troubleshooting adapter for paper-editing workflows.

## Source of Truth

- Shared process and constraints: `PROCESS.md`.
- Runtime-specific operational details: root `AGENTS.md` and `.agents/CODEX_RULES.md`.

## Debug Focus

- Validate edits against the effective paper source under `overleaf/`.
- Use document-oriented validation (LaTeX build checks, consistency checks, PDF inspection).
- Report residual risks clearly when full validation is not possible in-session.
