# A* Paper Workflow Guide

This guide explains how to use this workspace end-to-end for writing, reviewing, and polishing a top-tier A* computer engineering paper.

## 1. What This Repository Is

- A paper-writing repository (LaTeX-centric), not a software application repository.
- Cross-LLM process source of truth: `PROCESS.md`.
- Project goal and venue: `task.md`.
- Runtime adapters: `AGENTS.md`, `CLAUDE.md`, `.agents/CODEX_RULES.md`, `.roomodes`, `.roo/rules-*/AGENTS.md`.

## 2. Core Policy Snapshot

- Conversation language: Italian.
- Deliverables: English (American English).
- Scope honesty is mandatory (no overclaiming).
- Venue anonymity constraints must be preserved.
- Bibliography standard: BibTeX.
- New references require donor metadata + DBLP-extracted content.
- Efficiency default: `FAST` mode (one complete draft + one final refinement).
- Clarifications default: maximum one aggregated question per turn.

## 3. Directory Conventions

- `overleaf/`: synchronized paper source (treated as source of truth).
- `agents/`: specialist role cards for routing tasks.
- `input/` (recommended): local source files/folders for drafting tasks.
- `output/` (recommended): generated drafts/reports/reviews.
- external input folders: allowed when explicitly provided by the user, always treated as read-only.

If `input/` and `output/` do not exist, create them before drafting-heavy workflows.

I/O enforcement:
- Never modify files in any input folder (local or external).
- Write only inside `output/`.

## 4. Agent System Overview

Default behavior is single-agent orchestration (`agents/coordinator.md`).
Use specialists only when needed or explicitly requested.

Core specialists:
- `theory_method.md`
- `experiments_evidence.md`
- `related_work_positioning.md`
- `bibtex_curator.md`
- `style_clarity.md`
- `anonymity_compliance.md`

Advanced quality specialists:
- `online_research.md`
- `peer_review_adversarial.md`
- `limitations_risk.md`
- `rebuttal_prep.md`
- `proofreading.md`
- `consistency_compliance.md`
- `reproducibility_artifacts.md`
- `storyline_flow.md`

## 5. Drafting Full Sections From Files/Folders

Recommended request pattern:
1. Place source material under `input/`.
2. Optionally provide external folder paths as additional read-only inputs.
3. Specify target section(s), constraints, tone, and output path under `output/`.
4. Request synthesis + drafting from those files/folders.

Example request:

"Read `input/prior_work/` and draft the Related Work section in American English.
Output to `output/related_work_draft.md`.
Use cautious claims and mark weak-evidence statements explicitly."

Minimum drafting contract:
- Distinguish extracted facts from inferences.
- Preserve evidence traceability.
- Do not overstate what sources support.
- Respect macro and notation consistency for LaTeX integration.

## 6. Online Research Workflow

Use online research only when explicitly requested or when evidence risk is high.

When enabled:
- Prefer primary sources.
- Track source links and access date.
- Separate facts from inference.
- Return confidence + open uncertainties.

Token guardrail:
- Prefer a small number of primary sources with direct relevance.

## 7. Serious Peer-Review Workflow (Recommended)

Use this sequence before major submission milestones:
1. `peer_review_adversarial.md`
2. `limitations_risk.md`
3. `experiments_evidence.md`
4. `reproducibility_artifacts.md`
5. `proofreading.md`
6. `consistency_compliance.md`

Expected outputs:
- Severity-ranked concerns
- Concrete fixes with effort estimates
- Go/no-go readiness recommendation

## 8. Validation and Build

Validation is document-oriented:
- LaTeX build checks
- cross-reference consistency
- figure/table/section consistency
- final proofreading and compliance checks

Build from `overleaf/` using TeX Live tooling as configured in this project.

## 9. Sync Governance (Do Not Skip)

When rules or workflow logic change, update adapters in the same change set.

Minimum sync set:
- `PROCESS.md`
- `AGENTS.md`
- `.agents/CODEX_RULES.md`
- `.roomodes`
- `.roo/rules-*/AGENTS.md`

If one file is intentionally not updated, document the reason in the delivery note.

## 10. Fast Playbooks

### A) Draft a new section from sources
1. Put files in `input/section_x/`.
2. Ask for drafting to `output/section_x_draft.md`.
3. Run `style_clarity` + `proofreading` pass.

### B) Stress-test contribution claims
1. Run `peer_review_adversarial`.
2. Patch major concerns in method/experiments text.
3. Run `limitations_risk` and soften unsupported claims.

### C) Final pre-submission pass
1. Run `consistency_compliance`.
2. Run `anonymity_compliance`.
3. Run final proofreading and bibliography hygiene checks.

### D) Ultra-efficient default loop
1. Run in `FAST` mode.
2. Deliver near-final output on first pass.
3. Aggregate all fixes into one final patch.

## 11. Suggested Request Templates

Template: section drafting

"Read `input/<folder>` and draft `<section>` in American English.
Target: `<audience/venue style>`.
Output: `output/<file>.md`.
Constraints: `<length, claims policy, must-include points>`."

Template: deep review

"Perform adversarial peer review on `<file/section>`.
Return major/minor concerns, rejection risk, and concrete fixes with priority order."

Template: online evidence check

"Run targeted online research for `<claim/topic>`.
Use primary sources only. Return links, confidence, and suggested edits."

## 12. Standard Prompt Structure (Recommended)

Use this structure to start tasks with minimum turns and token cost.

```text
TASK_TYPE: [draft_section | full_draft | scaffolding | peer_review | proofreading | online_research | compliance_check]
MODE: [FAST | PRECISION]   # default FAST
RISK_LEVEL: [LOW | MEDIUM | HIGH]

INPUT_SOURCES:
- [input/local_folder_or_file]
- [optional external read-only folder path]

TARGET_OUTPUT:
- FILE: output/<target_filename>.md
- FORMAT: [markdown | latex-ready text]

OBJECTIVE:
- [what must be produced]

CONSTRAINTS:
- [length budget]
- [must-include points]
- [style/tone]
- [forbidden claims or boundaries]

CITATION_POLICY:
- [reuse existing only | allow new references with donor+DBLP]

VALIDATION_REQUIRED:
- [self-check | adversarial review | compliance pass | proofreading]

OPEN_QUESTIONS:
- [optional; if empty write NONE]
```

For `TASK_TYPE: scaffolding`, specify one of:
- `SCAFFOLD_FROM: research_questions`
- `SCAFFOLD_FROM: experiments`
- `SCAFFOLD_FROM: research_plan`

Minimal ultra-fast version:

```text
TASK_TYPE: draft_section
MODE: FAST
INPUT_SOURCES: input/related_work/
TARGET_OUTPUT: output/related_work_draft.md
OBJECTIVE: Draft Related Work in American English with cautious claims.
CONSTRAINTS: 700-900 words, include 3 thematic clusters, no overclaiming.
VALIDATION_REQUIRED: proofreading
```

Scaffolding example:

```text
TASK_TYPE: scaffolding
SCAFFOLD_FROM: research_questions
MODE: FAST
INPUT_SOURCES:
- input/rq_notes/
TARGET_OUTPUT:
- FILE: output/paper_scaffold_from_rq.md
OBJECTIVE: Build a full paper scaffold (section tree + bullet intent per section + evidence map).
CONSTRAINTS: Keep claims conservative; flag missing evidence explicitly.
VALIDATION_REQUIRED: self-check
```
