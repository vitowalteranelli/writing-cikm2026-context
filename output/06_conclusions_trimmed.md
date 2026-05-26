# 06_conclusions.tex — Versione ridotta A* (-70 parole)

## Blocco sostitutivo (da copiare in `overleaf/06_conclusions.tex`, righe 7--11)

```latex
This work introduced \modelname{}, a context-aware graph recommender with context-gated message passing, and nine context-sensitive evaluation metrics -- from exact match (ACC) through partial alignment (CS, WCS, WCA, Friction) to list-level coverage (CR, CGB) and context-weighted ranking (CW-nDCG, CW-MAP).

The experiments support two main conclusions. First, context-gated message passing improves standard ranking accuracy on informative datasets (Yelp, Frappe), accompanied by better contextual alignment. On BGG, despite reduced embedding size, the architecture achieves superior geometric alignment and contextual ranking quality, showing that context-gated benefits extend beyond accuracy. Second, using CW-nDCG@10 as a validation objective does not improve recommendation quality over nDCG@10 and may penalize atypical interactions. This negative result is informative: it separates context-aware evaluation (effective) from context-aware optimization (open problem).

The ablation study confirms that the optimal context feature subset is dataset-dependent and that standard accuracy measures alone miss contextual alignment degradation. Future work includes extending to continuous context, improving memory efficiency via sparse context-gating, and refining context-sensitive validation objectives.
```

## Parole: ~174 (-70 rispetto a ~244 correnti)

## Modifiche puntuali rispetto alla bozza precedente

| Dove | Prima | Ora |
|------|-------|-----|
| ¶2, frase 3 | `superior geometric and contextual ranking quality` | `superior geometric alignment and contextual ranking quality` |
| ¶2, frase 3 | `context-aware benefits` | `context-gated benefits` |
| ¶2, frase 5 | `This separates` | `This negative result is informative: it separates` |
| ¶3, frase 1 | `contextual degradation` | `contextual alignment degradation` |

## Criteri A*

| Criterio | Stato |
|----------|-------|
| Chiarezza del contributo | ✅ Modello + 9 metriche elencate con nome e acronimo |
| Self-consistency | ✅ Affermazioni allineate ai risultati delle sezioni 4-5 |
| Onestà scientifica | ✅ Embedding size BGG riconosciuto, CA-Val negativo preservato |
| No overclaiming | ✅ "accompanied by better" (non "caused by"), "open problem" |
| Conclusività | ✅ Due conclusioni chiuse + future work concreto |
| **A\*** | **✅ PASS** |
