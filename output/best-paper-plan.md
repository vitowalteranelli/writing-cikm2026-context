# Best-Paper Rewrite Plan for CIKM 2026

## Goal
Turn the current submission into a much stronger, submission-ready paper without running any new experiments.

The main constraint is fixed: we must improve the paper through rewrite, reframing, tightening, and evidence-aware positioning only. That means the plan must maximize perceived rigor, clarity, fairness, and novelty while staying honest about what the current results can and cannot support.

## Core Strategy

The fastest credible path is not to "add more claims." It is to:

1. Remove avoidable weaknesses in presentation and argumentation.
2. Make the contribution easier to understand in the first read.
3. Reposition the paper around the strongest defensible novelty.
4. Neutralize review risk with precise limitations, careful comparisons, and clean prose.
5. Make the metrics section look intentional, formal, and validated within the limits of the existing evidence.

If we do this well, the paper becomes easier for reviewers to trust, even if the empirical envelope stays fixed.

## Quantitative Writing Targets

The structural stats suggest that best-paper submissions in this space usually have a substantial core method and a non-trivial empirical section. We should treat this as a calibration target, not a rigid template.

Recommended body budget:

- Abstract: about 250 words
- Introduction: about 800 to 950 words
- Related Work: about 900 to 1,200 words
- Method: about 1,700 to 2,000 words
- Experiments and Results combined: about 2,400 to 3,000 words
- Limitations: about 500 to 800 words
- Conclusion: about 300 to 500 words

Practical implication:

- The method and evaluation narrative should remain the longest and most carefully written parts of the paper.
- The conclusion should stay short.
- Related work should be complete but not bloated.
- Limitations should be explicit enough to show maturity, but not so long that they crowd out the technical core.

Working rule:

- If the paper feels too short to be credible, expand explanation and interpretation before adding new claims.
- If the paper feels too long, cut repetition from introduction, related work, and result commentary before trimming the method or limitations.

## What We Cannot Do

- No new experiments.
- No new baselines.
- No new claims that depend on missing evidence.
- No expansion of the model story beyond what the current results can honestly support.
- No vague "we outperform everyone" language.

## What We Can Still Win On

- Clearer contribution framing.
- Much stronger related-work positioning.
- Better definition of the context-sensitive metrics.
- More precise treatment of limitations and fairness issues.
- Better narrative flow from problem to model to evaluation.
- Cleaner presentation that removes the "draft-like" feel.

## Hidden Critiques To Address

The review text already points to visible issues, but a best-paper rewrite also has to neutralize the criticisms that sit behind the wording. The most important ones here are:

- The method can look like a derivative variant unless the framing makes the context-in-propagation design feel principled and not cosmetic.
- The metrics can look self-referential if the representative context is not defined carefully and if saturation behavior is not discussed honestly.
- The comparisons can look uneven if feature-subset selection is asymmetrical or if capacity constraints are acknowledged only as an afterthought.
- The evaluation can look underpowered if we do not say clearly that no new experiments are available, so the paper must gain credibility through scope honesty rather than through stronger claims.
- The model can look overfitted to the chosen benchmarks if we do not explain why each dataset is informative for a different part of the method.
- The contribution can look fragmented unless the model, metrics, and limitations are written as one consistent argument about contextual alignment.

Operational implications:

- Use `\modelname` as a single-point rename macro throughout the manuscript.
- Avoid language that suggests the model is a completely new paradigm; call it a principled context-conditioned graph recommender.
- Treat WCA/CGB saturation and capacity mismatch as first-class analytical limitations, not footnotes.
- Make the limitations section sound like evidence-aware scholarship, not damage control.

## Priority Order

### P0. Fix anything that makes the paper look unfinished

This is the highest priority because it directly affects reviewer trust.

Actions:

- Remove placeholders, duplicated tables, incomplete paragraphs, and any residual editing artifacts.
- Standardize notation, symbols, and terminology across all sections.
- Ensure every metric and acronym is defined before first use.
- Make sure figure/table captions explain the takeaway, not just the content.
- Check that equations render correctly and all cross-references resolve.
- Replace any informal wording with publication-grade prose.

Success criterion:

- A reviewer should never feel they are reading a partially assembled draft.

### P1. Rebuild the paper’s argument around one central claim

The current paper should read like it has a single strong thesis, not three separate ones.

Recommended central claim:

- We introduce a lightweight context-aware graph recommender that injects interaction context into propagation, and we propose context-sensitive offline metrics that expose alignment between context and ranking behavior.

Why this works:

- It keeps the model contribution and the evaluation contribution connected.
- It avoids overclaiming a major algorithmic leap.
- It makes the paper about "context-aware recommendation under context-aware evaluation" instead of a loose bundle of improvements.

Actions:

- Rewrite the introduction to state the problem, gap, method, and evaluation contribution in the first page.
- Make the contribution bullets sharply distinct:
  - model design,
  - context-aware scoring / propagation,
  - evaluation metrics,
  - empirical evidence.
- Ensure the conclusion mirrors those same four bullets.

Success criterion:

- A reviewer can summarize the paper in one sentence after reading the abstract and intro.

### P1.5. Match the manuscript shape to best-paper norms

The best-paper stats suggest that the paper should not be method-light or result-light.

Actions:

- Keep the method section as the largest or near-largest section.
- Give experiments/results enough space for interpretation, not just tables.
- Expand limitations enough to read as a mature paper section.
- Keep the introduction crisp rather than expansive.
- Avoid over-investing in related work at the expense of the method and results narrative.

Success criterion:

- The manuscript’s section proportions feel aligned with strong papers in the venue, not with a generic workshop draft.

### P2. Defend the model as a principled lightweight extension, not a novelty bomb

The review suggests the gating idea is incremental relative to edge-conditioned and FiLM-like methods. We should not fight that head-on.

Instead, we should frame the model as:

- a deliberately simple, scalable, context-conditioned propagation mechanism,
- designed to preserve the efficiency and interpretability of LightGCN-style recommenders,
- while enabling context-aware interaction modeling.

Actions:

- Reword the method section to emphasize design choices:
  - why context is encoded on edges,
  - why feature-wise gating is the right complexity point,
  - why the scoring function has the form it has.
- Add a short "design rationale" paragraph after the method equations.
- Explicitly acknowledge that the architecture is lightweight rather than radically novel.
- Make the NA-loss combination feel like a principled regularizer, not an unexplained add-on.

Success criterion:

- The method reads as intentional engineering with a clear bias toward simplicity, not as a slightly modified baseline.

### P3. Make the metrics section much more formal and less ambiguous

This is likely the highest-risk part of the paper, so it needs the most care.

The review flags:

- unclear representative context definition,
- possible WCA saturation issues,
- ad hoc normalization in CGB,
- sensitivity to high-cardinality contexts,
- underspecified implementation details.

Actions:

- Add an explicit formal definition for every new metric component.
- Define "representative context" precisely, including:
  - how it is computed,
  - what happens on ties,
  - how multi-field contexts are handled,
  - whether it is per-item, per-interaction, or aggregated over history.
- Add a notation table if needed.
- For each metric, include:
  - intuition,
  - formula,
  - interpretation,
  - boundary behavior,
  - failure modes.
- If WCA can saturate by construction, say so and explain when it is informative versus when it is not.
- If CGB normalization relies on a maximum deviation constant, justify it conceptually and keep the explanation simple.
- Make the role of IDF weighting explicit as a correction for context frequency imbalance.

Success criterion:

- The metrics section looks like a rigorous measurement framework, not an idea sketch.

### P4. Neutralize fairness critiques without new experiments

We cannot re-run comparisons, but we can stop looking careless.

Actions:

- State clearly where comparisons are not perfectly matched.
- Explain the capacity mismatch on BGG as a limitation, not a hidden advantage.
- Avoid overstating "competitive" if the setup is not fully normalized.
- Remove any language that implies exhaustive baseline coverage.
- If feature-subset asymmetry remains in the experiments, acknowledge it directly and frame it as an analysis constraint rather than a universal conclusion.
- Wherever possible, soften comparative claims from "superior" to "strong" or "promising" unless the evidence is unequivocal.

Success criterion:

- The paper does not invite easy reviewer criticism on fairness or experimental design.

### P5. Upgrade related work into positioning, not a literature dump

The review points to missing or under-discussed lines of work. Since we cannot add experiments, the next best move is to position carefully.

Actions:

- Expand the related work section to explicitly compare:
  - context-aware GNN recommenders,
  - feature-graph methods,
  - disentanglement-based CARS,
  - context-sensitive evaluation work.
- Make the distinctions structural:
  - interaction graph vs feature graph,
  - context on edges vs context as nodes or latent factors,
  - gating vs disentanglement,
  - ranking accuracy vs context alignment metrics.
- For each close baseline family, add a short "why not equivalent" statement.
- Avoid claiming novelty by omission.

Success criterion:

- Reviewers feel that the paper knows exactly where it sits in the literature.

### P6. Strengthen the empirical narrative using only existing results

We cannot manufacture evidence, but we can present what we have in a more reviewer-friendly way.

Actions:

- Reorganize the experiments section around questions, not tables.
- Use one subsection per question:
  - Does context-aware propagation help?
  - Do the context-sensitive metrics reveal different behavior than standard ranking metrics?
  - Which context groups matter most?
- Put the strongest result first.
- Make each table answer one specific claim.
- Add short interpretive paragraphs after each result table.
- Make sure the narrative includes mixed results honestly instead of smoothing them away.

Success criterion:

- The experiments read like a disciplined investigation, not a table dump.

### P7. Add a compact limitations section that sounds confident, not defensive

The review already exposes likely limitations. We should own them before reviewers do.

Actions:

- Add a dedicated limitations / threats-to-validity subsection.
- Cover:
  - discrete-context assumption,
  - no continuous context handling,
  - memory overhead for large context spaces,
  - fairness caveats in baseline capacity,
  - metric sensitivity and possible saturation,
  - lack of multi-seed statistics if absent.
- For each limitation, add one sentence about how it could be addressed in future work.

Success criterion:

- The paper demonstrates maturity and realism rather than evasiveness.

## Recommended Rewrite Sequence

### Pass 1: Structural rewrite

Order:

1. Abstract
2. Introduction
3. Contributions bullets
4. Method section
5. Metrics definitions
6. Related work
7. Experiments framing
8. Conclusion

Goal:

- Create a coherent first-order narrative before polishing sentence-level style.

Operational note:

- During this pass, the method and experiments sections should receive the most rewrite attention, because the stats indicate that strong papers in this area spend a large fraction of the body on these sections.

### Pass 2: Reviewer-risk rewrite

Order:

1. Fix ambiguous definitions.
2. Soften overclaims.
3. Add limitations.
4. Tighten fairness language.
5. Make the metrics section mathematically explicit.
6. Remove all draft artifacts.

Goal:

- Remove the easiest reasons for rejection.

### Pass 3: Final polish

Order:

1. Line editing for clarity and rhythm.
2. LaTeX consistency check.
3. Cross-reference and notation audit.
4. Figure/table caption tightening.
5. Final compliance read.

Goal:

- Make the final manuscript feel polished, deliberate, and submission-ready.

## Proposed Use of Specialist Review Roles

If we want to keep the process fast and high-quality, the most valuable review lenses are:

- `agents/theory_method.md` for the method and metric formalization.
- `agents/related_work_positioning.md` for literature framing and novelty positioning.
- `agents/style_clarity.md` for sentence-level cleanup and readability.
- `agents/peer_review_adversarial.md` for a hostile-read pass on reviewer objections.
- `agents/consistency_compliance.md` for final alignment, anonymity, and submission hygiene.

Recommended order:

1. theory/method
2. related work
3. adversarial review
4. style clarity
5. consistency/compliance

## Decision Rules During Rewrite

Use these rules to avoid wasting time:

- If a sentence increases ambition without adding evidence, cut it.
- If a claim depends on missing experiments, downgrade it or remove it.
- If a metric cannot be defined precisely, simplify the metric explanation before adding more prose.
- If two sections repeat the same message, keep the stronger version and delete the rest.
- If a comparison sounds unfair, make the caveat explicit.
- If a paragraph exists only to sound impressive, rewrite it to sound exact.

## Fast-Track Milestones

### Milestone A: Structural clarity

Done when:

- the paper has one clear thesis,
- contributions are explicit,
- method and metrics are fully defined,
- no obvious draft artifacts remain.

### Milestone B: Reviewer resistance reduced

Done when:

- fairness issues are disclosed,
- limitations are acknowledged,
- related work is structurally complete,
- overclaiming is removed.

### Milestone C: Submission polish

Done when:

- all references and cross-references are consistent,
- wording is crisp,
- LaTeX compiles cleanly,
- the manuscript feels complete and intentional.

## Final Outcome We Want

The final paper should leave a reviewer with this impression:

- The model is simple, coherent, and plausible.
- The metrics address a real evaluation gap.
- The empirical evidence is honest and useful.
- The authors understand the literature and their own limits.
- The manuscript is polished enough to trust.

That is the best realistic route to an A* outcome when no new experiments are possible.
