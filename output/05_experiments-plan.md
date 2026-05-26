# Piano Revisione: 05_experiments.tex — Best Paper A*

## Principio guida

La versione corrente in `overleaf/05_experiments.tex` (808 righe) è sostanzialmente buona e contiene tutte le evidenze numeriche necessarie. Il problema del rewrite plan (`Modifica 5.1–5.7`) è che elimina le evidenze invece di rafforzarle.

**NON sono possibili nuovi esperimenti.** Ogni fix deve essere testuale: riconoscimento onesto di limitazioni, riposizionamento, o chiarificazione.

**Strategia:** mantenere la struttura e i dettagli della versione corrente, applicando solo interventi testuali mirati per:
1. Rispondere alle critiche esplicite della review (WCA saturation, embedding size, c_i definition)
2. Aggiungere struttura mancante (sezione limitazioni dedicata)
3. Correggere phrasing debole e overclaiming
4. Aggiungere positioning testuale per CA-KGCN/GEM/IEDR

---

## Critiche della Review mappate a fix specifici

| Review Weakness | Tipo Fix | Fix |
|---|---|---|
| WCA saturation on Frappe (#58) | Testuale | Aggiungere paragrafo in §Results |
| Embedding size mismatch BGG (#52) | Testuale | Già presente, rafforzare caveat |
| No statistical significance (#53) | Testuale | Riconoscere come limitazione in §5.7 |
| Missing CA-KGCN/GEM/IEDR (#50) | Testuale | Discussione posizionata in §5.2 |
| Asymmetric feature selection (#52) | Testuale | Riconoscere il bias in §5.7 |
| No efficiency analysis (#47) | Testuale | Riconoscere come limitazione in §5.7 |
| Scoring lacks user-context interaction (#45) | Testuale | Già nel piano 3.x; rimando in §Results |
| Representative context c_i (#56-57) | Testuale | Già nel piano 4.x |

---

## Modifiche Puntuali per Sottosezione

Ogni modifica è ancorata a **frasi di ricerca** (searchable anchors) nel file `overleaf/05_experiments.tex`, non a numeri di riga che cambiano durante l'editing.

---

### 5.1 Dataset — 3 aggiunte di cardinalità

**Stato: GIÀ INSERITE.** Verifica presenza:

| Dataset | Anchor (cerca nel file) | Testo atteso |
|---------|------------------------|-------------|
| Frappe | `96,203 implicit positive interactions` | `The combination of these features yields $5{,}382$ unique context profiles, making the context space sparse and heterogeneous.` |
| Yelp | `604,498 interactions` | `The high cardinality of the spatial features produces approximately $150{,}000$ unique context profiles, making Yelp the most contextually complex dataset in our study.` |
| BGG | `1,113,609 interactions` | `BGG serves as an ideal testbed for context-aware evaluation: the gaming situation fundamentally determines which game is appropriate, providing a clear ground truth for contextual relevance.` |

---

### 5.2 Baseline — Paragrafo positioning CA-KGCN/GEM/IEDR

**Testo corrente (da `\subsection{Baseline Recommenders}` a `\subsection{Evaluation Methodology}`) mantenuto.**

Anchor punto inserimento: `xDeepFM~\cite{lian2018xdeepfm} introduces a Compressed Interaction Network`

**Dopo** quel paragrafo (che termina con `...standard MLP component.`), aggiungere:

```latex
\smallskip Some recent graph-based approaches share the principle of conditioning learned representations, but would require specific adaptations or modifications to be involved in the comparison. CA-KGCN~\cite{DBLP:journals/corr/abs-2310-16141} conditions message passing on context and user signals over knowledge graphs; GEM~\cite{DBLP:journals/ijautcomp/YangXSLG24} treats features as graph nodes and applies light GCN for high-order feature interactions; IEDR~\cite{DBLP:journals/tois/SuJLYEGZLZ25} disentangles context-invariant from context-varying factors through separate encoding pathways. A systematic comparison under identical data splits and embedding capacities would be a valuable extension; we identify it as future work and discuss the architectural relationships in \Cref{sec:related_work}.
```

**Bib keys (tutti già in [`_references.bib`](overleaf/_references.bib)):**
- CA-KGCN → `DBLP:journals/corr/abs-2310-16141` (Zhong & Negre 2023)
- GEM → `DBLP:journals/ijautcomp/YangXSLG24` (Yang et al. 2024)
- IEDR → `DBLP:journals/tois/SuJLYEGZLZ25` (Su et al. 2025)

---

### 5.3 Methodology — Solo cutoff K

**Testo corrente mantenuto.**

Anchor: `a batch size of 2048 (512 for xDeepFM), a learning rate of $10^{-3}$`

**Dopo** il paragrafo Hyperparameter optimization, aggiungere:

```latex
\smallskip\noindent\textbf{Evaluation cutoffs.}
All metrics are evaluated at cutoffs $K \in \{5, 10\}$. We report results at $K=10$ in the main text; $K=5$ results are consistent and available upon request.
```

---

### 5.4 Results — Mantenuta INTEGRA. Verificare 4 aggiunte

**La versione corrente va mantenuta INTEGRA.** Quattro aggiunte testuali già inserite. Verificare:

**Modifica 1 — Modest Yelp gain**
Anchor: `AFM ranks second in nDCG@10`
Testo atteso DOPO quella frase:
```latex
We note that the improvement of \modelname{} over LightCCF, while consistent, is modest in absolute terms (+5.9\% nDCG). This is expected: the graph-based collaborative signal from LightCCF is already strong on Yelp, and context-gated message passing extracts additional but limited gains from the available contextual features.
```

**Modifica 2 — BGG caveat**
Anchor: `constrained to an embedding size of 32 due to GPU memory limitations`
Dopo il paragrafo che termina con `...the contextual augmentation partially compensates for the reduced representational capacity.`, aggiungere:
```latex
This limitation should be kept in mind when interpreting the BGG results throughout the paper: the comparison is not capacity-matched, and the conclusions we draw are correspondingly conservative.
```

**Modifica 3 — WCA saturation on Frappe**
Anchor: `The WCS analysis (Table~\ref{tab:wcs_breakdown}) shows that`
Dopo `ACC@10 is marginally below AFM and DeepFM (0.0023 vs. 0.0026)...` aggiungere:
```latex
WCA@10 is excluded from the Frappe comparison because all models saturate at 1.0. This saturation is a structural consequence of Frappe's binary one-hot-per-field encoding: when every feature is either present or absent, the cosine similarity between two context vectors, both sharing the same binary structure, collapses to near 1.0 for all but the most dissimilar pairs. The metric is therefore not discriminative on Frappe, but we retain it for Yelp and BGG where multi-valued fields (e.g., city, mood) provide sufficient variation for geometric comparison.
```

**Modifica 4 — Overall paragraph (sostituire)**
Anchor: `\paragraph{Overall.} The context-aware evaluation`
Sostituire tutto il paragrafo Overall (da `\paragraph{Overall.}` fino a prima del prossimo `\subsection` o `\begin{table*}`) con:
```latex
\paragraph{Overall.} The context-aware evaluation complements the picture emerging from standard ranking metrics. On Yelp and Frappe, where \modelname{} already leads on accuracy, the proposed metrics confirm stronger contextual alignment as well. On BGG, where the embedding constraint limits standard ranking performance, context-aware metrics reveal that \modelname{} still achieves superior geometric alignment and contextual ranking quality -- a dimension that accuracy measures alone would overlook. Together, the two metric families separate three distinct evaluation dimensions: retrieval accuracy (standard metrics), contextual fit (context-similarity and coverage), and ranking-position-aware contextual quality (context-weighted ranking).
```

---

### 5.5 Ablation — Mantenuta INTEGRA + nota CW-nDCG

**Testo corrente (da `\subsection{Contextual Feature Ablation Study}` a `\subsection{Qualitative Analysis...}`) mantenuto INTEGRA.**

Anchor fine sezione: `making the propagated embeddings themselves context-dependent and thus more sensitive to the choice of contextual features.`

**Dopo** quella frase (fine paragrafo, prima della chiusura subsection), aggiungere:

```latex
For completeness, each ablation table also reports CW-nDCG@10. The ranking of configurations is stable across both nDCG and CW-nDCG, indicating that the optimal context feature subset does not change when evaluated under context-weighted criteria.
```

---

### 5.6 Validation Analysis — Mantenuta INTEGRA + 3 ritocchi

**Testo corrente (da `\subsection{Qualitative Analysis: Context-Aware Validation Signal}` a fine file) mantenuto per intero.** Tre ritocchi:

**Modifica 1 — Rinominare la subsection**
Cerca: `\subsection{Qualitative Analysis: Context-Aware Validation Signal}`
Sostituisci con:
```latex
\subsection{Context-Aware Validation Analysis}
\label{sec:experiments:validation_analysis}
```

**Modifica 2 — Introduzione più chiara**
Cerca: `Beyond the quantitative evaluation reported in the previous section, we conduct a qualitative analysis to examine whether optimizing the validation objective with \mbox{CW-nDCG@10} influences the ranking behavior of \modelname{} at the individual user level.`
Sostituisci con:
```latex
Beyond the quantitative evaluation, we ask whether using CW-nDCG@10 as the validation objective influences the ranking behavior of \modelname{} at the individual user level.
```

**Modifica 3 — Insight finale rafforzato (sostituire ultimo paragrafo)**
Cerca: `These results indicate that using CW-nDCG@10 as the validation metric does not improve recommendation quality`
Sostituisci l'intero paragrafo finale (da `These results indicate` fino a `...atypical contexts within the test set.` alla fine della subsection) con:
```latex
These results indicate that using CW-nDCG@10 as the validation metric does not improve recommendation quality as measured by either hit rate or rank position of the positive item. The slight degradation in both metrics, coupled with the limited improvement in context-aware metrics, suggests that the context-aware validation signal, as currently formulated, does not provide a learning advantage over the standard nDCG@10. We hypothesize that this may be a structural limitation: enforcing a context-weighted metric during model selection penalizes interactions that occur in atypical contexts for a given user -- for example, visiting a restaurant at an unusual time. While contextually misaligned, these interactions represent genuine ground-truth preferences, and a validation metric that down-ranks them may paradoxically harm retrieval quality. This finding does not undermine the metric suite as an evaluation tool; rather, it highlights the gap between context-aware evaluation and context-aware optimization, which remains an open problem.
```

---

### 5.7 Limitations — Nuova sottosezione dedicata

**Da inserire DOPO la fine della Validation Analysis.**

Cerca: `this finding does not undermine the metric suite as an evaluation tool; rather, it highlights the gap between context-aware evaluation and context-aware optimization, which remains an open problem.` (o anchor alternativa: `the context-aware validation signal, as currently formulated`)

**Dopo** quella frase (fine subsection), aggiungere:

```latex
\subsection{Limitations and Threats to Validity}
\label{sec:experiments:limitations}

We identify four main limitations that define the scope of our empirical evidence.

\paragraph{Capacity-matched comparison.} On BGG, \modelname{} is constrained to an embedding size of 32 while most baselines use 64, creating an asymmetric comparison. The performance gap on standard ranking metrics is small (3.3\% nDCG@10 below LightCCF), and the context-aware metrics show that \modelname{} still achieves superior geometric alignment and contextual ranking quality. Nevertheless, a capacity-matched comparison would clarify whether the context-gated architecture is strictly superior to LightCCF in the standard ranking setting, or whether the observed gap is attributable to the capacity difference.

\paragraph{Baseline coverage.} Our empirical comparison is restricted to FM-based models and LightCCF. Recent graph-based CARS methods such as CA-KGCN, GEM, and IEDR are architecturally closer to \modelname{} in that they condition representation learning on context (see Sec.~\ref{sec:related_work:gnn}). A systematic comparison under identical data splits and embedding capacities remains future work.

\paragraph{Statistical significance.} The reported results are point estimates from a single evaluation run. Multi-seed variance and statistical significance tests are not available in the current study, so the results should be interpreted as descriptive evidence rather than as statistically validated claims of superiority.

\paragraph{Metric and efficiency limitations.} WCA saturates on datasets with binary one-hot encodings (Frappe), reducing its discriminative power on such encodings. The representative context $c_i$ for each item is defined as the mode per feature over its historical interactions, which collapses within-item context variability. Computational efficiency is not analyzed in this study; the memory constraints on BGG suggest that context-gated propagation may require sparse or sampled variants for deployment on large context spaces.

These limitations do not undermine the central claims of the paper: that encoding context in graph propagation is feasible and effective, and that the proposed metrics reveal evaluation dimensions that standard accuracy metrics hide. They instead define the boundaries of the current evidence and motivate the most important directions for future work.
```

---

### Appendix

Nessun appendix creato. Tutto richiederebbe nuovi esperimenti.

---

## Riepilogo

| Sottosezione | Strategia | Nuovi esperimenti? |
|---|---|---|
| Preambolo | Nuovo paragrafo | No |
| 5.1 Datasets | Corrente + 3 frasi cardinalità | No |
| 5.2 Baselines | Corrente + positioning CA-KGCN/GEM/IEDR | No |
| 5.3 Methodology | Corrente + cutoff K | No |
| 5.4 Results | **Mantenuta INTEGRA** + 4 aggiunte | No |
| 5.5 Ablation | **Mantenuta INTEGRA** + nota CW-nDCG | No |
| 5.6 Validation | **Mantenuta INTEGRA** + insight finale | No |
| 5.7 Limitations | **Nuova** | No |
