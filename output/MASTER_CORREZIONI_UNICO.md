# MASTER — Tutte le correzioni: proofreading, phrasing, AmE, markup

**Paper:** *Graph Neural Networks for Context-Aware Recommendations under Context-Sensitive Evaluation Dimensions*  
**Target:** Best Paper @ CIKM 2026  
**Data:** 2026-05-24

---

## Come usare questo file

Ogni issue ha:
- **ID**: codice univoco (es. `M-01`) per riferimenti
- **File**: percorso relativo al workspace
- **Linea/e**: numero di linea nel file sorgente
- **Originale**: testo attuale (esatto)
- **Corretto**: testo proposto
- **Fonte**: report di origine (P1=Pass1, P2=Pass2, LA=LanguageAudit)
- **Priorità**: 🔴 Alta / 🟡 Media / 🟢 Bassa

Le issue sono **organizzate per file**, in ordine di linea.  
I file sono nell'ordine in cui appaiono nel paper.

---

## SOMMARIO

| File | Issue | 🔴 | 🟡 | 🟢 |
|------|-------|---|---|---|
| `00_main.tex` | M-01..M-09 | 5 | 1 | 3 |
| `01_introduction.tex` | M-10..M-20 | 1 | 8 | 2 |
| `02_related_work.tex` | M-21..M-33 | 2 | 9 | 2 |
| `03_model.tex` | M-34..M-48 | 0 | 9 | 6 |
| `04_metrics.tex` | M-49..M-62 | 0 | 9 | 5 |
| `05_experiments.tex` | M-63..M-120 | 10 | 34 | 14 |
| `06_conclusions.tex` | M-121..M-126 | 0 | 3 | 3 |
| `_references.bib` | M-127..M-131 | 0 | 3 | 2 |
| **Totale** | **131** | **18** | **76** | **37** |

---

# FILE: 00_main.tex

### M-01 — Trailing comma in \documentclass
| | |
|---|---|
| **Linea** | 48 |
| **Originale** | `\documentclass[natbib=false,sigconf,anonymous,review,screen,]{acmart}` |
| **Corretto** | `\documentclass[natbib=false,sigconf,anonymous,review,screen]{acmart}` |
| **Fonte** | P2/G1 |
| **Priorità** | 🔴 Rimuovere virgola prima di `]` — può generare warning |

### M-02 — Commented-out alternative titles dentro \title{}
| | |
|---|---|
| **Linee** | 152–157 |
| **Originale** | `\title{Graph Neural Networks for Context-Aware Recommendations under Context-Sensitive\nEvaluation Dimensions\n%A Graph Neural Network Model...\n% Graph Neural Networks...\n% %Novel\n% Context-Sensitive\n% Evaluation Dimensions\n}` |
| **Corretto** | Rimuovere tutte le linee commentate (153–157) dentro `\title{}` |
| **Fonte** | P2/G2 |
| **Priorità** | 🟡 Pulizia codice |

### M-03 — ACM ISBN placeholder non aggiornato
| | |
|---|---|
| **Linea** | 79 |
| **Originale** | `\acmISBN{978-1-4503-XXXX-X/2018/06}` |
| **Corretto** | Sostituire con ISBN corretto per CIKM 2026 o lasciare placeholder ufficiale |
| **Fonte** | LA #115 |
| **Priorità** | 🟡 Da aggiornare prima della camera-ready |

### M-04 — `\setcopyright{acmlicensed}` in anonymous submission
| | |
|---|---|
| **Linea** | 62 |
| **Originale** | `\setcopyright{acmlicensed}` |
| **Corretto** | Verificare se va commentato per double-blind |
| **Fonte** | LA #116 |
| **Priorità** | 🟡 Da verificare prima della submission |

### M-05 — Inline `%collaborative` comment nell'abstract
| | |
|---|---|
| **Linea** | 242 |
| **Originale** | `...how strongly context interacts with the %collaborative` |
| **Corretto** | `...how strongly context interacts with the collaborative` (rimuovere `%`) |
| **Fonte** | P2/G4 |
| **Priorità** | 🟢 Pulizia |

### M-06 — Stray `%\textcolor{red}{...}` comment dopo il titolo
| | |
|---|---|
| **Linea** | 159 |
| **Originale** | `%\textcolor{red}{Designed/Dedicated/Purpose-Built/Situational/Sensitive}` |
| **Corretto** | Rimuovere l'intera linea |
| **Fonte** | P2/G5 |
| **Priorità** | 🟢 Pulizia |

### M-07 — "context dependent" → "context-dependent" (abstract)
| | |
|---|---|
| **Linea** | 239 |
| **Originale** | `makes the learned embeddings context dependent` |
| **Corretto** | `makes the learned embeddings context-dependent` |
| **Fonte** | P1/D1 |
| **Priorità** | 🟢 Hyphenation |

### M-08 — Keywords: "GNN" → "graph neural networks"
| | |
|---|---|
| **Linea** | 283 |
| **Originale** | `\keywords{Context-aware recommender systems, GNN, evaluation}` |
| **Corretto** | `\keywords{Context-aware recommender systems, graph neural networks, evaluation}` |
| **Fonte** | LA #5 |
| **Priorità** | 🟢 Better discoverability |

### M-09 — Abstract: "remains competitive on BGG under a tighter embedding budget"
| | |
|---|---|
| **Linea** | 241 |
| **Originale** | `...remains competitive on BGG under a tighter embedding budget, while the proposed metrics expose context effects that accuracy-only evaluation does not reveal.` |
| **Corretto** | `...remains competitive on BGG despite a tighter embedding budget; the proposed metrics further expose contextual effects that standard accuracy-oriented evaluation does not capture.` |
| **Fonte** | LA (rewrite suggestion) |
| **Priorità** | 🟡 Migliora tono e precisione |

---

# FILE: 01_introduction.tex

### M-10 — "conditioning them" — antecedente ambiguo
| | |
|---|---|
| **Linea** | 9 |
| **Originale** | `...improve the relevance and personalization of recommendations by conditioning them on situational factors` |
| **Corretto** | `...improve the relevance and personalization of recommendations by conditioning recommendations on situational factors` |
| **Fonte** | P2/H1 |
| **Priorità** | 🟡 Chiarezza sintattica |

### M-11 — "This capability provides important benefits" — tautologico
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `This capability provides important benefits, including greater adaptability to real-world scenarios and increased user satisfaction.` |
| **Corretto** | `This makes recommendations more adaptable to real-world scenarios and increases user satisfaction.` |
| **Fonte** | P1/C1 |
| **Priorità** | 🟡 Tono più diretto |

### M-12 — "CARS also pose significant research challenges" → "introduce"
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `CARS also pose significant research challenges` |
| **Corretto** | `CARS also introduce significant research challenges` |
| **Fonte** | LA #6 |
| **Priorità** | 🟢 Scelta verbale più idiomatica |

### M-13 — "high-order" → "higher-order" (due occorrenze)
| | |
|---|---|
| **Linee** | 13, 14 |
| **Originale** | `high-order collaborative structure` (13), `high-order connectivity patterns` (14) |
| **Corretto** | `higher-order collaborative structure`, `higher-order connectivity patterns` |
| **Fonte** | P1/C2 |
| **Priorità** | 🟡 Uniformare terminologia (altrove si usa `higher-order`) |

### M-14 — "with relatively little architectural overhead" → "with low"
| | |
|---|---|
| **Linea** | 13 |
| **Originale** | `...model higher-order collaborative structure with relatively little architectural overhead.` |
| **Corretto** | `...model higher-order collaborative structure with low architectural overhead.` |
| **Fonte** | P1/C7 |
| **Priorità** | 🟡 Più formale |

### M-15 — "do not affect propagation itself" → "do not affect propagation"
| | |
|---|---|
| **Linea** | 14 |
| **Originale** | `...incorporate it in ways that do not affect propagation itself.` |
| **Corretto** | `...incorporate it in ways that do not affect propagation.` |
| **Fonte** | P1/C3 |
| **Priorità** | 🟢 Filler removal |

### M-16 — "are well-suited" → "are well suited" (AmE predicativo)
| | |
|---|---|
| **Linea** | 13 |
| **Originale** | `GNN recommenders are well-suited to this setting` |
| **Corretto** | `GNN recommenders are well suited to this setting` |
| **Fonte** | P1/B3 |
| **Priorità** | 🟢 AmE consistency |

### M-17 — "one for learning, the other for evaluation" → "the former...the latter"
| | |
|---|---|
| **Linea** | 19 |
| **Originale** | `Together, the model and the metrics provide a consistent view of context-aware recommendation: one for learning, the other for evaluation.` |
| **Corretto** | `Together, the model and the metrics provide a consistent view of context-aware recommendation—the former for learning, the latter for evaluation.` |
| **Fonte** | P1/C4 |
| **Priorità** | 🟡 Chiarezza |

### M-18 — "the benefit...is dataset dependent" → "the benefits...are dataset-dependent"
| | |
|---|---|
| **Linea** | 22 |
| **Originale** | `the benefit of contextual modeling is dataset dependent` |
| **Corretto** | `the benefits of contextual modeling are dataset-dependent` |
| **Fonte** | P1/C5, P1/D2, LA #3 |
| **Priorità** | 🟡 Accordo numero + hyphenation |

### M-19 — "not overly sparse" → "not prohibitively sparse"
| | |
|---|---|
| **Linea** | 22 |
| **Originale** | `...when the context space is informative and not overly sparse` |
| **Corretto** | `...when the context space is informative and not prohibitively sparse` |
| **Fonte** | LA #12 |
| **Priorità** | 🟢 Tono più accademico |

### M-20 — "observable separation between models" → "measured differences among models"
| | |
|---|---|
| **Linea** | 22 |
| **Originale** | `...highly balanced context groups limit the observable separation between models.` |
| **Corretto** | `...highly balanced context groups limit the measured differences among models.` |
| **Fonte** | LA #13 |
| **Priorità** | 🟢 Maggiore chiarezza |

---

# FILE: 02_related_work.tex

### M-21 — Nomi autori nei commenti (double-blind violation!)
| | |
|---|---|
| **Linee** | 13, 30, 42 (commentate) |
| **Originale** | `%\textcolor{blue}{I explained this acronym...}`, `%\textcolor{blue}{it may be strange...}`, `\textcolor{red}{Iván: I have changed...}` |
| **Corretto** | **Rimuovere TUTTI i commenti** contenenti nomi propri (Iván, Alejandro) |
| **Fonte** | P2/K1, P2/K2 |
| **Priorità** | 🔴 **Double-blind — critico** |

### M-22 — "families of methods" → "families of approaches"
| | |
|---|---|
| **Linea** | 7 |
| **Originale** | `three families of methods` |
| **Corretto** | `three families of approaches` |
| **Fonte** | LA #14 |
| **Priorità** | 🟢 Tono accademico |

### M-23 — "shallow side channels" — metafora vaga
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `...they are often incorporated as auxiliary features, shallow side channels, or post-hoc re-ranking signals...` |
| **Corretto** | `...they are often incorporated as auxiliary features, shallow side-channel signals, or post-hoc re-ranking adjustments...` |
| **Fonte** | P1/C6 |
| **Priorità** | 🟡 Precisione terminologica |

### M-24 — "no KG dependency" → "does not require an external KG"
| | |
|---|---|
| **Linea** | 15 |
| **Originale** | `no KG dependency` |
| **Corretto** | `without a KG dependency` o `does not require an external KG` |
| **Fonte** | LA #23 |
| **Priorità** | 🟢 Tono più formale |

### M-25 — "generic GNN recommenders" → "general GNN-based recommenders"
| | |
|---|---|
| **Linea** | 19 |
| **Originale** | `Relative to generic GNN recommenders` |
| **Corretto** | `Relative to general GNN-based recommenders` |
| **Fonte** | LA #26 |
| **Priorità** | 🟢 Evita tono dismissivo |

### M-26 — "Disentanglement seeks factor separation as an end in itself" → neutrale
| | |
|---|---|
| **Linea** | 22 |
| **Originale** | `Disentanglement seeks factor separation as an end in itself` |
| **Corretto** | `Disentanglement-oriented methods primarily aim to separate latent preference factors from contextual factors.` |
| **Fonte** | LA #27 |
| **Priorità** | 🟡 Tono neutrale verso lavoro altrui |

### M-27 — "Our metric family" → "Our family of metrics"
| | |
|---|---|
| **Linea** | 27 |
| **Originale** | `Our metric family is intended for this role` |
| **Corretto** | `Our family of metrics is intended for this role` |
| **Fonte** | LA #29 |
| **Priorità** | 🟢 Più idiomatico |

### M-28 — "do not tell us whether" → "do not capture whether"
| | |
|---|---|
| **Linea** | 27 |
| **Originale** | `but they do not tell us whether the retrieved items fit the query context` |
| **Corretto** | `but they do not capture whether the retrieved items are contextually appropriate for the query situation` |
| **Fonte** | P1/C18 |
| **Priorità** | 🟡 Meno colloquiale |

### M-29 — "Knowledge-Graph (KG)-conditioned" → doppia hyphenation
| | |
|---|---|
| **Linea** | 13 |
| **Originale** | `Knowledge-Graph (KG)-conditioned` |
| **Corretto** | `knowledge graph (KG)-conditioned` |
| **Fonte** | P1/D3 |
| **Priorità** | 🟡 Fix hyphenation + capitalization |

### M-30 — "reuse standard recommenders" → "reuse standard recommendation models"
| | |
|---|---|
| **Linea** | 7 |
| **Originale** | `reuse standard recommenders` |
| **Corretto** | `reuse standard recommendation models` |
| **Fonte** | LA #15 |
| **Priorità** | 🟢 Precisione |

### M-31 — "core representation-learning loop" → "core representation-learning process"
| | |
|---|---|
| **Linea** | 7 |
| **Originale** | `core representation-learning loop` |
| **Corretto** | `core representation-learning process` |
| **Fonte** | LA #16 |
| **Priorità** | 🟢 Meno colloquiale |

### M-32 — "scoring layer" → "scoring function"
| | |
|---|---|
| **Linea** | 8 |
| **Originale** | `...exploit context at the scoring layer` |
| **Corretto** | `...exploit context at the scoring function` |
| **Fonte** | LA #18 |
| **Priorità** | 🟢 Più generale (copre tutti i FM variants) |

### M-33 — "this concern has also been emphasized" → più diretto
| | |
|---|---|
| **Linea** | 27 |
| **Originale** | `This concern has also been emphasized in recent context-aware and POI-oriented analyses...` |
| **Corretto** | `Recent context-aware and POI-focused analyses have also emphasized this limitation...` |
| **Fonte** | LA #28 |
| **Priorità** | 🟢 Più diretto |

---

# FILE: 03_model.tex

### M-34 — Ranking "discrimination" → "differentiation"
| | |
|---|---|
| **Linea** | 120 |
| **Originale** | `This ensures that ranking discrimination accounts for contextual appropriateness` |
| **Corretto** | `This ensures that ranking differentiation accounts for contextual appropriateness` |
| **Fonte** | P2/H3 |
| **Priorità** | 🟡 "discrimination" ha connotazioni negative in inglese |

### M-35 — "over-smoothing" → "oversmoothing" (due occorrenze)
| | |
|---|---|
| **Linee** | 76, 126 |
| **Originale** | `over-smoothing` |
| **Corretto** | `oversmoothing` |
| **Fonte** | P1/B2 |
| **Priorità** | 🟡 AmE consistency |

### M-36 — Soggetto ambiguo in frase di apertura
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `This section introduces \modelname{}, ..., and is organized into three parts.` |
| **Corretto** | `This section introduces \modelname{}, ..., \textbf{The section} is organized into three parts.` |
| **Fonte** | LA #30 |
| **Priorità** | 🟡 Soggetto grammaticale chiaro |

### M-37 — "lets the model preserve" → "allows the model to preserve"
| | |
|---|---|
| **Linea** | 26 |
| **Originale** | `lets the model preserve the user--item graph` |
| **Corretto** | `allows the model to preserve the user--item graph` |
| **Fonte** | LA #33 |
| **Priorità** | 🟢 Più formale |

### M-38 — ReLU in Eq. 2 vs "No nonlinear activations" in Eq. 4
| | |
|---|---|
| **Linea** | 68 |
| **Originale** | `No nonlinear activations or additional feature transforms are applied` |
| **Corretto** | `No nonlinear activations or additional feature transforms are applied \textbf{during propagation}` (aggiungere qualifica) |
| **Fonte** | LA #34 |
| **Priorità** | 🟡 Evita apparente contraddizione con Eq. 2 (edge encoder usa ReLU) |

### M-39 — "user-item affinity" — uniformare trattino (en-dash vs hyphen)
| | |
|---|---|
| **Linea** | 111 |
| **Originale** | `user-item affinity` |
| **Corretto** | Usare `user-item` (hyphen) o `user–item` (en-dash) **consistentemente** in tutto il paper |
| **Fonte** | LA #39 |
| **Priorità** | 🟢 Consistenza tipografica |

### M-40 — "where sim(·,·) is cosine similarity and τ a temperature" → "τ is"
| | |
|---|---|
| **Linea** | 126 |
| **Originale** | `where sim(·,·) is cosine similarity and τ a temperature hyperparameter.` |
| **Corretto** | `where sim(·,·) is cosine similarity and τ is a temperature hyperparameter.` |
| **Fonte** | LA #40 |
| **Priorità** | 🟢 Grammatica |

### M-41 — "L2 regularization controls embedding magnitude" → "The L2 term"
| | |
|---|---|
| **Linea** | 127 |
| **Originale** | `L2 regularization controls embedding magnitude.` |
| **Corretto** | `The L2 term controls the magnitude of the embeddings.` |
| **Fonte** | LA #43 |
| **Priorità** | 🟢 Maggiore scorrevolezza |

### M-42 — "message passing" vs "message-passing" inconsistency
| | |
|---|---|
| **Tutto il file** | vari |
| **Originale** | Uso misto di `message passing` (nome) e `message-passing` (aggettivo) |
| **Corretto** | `message passing` come nome, `message-passing` come aggettivo |
| **Fonte** | LA #42 |
| **Priorità** | 🟡 Consistenza |

### M-43 — "current context" ambiguo in Sec. 3.2
| | |
|---|---|
| **Linea** | 55 |
| **Originale** | `...making message passing sensitive to the current context.` |
| **Corretto** | Specificare: contesto dell'interazione osservata vs contesto della query |
| **Fonte** | LA #35 |
| **Priorità** | 🟡 Chiarezza concettuale |

### M-44 — "non-linear" commentato (linea 90) — solo nota
| | |
|---|---|
| **Linea** | 90 (commentata) |
| **Originale** | `no non-linear activation` |
| **Corretto** | Non serve correzione (linea commentata), ma notare per consistenza |
| **Fonte** | P1/B1, P1/D4 |
| **Priorità** | 🟢 Solo nota |

---

# FILE: 04_metrics.tex

### M-45 — Inline `%judgment` comment tronca la frase
| | |
|---|---|
| **Linea** | 233 |
| **Originale** | `Family~3 solves this by replacing the static relevance %judgment with context-weighted relevance` |
| **Corretto** | `Family~3 solves this by replacing the static relevance judgment with context-weighted relevance` (o eliminare "judgment" e il `%`) |
| **Fonte** | P2/G3 |
| **Priorità** | 🟡 Rischio di breaking alla prossima modifica |

### M-46 — "along a spectrum of strictness and perspective" → vago
| | |
|---|---|
| **Linea** | 16 |
| **Originale** | `The five metrics are designed along a spectrum of strictness and perspective.` |
| **Corretto** | `The five metrics span a spectrum from strict exact-match to relaxed partial-alignment.` |
| **Fonte** | P1/C14 |
| **Priorità** | 🟡 Maggiore precisione |

### M-47 — "Friction sits between" → informale
| | |
|---|---|
| **Linea** | 16 |
| **Originale** | `Friction sits between the set-based and geometric approaches` |
| **Corretto** | `Friction occupies an intermediate position between the set-based and geometric approaches` |
| **Fonte** | P1/C15 |
| **Priorità** | 🟡 Tono più formale |

### M-48 — "structurally saturate" → forzato
| | |
|---|---|
| **Linea** | 44 |
| **Originale** | `...binary one-hot encodings make this measure structurally saturate` |
| **Corretto** | `...binary one-hot encodings cause this measure to saturate structurally` |
| **Fonte** | P1/C16 |
| **Priorità** | 🟡 Più idiomatico |

### M-49 — "diagnostic quantity" → "diagnostic indicator"
| | |
|---|---|
| **Linea** | 44 |
| **Originale** | `...it should be interpreted as a diagnostic quantity rather than as an optimization target.` |
| **Corretto** | `...it should be interpreted as a diagnostic indicator rather than an optimization target.` |
| **Fonte** | P1/C20 |
| **Priorità** | 🟡 Maggiore precisione |

### M-50 — "model-agnostic, and computable without annotations" → riformulare
| | |
|---|---|
| **Linea** | 299 |
| **Originale** | `All metrics are bounded in $[0,1]$, model-agnostic, and computable without annotations beyond the contextual features already in the dataset.` |
| **Corretto** | `All metrics are bounded in $[0,1]$, model-agnostic, and computable from only the contextual features present in the dataset, requiring no additional annotations.` |
| **Fonte** | P1/C19 |
| **Priorità** | 🟡 Scorrevolezza |

### M-51 — "measure whether relevant items are retrieved" → incompleto per nDCG
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `Standard ranking metrics such as nDCG, Recall, MAP, and MRR measure whether relevant items are retrieved` |
| **Corretto** | `Standard ranking metrics such as nDCG, Recall, MAP, and MRR measure whether relevant items are retrieved and ranked highly` |
| **Fonte** | LA #28 |
| **Priorità** | 🟡 Precisione (nDCG/MRR/MAP misurano anche il ranking) |

### M-52 — "ties are broken first by global feature frequency" → ambiguo
| | |
|---|---|
| **Linea** | 12 |
| **Originale** | `ties are broken first by global feature frequency and then by recency` |
| **Corretto** | Specificare: "most frequent globally" o "least frequent globally" |
| **Fonte** | LA #30 |
| **Priorità** | 🟡 Chiarezza |

### M-53 — CR@K formula: manca media sulle query
| | |
|---|---|
| **Linea** | 174 |
| **Originale** | `\mathrm{CR@K} = \frac{1}{K} \sum_{i \in R_K} \frac{|c_q \cap c_i|}{|c_q|}` (per-query) |
| **Corretto** | Aggiungere media esterna: `\mathrm{CR@K} = \frac{1}{|\mathcal{Q}|} \sum_{q \in \mathcal{Q}} \frac{1}{K} \sum_{i \in R_q^K} \frac{|c_q \cap c_i|}{|c_q|}` |
| **Fonte** | LA #34 |
| **Priorità** | 🟡 Allineare formula a definizione testuale |

### M-54 — "IDF-weighting" → "IDF weighting" (non aggettivale)
| | |
|---|---|
| **Linea** | 37 |
| **Originale** | `IDF-weighting prevents high-frequency features...` |
| **Corretto** | `IDF weighting prevents high-frequency features...` |
| **Fonte** | LA #33 |
| **Priorità** | 🟢 Stile |

### M-55 — "feature/context group" → "feature group"
| | |
|---|---|
| **Linea** | 169 |
| **Originale** | `CGB detects whether the model systematically over-covers one feature/context group` |
| **Corretto** | `CGB detects whether the model systematically over-covers one feature group` |
| **Fonte** | LA #35 |
| **Priorità** | 🟢 Pulizia |

### M-56 — "per-item similarity metrics would not reveal" → "may not reveal"
| | |
|---|---|
| **Linea** | 169 |
| **Originale** | `...a failure mode that per-item similarity metrics would not reveal` |
| **Corretto** | `...a failure mode that per-item similarity metrics may not reveal` |
| **Fonte** | LA #36 |
| **Priorità** | 🟢 Più cauto |

### M-57 — "non-relevant" → "irrelevant" o "nonrelevant"
| | |
|---|---|
| **Linea** | 233 |
| **Originale** | `...ranking relevant items above non-relevant ones` |
| **Corretto** | `...ranking relevant items above irrelevant ones` |
| **Fonte** | LA #37 |
| **Priorità** | 🟢 AmE consistency |

### M-58 — `\iffalse` block (linee 52–59) — da pulire
| | |
|---|---|
| **Linee** | 52–59 |
| **Originale** | `\iffalse ... \fi` contenente versione commentata di Friction@K |
| **Corretto** | Eliminare o sostituire con commenti `%` |
| **Fonte** | P1/A6 |
| **Priorità** | 🟡 Pulizia |

### M-59 — Rappresentazione insiemistica del contesto: ambigua
| | |
|---|---|
| **Linea** | 12 |
| **Originale** | Operazioni insiemistiche (`\cap`, `\cup`, `\setminus`) su vettori contestuali |
| **Corretto** | Definire esplicitamente i contesti come insiemi di coppie `{(f, c_f)}` |
| **Fonte** | LA #31 |
| **Priorità** | 🟡 Precisione matematica |

### M-60 — WCS formula (Eq. 11): difficile da leggere
| | |
|---|---|
| **Linea** | 34 |
| **Originale** | WCS su singola linea, denominatore complesso |
| **Corretto** | Riformattare su più linee allineate con numeratore e denominatore chiari |
| **Fonte** | LA #32 |
| **Priorità** | 🟡 Leggibilità |

---

# FILE: 05_experiments.tex

## Sezione 5.1 — Datasets

### M-61 — Yelp: 11 vs 12 feature count
| | |
|---|---|
| **Linee** | 19 vs 543 |
| **Originale** | Riga 19: `11 contextual features` — Riga 543: `twelve contextual features` |
| **Corretto** | **Uniformare**: decidere il numero corretto e usarlo in entrambi i punti |
| **Fonte** | P2/I1, LA #41, #69, #79, #109 |
| **Priorità** | 🔴 **Inconsistenza critica** |

### M-62 — Yelp: feature group names inconsistenti tra 5.1 e 5.5.1
| | |
|---|---|
| **Linee** | 19 vs 543 |
| **Originale** | 5.1: temporal / social and user / spatial — 5.5.1: Temporal / Location / Atmosphere |
| **Corretto** | **Uniformare la tassonomia** in tutto il paper. Se sono due modi diversi di raggruppare, spiegare la differenza |
| **Fonte** | P2/I2, LA #70 |
| **Priorità** | 🔴 **Inconsistenza critica** |

### M-63 — Yelp 5.1: "reviews with ≥ 4 stars treated as positive"
| | |
|---|---|
| **Linea** | 19 |
| **Originale** | `reviews with ≥ 4 stars treated as positive` |
| **Corretto** | `reviews with ratings of at least 4 stars treated as positive interactions` |
| **Fonte** | LA #40 |
| **Priorità** | 🟡 Più formale |

### M-64 — Yelp: "context space" (singolare) ma multiple feature spaces
| | |
|---|---|
| **Linea** | 12 |
| **Originale** | `three datasets spanning distinct recommendation domains, context space, and interaction densities.` |
| **Corretto** | `three datasets spanning distinct recommendation domains, context spaces, and interaction densities.` |
| **Fonte** | LA #38, #39 |
| **Priorità** | 🟢 Accordo di numero |

### M-65 — BGG: "BoardGameGeek community platform" → "the BoardGameGeek"
| | |
|---|---|
| **Linea** | 22 |
| **Originale** | `on the BoardGameGeek (BGG) community platform` — OK in questo caso |
| **Corretto** | Verificato: è già corretto. Nessuna azione. |
| **Fonte** | LA #42 (forse riferito ad altra occorrenza) |
| **Priorità** | 🟢 Già OK |

### M-66 — BGG: "ideal testbed" → "useful testbed"
| | |
|---|---|
| **Linea** | 23 |
| **Originale** | `BGG serves as an ideal testbed for context-aware evaluation` |
| **Corretto** | `BGG serves as a useful testbed for context-aware evaluation` |
| **Fonte** | LA #43 |
| **Priorità** | 🟡 Evita overclaiming |

## Sezione 5.2 — Baselines

### M-67 — Spazio prima della virgola
| | |
|---|---|
| **Linea** | 27 |
| **Originale** | `FM-based models , all trained within the WarpRec framework` |
| **Corretto** | `FM-based models, all trained within the WarpRec framework` |
| **Fonte** | P1/A1, LA #44 |
| **Priorità** | 🔴 Typo |

### M-68 — "the theoretical lower bound" → "a naive baseline"
| | |
|---|---|
| **Linea** | 29 |
| **Originale** | `Random ... represents the theoretical lower bound` |
| **Corretto** | `Random ... represents a naive baseline` (non è un lower bound teorico) |
| **Fonte** | LA #45 |
| **Priorità** | 🟡 Overclaiming |

## Sezione 5.3 — Methodology

### M-69 — Spazio prima di tilde: `Eq. ~\ref{eq:score}` → `Eq.~\ref{eq:score}`
| | |
|---|---|
| **Linea** | 49 |
| **Originale** | `Eq. ~\ref{eq:score}` |
| **Corretto** | `Eq.~\ref{eq:score}` |
| **Fonte** | P1/A5 |
| **Priorità** | 🟢 Spaziatura |

### M-70 — Missing period at end of sentence
| | |
|---|---|
| **Linea** | 50 |
| **Originale** | `...is known at query time \cite{Rashed_2022}` (nessun punto) |
| **Corretto** | `...is known at query time \cite{Rashed_2022}.` |
| **Fonte** | P1/A4, LA #49 |
| **Priorità** | 🔴 Punteggiatura mancante |

### M-71 — "score=−∞" → "a score of −∞"
| | |
|---|---|
| **Linea** | 43 |
| **Originale** | `Items already observed during training are masked with a score=$-\infty$` |
| **Corretto** | `Items already observed during training are masked with a score of $-\infty$` |
| **Fonte** | LA #46 |
| **Priorità** | 🟢 Forma più chiara |

### M-72 — "associated to" → "associated with"
| | |
|---|---|
| **Linea** | 48-49 |
| **Originale** | `the context associated to the interaction` |
| **Corretto** | `the context associated with the interaction` |
| **Fonte** | LA #47 |
| **Priorità** | 🟡 Preposizione corretta |

### M-73 — "all others items" → "all other items"
| | |
|---|---|
| **Linea** | 49 |
| **Originale** | `all others items in the catalog` |
| **Corretto** | `all other items in the catalog` |
| **Fonte** | LA #48 |
| **Priorità** | 🔴 Grammar error |

### M-74 — "on BGG dataset" → "on the BGG dataset"
| | |
|---|---|
| **Linea** | 53 |
| **Originale** | `...for \modelname{} on BGG dataset` |
| **Corretto** | `...for \modelname{} on the BGG dataset` |
| **Fonte** | LA #50 |
| **Priorità** | 🟢 Articolo mancante |

### M-75 — "available upon request" → stronger reproducibility
| | |
|---|---|
| **Linea** | 58 |
| **Originale** | `K=5 results are consistent and available upon request.` |
| **Corretto** | `K=5 results are consistent and reported in Appendix A.` (meglio includere i dati) |
| **Fonte** | LA #51 |
| **Priorità** | 🟡 Riproducibilità |

## Sezione 5.4 — Results

### M-76 — NFM stray number `0.2549` in table
| | |
|---|---|
| **Linea** | 156 |
| **Originale** | `NFM 0.2549 & 0.0312 & 0.0224 & 0.0069 & 0.0607 \\` |
| **Corretto** | `NFM & 0.0312 & 0.0224 & 0.0069 & 0.0607 \\` (rimuovere `0.2549`) |
| **Fonte** | P1/A2, LA #56, #85 |
| **Priorità** | 🔴 **Rompe la tabella** |

### M-77 — "On\textbf{ Frappe}" → "On \textbf{Frappe}"
| | |
|---|---|
| **Linea** | 224 |
| **Originale** | `On\textbf{ Frappe}` |
| **Corretto** | `On \textbf{Frappe}` |
| **Fonte** | P1/A3 |
| **Priorità** | 🔴 Spazio mancante |

### M-78 — "gets better or comparable with other competitors"
| | |
|---|---|
| **Linea** | 219 |
| **Originale** | `...\modelname{} gets better or comparable with other competitors on most of the context-aware metrics` |
| **Corretto** | `...\modelname{} matches or outperforms the competing methods on most context-sensitive metrics` |
| **Fonte** | P1/C8, LA #60 |
| **Priorità** | 🟡 Grammatica + tono |

### M-79 — "evidencing context-gated message passing is able to capture"
| | |
|---|---|
| **Linea** | 225 |
| **Originale** | `...evidencing context-gated message passing is able to capture contextual signals` |
| **Corretto** | `...demonstrating that context-gated message passing captures contextual signals` |
| **Fonte** | P1/C9, LA #66 |
| **Priorità** | 🟡 Verbo atipico + ridondanza |

### M-80 — "the best concordance" → "the best alignment"
| | |
|---|---|
| **Linea** | 227 |
| **Originale** | `...\modelname{} achieving the best concordance on the Environment group` |
| **Corretto** | `...\modelname{} achieving the best alignment on the Environment group` |
| **Fonte** | P1/C10 |
| **Priorità** | 🟡 Terminologia |

### M-81 — "much better fitted to the query context" → "better aligned with"
| | |
|---|---|
| **Linea** | 232 |
| **Originale** | `...its recommendations are much better fitted to the query context geometrically` |
| **Corretto** | `...its recommendations are better geometrically aligned with the query context` |
| **Fonte** | P1/C11, LA #68 |
| **Priorità** | 🟡 Idiomatico |

### M-82 — "in line with its preference for recommending popular items that perfectly match"
| | |
|---|---|
| **Linea** | 237 |
| **Originale** | `...which is in line with its preference for recommending popular items that perfectly match different gaming moods.` |
| **Corretto** | `...which aligns with its tendency to recommend popular items that match different gaming moods.` |
| **Fonte** | P1/C12 |
| **Priorità** | 🟡 Prolisso + overclaiming ("perfectly") |

### M-83 — "non negligible" → "non-negligible"
| | |
|---|---|
| **Linea** | 843 |
| **Originale** | `A non negligible fraction of users` |
| **Corretto** | `A non-negligible fraction of users` |
| **Fonte** | P1/C13, LA #101 |
| **Priorità** | 🟡 Hyphenation |

### M-84 — "as we said in Sec." → "as described in Sec."
| | |
|---|---|
| **Linea** | 204 |
| **Originale** | `as we said in Sec.~\ref{sec:experiments:methodology}` |
| **Corretto** | `as described in Sec.~\ref{sec:experiments:methodology}` |
| **Fonte** | P2/H2, LA #57 |
| **Priorità** | 🟡 Informale |

### M-85 — "ACC is marginally below...a direct consequence of all models on this dataset for which"
| | |
|---|---|
| **Linea** | 228 |
| **Originale** | `ACC is marginally below AFM and DeepFM~(0.0023 vs.\ 0.0026), a direct consequence of all models on this dataset for which exact full-context matches are still quite infrequent.` |
| **Corretto** | `ACC is marginally below AFM and DeepFM (0.0023 vs.\ 0.0026), reflecting that exact full-context matches remain rare for all models on this dataset.` |
| **Fonte** | P2/H4 |
| **Priorità** | 🟡 Sintassi contorta |

### M-86 — "the proposed metrics confirm stronger contextual alignment as well" → "also confirm"
| | |
|---|---|
| **Linea** | 240 |
| **Originale** | `the proposed metrics confirm stronger contextual alignment as well.` |
| **Corretto** | `the proposed metrics also confirm stronger contextual alignment.` |
| **Fonte** | P2/H6 |
| **Priorità** | 🟢 Idiomatico |

### M-87 — "have each similar cardinality" → "have similar cardinalities"
| | |
|---|---|
| **Linea** | 235 |
| **Originale** | `the three feature groups ... have each similar cardinality` |
| **Corretto** | `the three feature groups ... have similar cardinalities` |
| **Fonte** | P2/I4, LA #71 |
| **Priorità** | 🟡 Grammar |

### M-88 — "and thus implying" → "which implies"
| | |
|---|---|
| **Linea** | 234 |
| **Originale** | `...and thus implying representational capacity restriction relative to the baselines.` |
| **Corretto** | `...which implies a representational capacity restriction relative to the baselines.` |
| **Fonte** | P2/I5, LA #70 |
| **Priorità** | 🟡 Grammar |

### M-89 — "for all the cases" → "in all cases"
| | |
|---|---|
| **Linea** | 225 |
| **Originale** | `for all the cases` |
| **Corretto** | `in all cases` |
| **Fonte** | P2/I6, LA #65 |
| **Priorità** | 🟢 Idiomatico |

### M-90 — "with the highest lead on all the datasets" → "largest margins"
| | |
|---|---|
| **Linea** | 224 |
| **Originale** | `...with the highest lead on all the datasets.` |
| **Corretto** | `...with the largest margins observed across the three datasets.` |
| **Fonte** | LA #64 |
| **Priorità** | 🟡 Awkward |

### M-91 — "frequently interacted during training" → "frequently observed during training"
| | |
|---|---|
| **Linea** | 236 |
| **Originale** | `since they are frequently interacted during training` |
| **Corretto** | `since they are frequently observed during training` |
| **Fonte** | LA #72 |
| **Priorità** | 🟡 I gruppi di contesto si osservano, non interagiscono |

### M-92 — "highest on Mood group" → "highest on the Mood group"
| | |
|---|---|
| **Linea** | 237 |
| **Originale** | `Pop scores highest on Mood group` |
| **Corretto** | `Pop scores highest on the Mood group` |
| **Fonte** | LA #73 |
| **Priorità** | 🟢 Articolo mancante |

### M-93 — "manages to beat" → "outperforms"
| | |
|---|---|
| **Linea** | 237 |
| **Originale** | `\modelname{}, despite the embedding constraint, manages to beat all FM-based baselines` |
| **Corretto** | `\modelname{}, despite the embedding constraint, outperforms all FM-based baselines` |
| **Fonte** | LA #74 |
| **Priorità** | 🟡 Informale |

### M-94 — "almost matches" → "nearly matches"
| | |
|---|---|
| **Linea** | 238 |
| **Originale** | `...almost matches AFM on CW-MAP` |
| **Corretto** | `...nearly matches AFM on CW-MAP` |
| **Fonte** | LA #75 |
| **Priorità** | 🟢 Più formale |

### M-95 — "the two metric families separate three distinct evaluation dimensions"
| | |
|---|---|
| **Linea** | 240 |
| **Originale** | `Together, the two metric families separate three distinct evaluation dimensions:` |
| **Corretto** | `Together, standard and context-aware metrics separate three distinct evaluation dimensions:` |
| **Fonte** | LA #76 |
| **Priorità** | 🟡 Chiarezza (più di due famiglie discusse) |

### M-96 — "we can generate more accurate recommendations" → first person
| | |
|---|---|
| **Linea** | 219 |
| **Originale** | `...we can generate more accurate recommendations for specific query conditions.` |
| **Corretto** | `...the model generates recommendations that better match query-specific conditions.` |
| **Fonte** | LA #61 |
| **Priorità** | 🟡 Evita generalizzazione in prima persona |

### M-97 — "rank relevant items higher and do so" → "ranks...does so"
| | |
|---|---|
| **Linea** | 221 |
| **Originale** | `...its recommendations rank relevant items higher and do so in a way that is more fitting for the context.` |
| **Corretto** | `...its recommendations rank relevant items higher and do so in a way that better fits the context.` — OK, ma check soggetto |
| **Fonte** | LA #62 |
| **Priorità** | 🟢 Minor fix |

### M-98 — "score˜ (0.9328)" → stray tilde/space
| | |
|---|---|
| **Linea** | 221 |
| **Originale** | `DeepFM achieves the highest score\~(0.9328)` |
| **Corretto** | `DeepFM achieves the highest score (0.9328)` (rimuovere `\~`) |
| **Fonte** | LA #63 |
| **Priorità** | 🟡 Formattazione |

### M-99 — "better fitted to the query context geometrically and also contextually..." → run-on
| | |
|---|---|
| **Linea** | 231-232 |
| **Originale** | `...which suggest that its recommendations are much better fitted to the query context geometrically and also contextually appropriate items are placed at higher rank positions.` |
| **Corretto** | `...suggesting that its recommendations are better geometrically aligned with the query context and that contextually appropriate items are placed at higher ranks.` |
| **Fonte** | LA #68-69 |
| **Priorità** | 🟡 Run-on sentence |

### M-100 — "and thus implying" (second occurrence, context: BGG)
| | |
|---|---|
| **Linea** | 234 |
| **Originale** | vedi M-88 |
| **Corretto** | vedi M-88 |
| **Priorità** | 🟡 Già coperto |

### M-101 — "We note the improvement" → "We note that the improvement"
| | |
|---|---|
| **Linea** | 130 |
| **Originale** | `We note the improvement of \modelname{} over LightCCF, while consistent, is modest` |
| **Corretto** | `We note that the improvement of \modelname{} over LightCCF, while consistent, is modest` |
| **Fonte** | LA #54 |
| **Priorità** | 🟡 Grammar ("note the improvement...is" → "note that the improvement...is") |

### M-102 — "venue check-ins" → "venue reviews" (Yelp)
| | |
|---|---|
| **Linea** | 167 |
| **Originale** | `...mobile application usage compared to venue check-ins.` |
| **Corretto** | `...mobile application usage compared to venue reviews.` (Yelp è reviews, non check-ins) |
| **Fonte** | LA #55 |
| **Priorità** | 🟡 Precisione |

### M-103 — "high number" → "large number"
| | |
|---|---|
| **Linea** | 205 |
| **Originale** | `The high number of binary contextual features` |
| **Corretto** | `The large number of binary contextual features` |
| **Fonte** | LA #58 |
| **Priorità** | 🟢 Più idiomatico |

### M-104 — "making it impossible to match" → "preventing us from matching"
| | |
|---|---|
| **Linea** | 206-207 |
| **Originale** | `...making it impossible to match the embedding capacity of the baselines.` |
| **Corretto** | `...preventing us from matching the embedding capacity of the baselines.` |
| **Fonte** | LA #59 |
| **Priorità** | 🟡 Meno assoluto |

## Sezione 5.5 — Ablation

### M-105 — "best performing" → "best-performing" (compound adjective)
| | |
|---|---|
| **Linea** | 695 |
| **Originale** | `...using the best performing context feature subset` |
| **Corretto** | `...using the best-performing contextual feature subset` |
| **Fonte** | LA #91, #95 |
| **Priorità** | 🟡 Hyphenation |

### M-106 — "employed in this work" → "used in this study"
| | |
|---|---|
| **Linea** | 537 |
| **Originale** | `...across the datasets employed in this work.` |
| **Corretto** | `...across the datasets used in this study.` |
| **Fonte** | LA #78 |
| **Priorità** | 🟢 Meno verboso |

### M-107 — "relative ranking by nDCG" → "ranking by nDCG"
| | |
|---|---|
| **Linea** | 554 |
| **Originale** | `The configurations and their relative ranking by nDCG are summarized` |
| **Corretto** | `The configurations ranked by nDCG are summarized` |
| **Fonte** | LA #82 |
| **Priorità** | 🟢 Più diretto |

### M-108 — "confirming the results of prior works" → "consistent with prior work"
| | |
|---|---|
| **Linea** | 557 |
| **Originale** | `...confirming the results of prior works` |
| **Corretto** | `...consistent with prior work` |
| **Fonte** | LA #83 |
| **Priorità** | 🟢 Idiomatico |

### M-109 — "all features of Yelp dataset" → "all features of the Yelp dataset"
| | |
|---|---|
| **Linea** | 557 |
| **Originale** | `among all features of Yelp dataset` |
| **Corretto** | `among all features of the Yelp dataset` |
| **Fonte** | LA #84 |
| **Priorità** | 🟢 Articolo mancante |

### M-110 — "which we can partition" → "which we partition"
| | |
|---|---|
| **Linea** | 587 |
| **Originale** | `...which we can partition into three semantic groups.` |
| **Corretto** | `...which we partition into three semantic groups.` |
| **Fonte** | LA #85 |
| **Priorità** | 🟢 Più diretto |

### M-111 — "features specify the conditions under which the mobile app is used" → circolare
| | |
|---|---|
| **Linea** | 587 |
| **Originale** | `Activity features specify the conditions under which the mobile app is used` |
| **Corretto** | `Activity features describe usage conditions such as homework status and data-cost concern.` |
| **Fonte** | LA #86 |
| **Priorità** | 🟡 Chiarezza |

### M-112 — "as partially demonstrated in literature" → "as suggested by prior work"
| | |
|---|---|
| **Linea** | 596 |
| **Originale** | `...as partially demonstrated in literature` |
| **Corretto** | `...as suggested by prior work` |
| **Fonte** | LA #88 |
| **Priorità** | 🟡 Tono |

### M-113 — "potential interference between these two groups" → "suggesting possible interference"
| | |
|---|---|
| **Linea** | 597 |
| **Originale** | `...indicating potential interference between these two groups` |
| **Corretto** | `...suggesting possible interference between these two groups` |
| **Fonte** | LA #89 |
| **Priorità** | 🟢 Cauto (interpretazione, non fatto) |

### M-114 — "We hypothesize this is due to" → "We hypothesize that this is due to"
| | |
|---|---|
| **Linea** | 679 |
| **Originale** | `We hypothesize this is due to the architectural design` |
| **Corretto** | `We hypothesize that this is due to the architectural design` |
| **Fonte** | LA #92 |
| **Priorità** | 🟡 Grammar |

### M-115 — "such models" → "these models"
| | |
|---|---|
| **Linea** | 679 |
| **Originale** | `...the architectural design of such models` |
| **Corretto** | `...the architectural design of these models` |
| **Fonte** | LA #93 |
| **Priorità** | 🟢 Più diretto |

### M-116 — "ranking of configurations is stable" → "the ranking of configurations"
| | |
|---|---|
| **Linea** | 681 |
| **Originale** | `ranking of configurations is stable` |
| **Corretto** | `the ranking of configurations is stable` |
| **Fonte** | LA #94 |
| **Priorità** | 🟢 Articolo mancante |

## Sezione 5.6 — Context-Aware Validation

### M-117 — "their positive item" → "the user's positive item"
| | |
|---|---|
| **Linea** | 696 |
| **Originale** | `...a user is considered a hit if their positive item appears` |
| **Corretto** | `...a user is considered a hit if the user's positive item appears` |
| **Fonte** | LA #96 |
| **Priorità** | 🟡 Formale (singular they è accettabile ma meno formale) |

### M-118 — "hit rate degradation" → "hit-rate degradation" (aggettivo)
| | |
|---|---|
| **Linea** | 745-747 |
| **Originale** | `hit rate degradation` |
| **Corretto** | `hit-rate degradation` quando usato come compound adjective |
| **Fonte** | LA #97 |
| **Priorità** | 🟢 Hyphenation |

### M-119 — "retrieve a positive item" → "retrieve the positive item"
| | |
|---|---|
| **Linea** | 811 |
| **Originale** | `...manages to retrieve a positive item that is not surfaced` |
| **Corretto** | `...retrieves the positive item that is not surfaced` |
| **Fonte** | LA #98, #74 |
| **Priorità** | 🟡 L'item è specifico (held-out) |

### M-120 — "no observable effect on the final ranking" → più preciso
| | |
|---|---|
| **Linea** | 843 |
| **Originale** | `...the validation objective has no observable effect on the final ranking.` |
| **Corretto** | `...the validation objective has no observable effect on the rank of the held-out positive item.` |
| **Fonte** | LA #102 |
| **Priorità** | 🟡 Precisione |

---

# FILE: 06_conclusions.tex

### M-121 — "context-aware benefits" → "the benefits of context-awareness"
| | |
|---|---|
| **Linea** | 8 |
| **Originale** | `...showing that context-aware benefits extend beyond accuracy.` |
| **Corretto** | `...showing that the benefits of context-awareness extend beyond accuracy.` |
| **Fonte** | P1/C17 |
| **Priorità** | 🟡 Ambiguità semantica |

### M-122 — "confirms the optimal context feature subset is dataset-dependent" → "confirms that"
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `The ablation study confirms the optimal context feature subset is dataset-dependent` |
| **Corretto** | `The ablation study confirms that the optimal contextual feature subset is dataset-dependent` |
| **Fonte** | LA #108 |
| **Priorità** | 🟡 Grammar + terminologia |

### M-123 — "standard accuracy measures alone miss" → "can miss"
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `...standard accuracy measures alone miss contextual degradation.` |
| **Corretto** | `...standard accuracy measures alone can miss contextual degradation.` |
| **Fonte** | LA #109 |
| **Priorità** | 🟡 Più cauto |

### M-124 — "continuous context" → "continuous contextual variables"
| | |
|---|---|
| **Linea** | 10 |
| **Originale** | `Future work includes extending to continuous context` |
| **Corretto** | `Future work includes extending to continuous contextual variables` |
| **Fonte** | LA #110 |
| **Priorità** | 🟢 Precisione |

### M-125 — Prima frase della conclusione: troppo densa
| | |
|---|---|
| **Linea** | 6 |
| **Originale** | Frase unica che elenca modello + 9 metriche |
| **Corretto** | Dividere in due frasi: una per il modello, una per le metriche |
| **Fonte** | LA #107 |
| **Priorità** | 🟡 Leggibilità |

### M-126 — Vecchie conclusioni commentate (linee 12-22)
| | |
|---|---|
| **Linee** | 12-22 |
| **Originale** | Grandi blocchi di vecchia versione delle conclusioni commentati |
| **Corretto** | Eliminare |
| **Fonte** | P1/F1 |
| **Priorità** | 🟢 Pulizia |

---

# FILE: _references.bib

### M-127 — Reference [1]: "Information systems" → "Information Systems"
| | |
|---|---|
| **Linea** | N/A |
| **Originale** | `Information systems` |
| **Corretto** | `Information Systems` (se è titolo di opera) |
| **Fonte** | LA #111 |
| **Priorità** | 🟢 Capitalizzazione |

### M-128 — References [10] and [11]: possibili duplicati
| | |
|---|---|
| **Linee** | N/A |
| **Originale** | Due entry quasi identiche |
| **Corretto** | Verificare se sono lo stesso lavoro; se sì, unire |
| **Fonte** | LA #112 |
| **Priorità** | 🟡 Possibile sciatteria |

### M-129 — References [23], [27], [35]: web resources senza access date
| | |
|---|---|
| **Linee** | N/A |
| **Originale** | Voci bibliografiche da web senza data di accesso |
| **Corretto** | Aggiungere access date se richiesto dal template ACM |
| **Fonte** | LA #113 |
| **Priorità** | 🟡 Completezza |

### M-130 — Reference [27]: arXiv 2026 — verifica anonimato
| | |
|---|---|
| **Linee** | N/A |
| **Originale** | Riferimento a preprint 2026 |
| **Corretto** | Verificare che non riveli identità degli autori |
| **Fonte** | LA #114 |
| **Priorità** | 🟡 Double-blind |

### M-131 — Capitalizzazione inconsistente nei titoli dei riferimenti
| | |
|---|---|
| **Linee** | Tutti |
| **Originale** | Stili di capitalization misti |
| **Corretto** | Allineare allo stile ACM bibliography |
| **Fonte** | LA #118 |
| **Priorità** | 🟢 Consistenza |

---

## APPENDICE: Note globali di stile da applicare su tutto il paper

Le seguenti regole vanno applicate **globalmente** su tutti i file `.tex`:

| # | Regola | Dettaglio |
|---|--------|-----------|
| S1 | "context-sensitive metrics" come umbrella term | Usare "context-similarity metrics" per ACC/CS/WCS/WCA/Friction; "context-dynamics metrics" per CR/CGB; "context-weighted ranking metrics" per CW-nDCG/CW-MAP |
| S2 | "higher-order" UNIFORME | Sostituire tutte le occorrenze di "high-order" con "higher-order" |
| S3 | "message passing" / "message-passing" | "message passing" come nome; "message-passing" come aggettivo |
| S4 | "user-item" / "user–item" | Scegliere uno stile (hyphen o en-dash) e usarlo consistentemente |
| S5 | "Section" vs "Sec." | Usare "Section" in prosa, "Sec." solo in tabelle/caption |
| S6 | Verbi informali da sostituire | "gets"→"achieves", "beats"→"outperforms", "manages to"→(rimuovere), "as we said"→"as noted" |
| S7 | Rimuovere overclaiming | "ideal"→"useful", "theoretical lower bound"→"naive baseline", "perfectly"→(rimuovere) |
| S8 | TUTTI i \textcolor{red/blue} commenti | Rimuovere prima della submission |
| S9 | TUTTI i commenti con nomi (Iván, Alejandro) | Rimuovere per double-blind |
| S10 | "context-aware metrics" → "context-sensitive metrics" | Dove possibile, usare "context-sensitive" per la famiglia di metriche |

---

*Fine del report. 131 issue totali, organizzati per file in ordine di comparsa nel paper.*
