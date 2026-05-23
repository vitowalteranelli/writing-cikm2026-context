# AGENTS.md

Operational instructions for AI coding agents working in this workspace.

> Portability note: shared cross-LLM rules are defined in [PROCESS.md](PROCESS.md).
> This file is a Codex-oriented adapter and must remain consistent with `PROCESS.md`.

## Scope

- This is a paper repository, not a software repository.
- Primary objective and quality bar are defined in [task.md](task.md).
- Shared process rules live in [PROCESS.md](PROCESS.md).
- Runtime-specific Claude guidance lives in [CLAUDE.md](CLAUDE.md).

## First Steps

1. Read [CLAUDE.md](CLAUDE.md) before editing anything.
2. If edits are substantial, provide a short plan before changes.
3. After edits, report changed files and any validation performed.
4. If rules/process changed, perform mandatory sync with `PROCESS.md`, `.agents/CODEX_RULES.md`, `.roomodes`, and `.roo/rules-*/AGENTS.md`.

## Source Of Truth

- Paper sources are under [overleaf/](overleaf/), which is gitignored and synchronized with Overleaf.
- Treat Overleaf as source of truth.
- "Overleaf" is a read-only directory.

## Input/Output Policy (Mandatory)

- Create and use `input/` and `output/` as default working folders.
- You may also use user-provided external folders as additional inputs.
- Every input folder (local `input/` and external input folders) is read-only and must not be modified.
- Write operations are allowed only in `output/` and its subfolders.
- Use `output/notepad.md` for compact handoff notes: `status`, `sources`, `decisions`, `pending`.

## Token-Efficiency Policy (Mandatory)

- Default mode is `FAST`: one complete draft + one final refinement.
- Ask at most one aggregated clarification question per turn.
- Avoid progressive micro-polishing loops unless explicitly requested.
- Prefer patching existing outputs instead of regenerating whole documents.
- For large inputs, use chunked reading with concise checkpoints.
- For online research, use only when explicitly requested or for high-risk tasks.

## Risk Triage (Paper Tasks)

- `Low`: proofreading, wording, local formatting/citation cleanup.
- `Medium`: full-section drafting, related-work framing, synthesis from multiple sources.
- `High`: claim-sensitive changes, theory/method edits, experiment interpretation, anonymity/compliance-critical updates.

Required QA by level:
- `Low` -> self-check.
- `Medium` -> self-check + one targeted specialist pass.
- `High` -> adversarial review + compliance pass before final delivery.

## Build And Validation

- Build from [overleaf/](overleaf/) with docker image texlive

## Routing Rapido (Task -> Agent)

- Global orchestration, planning, and final integration -> `agents/coordinator.md`
- Theory, assumptions, formal claims, method details -> `agents/theory_method.md`
- Experiments, ablations, evidence quality -> `agents/experiments_evidence.md`
- Related work, novelty positioning, comparison framing -> `agents/related_work_positioning.md`
- Bibliography curation and citation hygiene -> `agents/bibtex_curator.md`
- Style polishing and readability -> `agents/style_clarity.md`
- Anonymity and submission-compliance checks -> `agents/anonymity_compliance.md`
- Targeted online research and source collection -> `agents/online_research.md`
- Adversarial peer review and rejection-risk analysis -> `agents/peer_review_adversarial.md`
- Limitations/threats-to-validity surfacing -> `agents/limitations_risk.md`
- Rebuttal preparation and anticipated Q&A -> `agents/rebuttal_prep.md`
- Final proofreading pass -> `agents/proofreading.md`
- Final consistency/compliance go-no-go -> `agents/consistency_compliance.md`
- Reproducibility and artifact-readiness checks -> `agents/reproducibility_artifacts.md`
- Storyline and section-flow optimization -> `agents/storyline_flow.md`

## Drafting From Input Files/Folders

- Supported workflow: drafting full sections (or complete drafts) from local or external source material.
- Preferred structure:
1. Put source material in `input/` (single files or nested folders).
2. Optionally provide external folder paths as additional read-only inputs.
3. Specify target section(s), constraints, and expected output filename under `output/`.
4. Agent reads, synthesizes, drafts in English (American English), and preserves evidence traceability.
5. Output draft goes to `output/` only.
6. Update `output/notepad.md` with sources used, assumptions, and open risks.

- Minimum drafting contract:
- Keep conversation in Italian, but produce drafted paper text in English.
- Distinguish extracted facts vs inferred statements.
- Preserve scope honesty (no overclaiming from partial evidence).
- When citing new external work, apply donor + DBLP rule before adding references.

## Writing And Editing Rules

- Conversation language is Italian; produced paper text and deliverables are English (American English).
- Keep anonymous submission mode aligned with the target venue; do not deanonymize.
- Use project macros from [overleaf/main.tex](overleaf/main.tex) (for example, `\ours{}` and `\URSp{}`), do not hardcode these terms.
- Bibliography is BibTeX.
- Before adding any new reference, include donor and DBLP-extracted content as required by project rules.

## Appendix And Evidence Integrity

- Keep appendix coverage aligned with [overleaf/appendix_notepad.md](overleaf/appendix_notepad.md) when moving or revising appendix material.
- Preserve scope honesty in reported results (especially mixed outcomes).

## Related Operational Rules

- Repository-wide Codex adapter constraints: [.agents/CODEX_RULES.md](.agents/CODEX_RULES.md).
- Research framing support (not routine typesetting): [plugins/research-companion/](plugins/research-companion/).
