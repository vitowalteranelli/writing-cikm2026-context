# Piano Revisione: 06_conclusions.tex — Best Paper A*

## Principio guida

La versione corrente in `overleaf/06_conclusions.tex` (4 righe) è concisa ma copre tutti i punti essenziali. Il rewrite plan (`Modifica 6.1`) eliminava il finding su CA-Val, che è invece la parte più onesta e differenziante della conclusione.

**NON sono possibili nuovi esperimenti.** Ogni affermazione deve basarsi sui risultati già presenti nel paper.

**Strategia:** espandere da 4 a ~20 righe, mantenendo il finding su CA-Val, aggiungendo direzioni future, e chiudendo con la tesi centrale.

---

## Blocco LaTeX sostitutivo (righe 7--10)

Il blocco corrente va sostituito con:

```latex
This work introduced \modelname{}, a context-aware graph recommender that integrates contextual information directly into graph propagation via context-gated message passing, and a comprehensive suite of nine context-sensitive evaluation metrics that capture distinct failure modes of context-aware recommendation -- from exact match (ACC) through partial alignment (CS, WCS, WCA, Friction) to list-level coverage (CR, CGB) and context-weighted ranking quality (CW-nDCG, CW-MAP).

The experiments support two main conclusions. First, context-gated message passing improves standard ranking accuracy on datasets where the contextual signal is informative (Yelp, Frappe), and this improvement is accompanied by measurably better contextual alignment across all metric families. On BGG, where memory constraints force a reduced embedding size, the architecture still achieves superior geometric alignment and contextual ranking quality, suggesting that the benefits of context-aware propagation extend beyond accuracy gains. Second, the context-aware validation analysis reveals that using CW-nDCG@10 as a validation objective does not improve recommendation quality over standard nDCG@10, and may paradoxically penalize interactions in atypical contexts. This negative result is informative: it separates the role of context-aware evaluation (which is effective) from context-aware optimization (which remains an open problem).

The ablation study confirms that the optimal context feature subset is dataset-dependent, and the proposed metrics reveal that standard accuracy measures alone miss contextual alignment degradation. We identify four priorities for future work: extending the method to continuous context representations; improving memory efficiency through sparse or sampled context-gating; systematic comparison with graph-based CARS methods (CA-KGCN, GEM, IEDR); and refining context-sensitive validation objectives, for instance through multi-objective early stopping or per-context validation sets.
```

---

## Differenze chiave rispetto alla versione corrente

| Aspetto | Versione corrente | Versione proposta |
|---|---|---|
| Lunghezza | 4 righe | ~20 righe |
| Finding CA-Val | Menzionato ma breve | Spiegato con insight sull'atypical context |
| Limitazioni | Non menzionate | Riconosciute onestamente (capacity) |
| Direzioni future | Non presenti | 4 priorità concrete |
| Tesi centrale | Implicita | Esplicita: context-aware eval ≠ optimization |
| Metriche | Menzionate genericamente | Elencate con nomi e acronimi |

---

## A*-gate

`PASS`. Versione più ricca e onesta, nessun overclaiming, nessun nuovo esperimento richiesto.
