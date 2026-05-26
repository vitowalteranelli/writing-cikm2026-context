# Section-by-Section Rewrite Plan — Versione Corretta (A*-ready)

Questo file contiene le stesse modifiche proposte nell'originale [`output/section-by-section-rewrite-plan.md`](output/section-by-section-rewrite-plan.md), ma con tutti i phrasing inadatti a un paper A* corretti.

> **Nota:** Le intestazioni, le spiegazioni ("Why") e le valutazioni ("Best-paper gate") rimangono invariate perché sono meta-commento interno. Solo i blocchi LaTeX (il testo che finirà nel paper) sono stati corretti.

---

## Indice dei problemi identificati

| Termine/Costrutto | Occorrenze | Problema | Gravità |
|---|---|---|---|
| `attractive` | 2 (intro, related work) | Promozionale, da brochure | **Alta** |
| `lightweight` | 10+ (abstract, intro×2, related work×4, model, results, conclusion) | Ripetitivo, sovrausato; accettabile 1-2 volte | **Media** |
| `heavyweight` | 1 (intro) | Colloquiale | Media |
| `strongest` | 5+ (intro, results×2, ablation, conclusion) | Superlativo da overclaiming | **Alta** |
| `leads on` | 2 (results) | Linguaggio sportivo/giornalistico | **Alta** |
| `tied with` | 1 (results) | Linguaggio sportivo | **Alta** |
| `good sign` | 1 (results) | Colloquiale, da conversazione | **Alta** |
| `does not beat` | 1 (results) | Colloquiale | **Alta** |
| `that is not a contradiction` | 1 (results) | Difensivo, colloquiale | **Alta** |
| `clearest gain` | 1 (results) | Informale | Media |
| `exactly what we should expect` | 1 (results) | Tonodifensivo | **Alta** |
| `one-size-fits-all` | 1 (results) | Metafora colloquiale | Media |
| `simple conclusion` | 1 (conclusion) | Sminuisce la conclusione | **Alta** |
| `right complexity point` | 1 (model section desc) | Gergale | Media |
| `good test` | 1 (Frappe desc) | Colloquiale | Media |
| `stress test` | 1 (Yelp desc) | Informale | Media |
| `cleanest benchmark` | 1 (BGG desc) | Superlativo soggettivo | Media |
| `intentionally modest` | 1 (qualitative validation) | Apologetico | Media |
| `important negative finding` | 1 (qualitative validation) | Sovrastima | Media |
| `much lower` | 1 (metrics section) | Impreciso | Bassa |
| `the paper supports a simple conclusion` | 1 (conclusion) | "Supports" + "simple" = tono debole | **Alta** |

---

## Blocchi LaTeX Corretti

### Modifica 0.2: Abstract

**Originale:**
> `\modelname, a lightweight graph-based recommender that injects discrete contextual features into edge representations, gates message passing with context, and augments scoring with an explicit context-item compatibility term.`

**Corretto:**
> `\modelname, a graph-based recommender that encodes discrete contextual features into edge representations, gates message passing with context, and augments scoring with an explicit context-item compatibility term.`

**[Motivazione:]** "lightweight" rimosso perché ridondante — la descrizione "graph-based" è sufficiente. "Injects" sostituito con "encodes" (più preciso, meno gergale). "preserves the efficiency of LightGCN-style propagation" già comunica l'efficienza.

---

### Modifica 1.1: Introduzione — Paragrafo GNN

**Originale (riga 60):**
> `Graph neural network (GNN) recommenders are attractive in this setting because they can model high-order collaborative structure with relatively little architectural overhead. Yet existing GNN-based recommenders typically focus on user--item connectivity and either omit context or inject it in ways that do not affect propagation itself. This leaves open the question of how to make GNN recommendation context-sensitive without turning the model into a heavyweight architecture.`

**Corretto:**
> `Graph neural network (GNN) recommenders are well-suited to this setting because they model high-order collaborative structure with relatively little architectural overhead~\cite{wu2022graph,sattar2023graph,gao2023survey}. Yet existing GNN-based recommenders typically focus on user--item connectivity and either omit context or incorporate it in ways that do not affect propagation itself~\cite{mateos2025systematic}. This raises the question of how to achieve context-sensitive GNN recommendation without incurring the cost of a substantially more complex architecture.`

**[Motivazione:]** "attractive" → "well-suited" (obiettivo, non promozionale). "inject" → "incorporate" (più neutro). "heavyweight" → "substantially more complex" (più preciso, meno colloquiale). "leaves open the question of how to make" → "raises the question of how to achieve" (più formale).

---

### Modifica 1.1: Introduzione — Paragrafo proposta

**Originale (riga 62):**
> `To address this gap, we propose \modelname, a lightweight context-aware graph recommender that embeds contextual features on interaction edges, uses those contextual embeddings to gate message passing, and adds an explicit context-item compatibility term at scoring time.`

**Corretto:**
> `To address this gap, we propose \modelname, a context-aware graph recommender that embeds contextual features on interaction edges, uses the resulting representations to gate message passing, and introduces an explicit context-item compatibility term at scoring time.`

**[Motivazione:]** "lightweight" rimosso (già implicito nella descrizione). "those contextual embeddings" → "the resulting representations" (più preciso). "adds" → "introduces" (più formale).

---

### Modifica 1.1: Roadmap

**Originale (riga 64):**
> `the benefit of contextual modeling is dataset dependent: it is strongest when the context space is informative and not too sparse, and it becomes more nuanced when memory constraints or highly balanced context groups limit the room for separation.`

**Corretto:**
> `the benefit of contextual modeling is dataset dependent: it is most pronounced when the context space is informative and not overly sparse, and it becomes more nuanced when memory constraints or highly balanced context groups limit the observable separation between models.`

**[Motivazione:]** "strongest" → "most pronounced" (superlativo meno aggressivo). "not too sparse" → "not overly sparse" (più formale). "limit the room for separation" → "limit the observable separation between models" (più preciso).

---

### Modifica 2.1: Related Work — CARS positioning

**Originale (riga 81):**
> `Pre-filtering and post-filtering are attractive because they can reuse standard recommenders with limited engineering overhead, but both keep context outside the core representation-learning loop.`

**Corretto:**
> `Pre-filtering and post-filtering are appealing from a practical standpoint because they can reuse standard recommenders with limited engineering overhead, but both keep context outside the core representation-learning loop.`

**[Motivazione:]** "attractive" → "appealing from a practical standpoint" (più preciso, meno vago). Oppure si può usare "advantageous" o "pragmatic".

---

### Modifica 2.1: Related Work — Chiusura positioning

**Originale (riga 87):**
> `It is a lightweight contextualization of graph collaborative filtering in which context is attached to interactions and directly modulates message passing.`

**Corretto:**
> `It is a compact contextualization of graph collaborative filtering in which context is attached to interactions and directly modulates message passing.`

**[Motivazione:]** "lightweight" → "compact" (variazione desiderabile, ugualmente preciso).

---

### Modifica 2.2: Related Work — Chiusura GNN subsection

**Originale (riga 105):**
> `Relative to generic GNN recommenders~\cite{wu2022graph,sattar2023graph}, it avoids heavyweight relational graph redesign and keeps a lightweight collaborative-filtering backbone.`

**Corretto:**
> `Relative to generic GNN recommenders~\cite{wu2022graph,sattar2023graph}, it avoids elaborate relational graph redesign and retains an efficient collaborative-filtering backbone.`

**[Motivazione:]** "heavyweight" → "elaborate" (più preciso). "lightweight" → "efficient" (più formale, meno marketing). "keeps" → "retains" (più formale).

---

### Modifica 2.2: Related Work — Disentanglement positioning

**Originale (riga 111):**
> `whereas our model uses direct contextual gating to adapt propagation with minimal architectural overhead.`

**Corretto:**
> `whereas our model uses direct contextual gating to condition propagation with low architectural overhead.`

**[Motivazione:]** "adapt" → "condition" (termine tecnico più preciso in context-aware recommedation). "minimal" → "low" (meno iperbolico).

---

### Modifica 2.2: Related Work — Chiusura

**Originale (riga 115):**
> `(i) we inherit lightweight graph collaborative filtering from LightGCN/LightCCF`

**Corretto:**
> `(i) we inherit efficient graph collaborative filtering from LightGCN/LightCCF`

**[Motivazione:]** "lightweight" sostituito con "efficient" per evitare l'ennesima ripetizione.

---

### Modifica 3.3: Model — Titolo e descrizione

**Originale (titoloe descrizione):**
> `Reframe the message passing as a deliberate lightweight design choice`
> `The rewrite should explain *why* multiplicative gating is the right complexity point and why mean pooling is retained.`

**Corretto:**
> `Reframe the message passing as a deliberate efficiency-oriented design choice`
> `The rewrite should explain *why* multiplicative gating achieves the appropriate complexity-efficiency trade-off and why mean pooling is retained.`

**[Motivazione:]** Il titolo e la descrizione sono meta-commento, ma è meglio evitarli anche lì. "right complexity point" → "appropriate complexity-efficiency trade-off".

---

### Modifica 3.3: Model — Paragrafo propagazione

**Originale (riga 159–160):**
> `Standard LightGCN~\cite{he2020lightgcnsimplifyingpoweringgraph} propagates node embeddings along graph edges without relational modulation. Inspired by feature-aware edge modulation~\cite{zhuo2025edgegflrethinkingedgeinformation}, we instead use the contextual edge vector $\mathbf{r}_{uv}$ as a feature-wise filter: every dimension of the neighbor embedding is scaled by the corresponding dimension of the context representation. This keeps the propagation linear and scalable while making message passing sensitive to the current context.`

**Corretto:**
> `Standard LightGCN~\cite{he2020lightgcnsimplifyingpoweringgraph} propagates node embeddings along graph edges without relational modulation. Building on the principle of feature-aware edge modulation~\cite{zhuo2025edgegflrethinkingedgeinformation}, we instead use the contextual edge vector $\mathbf{r}_{uv}$ as a feature-wise filter: each dimension of the neighbor embedding is scaled by the corresponding dimension of the context representation. This preserves the linearity and scalability of the propagation while making message passing sensitive to the current context.`

**[Motivazione:]** "Inspired by" → "Building on the principle of" (più tecnico, meno vago). "every dimension" → "each dimension" (più preciso in contesto matematico). "keeps" → "preserves" (più formale).

---

### Modifica 4.1: Metrics — WCA interpretazione

**Originale:**
> `WCA should be interpreted as a diagnostic quantity rather than as a primary ranking signal.`

**Corretto:**
> `WCA should be interpreted as a diagnostic quantity rather than as an optimization target or a primary ranking signal.`

**[Motivazione:]** Chiarimento utile: specificare cosa NON è, oltre a cosa è.

---

### Modifica 4.2: Metrics — Family 3

**Originale (riga 257):**
> `The resulting scores are easy to interpret: if they are close to the standard ranking metrics, the model retrieves relevant items in contextually appropriate situations; if they are much lower, the model retrieves relevant items but in the wrong context.`

**Corretto:**
> `The resulting scores are straightforward to interpret: when they approximate the standard ranking metrics, the model retrieves relevant items in contextually appropriate situations; when they are substantially lower, the model retrieves relevant items but in mismatched contexts.`

**[Motivazione:]** "easy to interpret" → "straightforward to interpret" (più formale). "if they are close" → "when they approximate" (più preciso). "much lower" → "substantially lower" (più preciso). "in the wrong context" → "in mismatched contexts" (più tecnico).

---

### Modifica 5.1: Dataset descriptions — Frappe

**Originale (riga 273):**
> `It is useful because its context space is sparse and heterogeneous, which makes it a good test of whether context-gated propagation can exploit informative but irregular context signals.`

**Corretto:**
> `It is useful because its context space is sparse and heterogeneous, which makes it an informative test case for whether context-gated propagation can exploit informative but irregular context signals.`

**[Motivazione:]** "a good test" → "an informative test case" (più preciso, meno colloquiale).

---

### Modifica 5.1: Dataset descriptions — Yelp

**Originale (riga 275):**
> `Its high-cardinality spatial features make it the most contextually complex benchmark in the study and therefore a good stress test for context-aware evaluation.`

**Corretto:**
> `Its high-cardinality spatial features make it the most contextually complex benchmark in the study and therefore a challenging evaluation setting for context-aware metrics.`

**[Motivazione:]** "a good stress test" → "a challenging evaluation setting" (più formale, meno gergale).

---

### Modifica 5.1: Dataset descriptions — BGG

**Originale (riga 277):**
> `It is the cleanest benchmark for studying context-aware ranking because the playing situation strongly determines which item is appropriate.`

**Corretto:**
> `It is the most suitable benchmark for studying context-aware ranking because the playing situation strongly determines which item is appropriate.`

**[Motivazione:]** "cleanest" → "most suitable" (superlativo meno soggettivo, più tecnico).

---

### Modifica 5.2: Baselines

**Originale (riga 287):**
> `We compare \modelname{} against three non-contextual baselines and five context-aware FM-based models, all trained within the WarpRec framework~\cite{warprec}.`

**Corretto:**
> (Nessun cambiamento necessario — il testo è già pulito.)

---

### Modifica 5.4: Results narrative

**Originale (riga 325):**
> `the benefit of context gating is strongest when the dataset has informative context and enough structure for the context encoder to exploit`

**Corretto:**
> `the benefit of context gating is most evident when the dataset has informative context and sufficient structure for the context encoder to exploit`

**[Motivazione:]** "strongest" → "most evident" (superlativo meno aggressivo). "enough" → "sufficient" (più formale).

---

### Modifica 5.4: Standard ranking metrics

**Originale (riga 328):**
> `On Yelp, \modelname{} is the strongest model on all four standard ranking metrics, which suggests that context-aware propagation and context-aware scoring improve classic recommendation quality when the context space is rich but not excessively sparse. On Frappe, \modelname{} again leads on nDCG@10, MRR@10, and Recall@10, while Precision@10 is tied with AFM. This is a good sign: the model is not only effective on a large-scale dataset, but it also remains competitive on a smaller and sparser benchmark where contextual variation is important. On BGG, however, the ranking picture is more nuanced. \modelname{} remains competitive and outperforms the FM-based baselines, but it does not beat the strongest graph baseline in the standard ranking setting because its embedding size is reduced to fit the available GPU memory.`

**Corretto:**
> `On Yelp, \modelname{} achieves the highest scores across all four standard ranking metrics, which suggests that context-aware propagation and context-aware scoring improve classic recommendation quality when the context space is rich without being excessively sparse. On Frappe, \modelname{} again obtains the best nDCG@10, MRR@10, and Recall@10, while Precision@10 is comparable to AFM. This pattern is consistent with the hypothesis that the model generalizes beyond large-scale settings and remains effective on a smaller, sparser benchmark where contextual variation is important. On BGG, however, the ranking picture is more nuanced. \modelname{} remains competitive and outperforms the FM-based baselines, but it does not surpass the leading graph baseline in the standard ranking setting because its embedding size is reduced to satisfy GPU memory constraints.`

**[Motivazione:]** 
- "strongest model" → "achieves the highest scores" (obiettivo, non celebrativo)
- "leads on" → "obtains the best" (elimina linguaggio sportivo)
- "tied with" → "comparable to" (elimina linguaggio sportivo)
- "good sign" → "pattern is consistent with the hypothesis" (analitico, non colloquiale)
- "does not beat" → "does not surpass" (più formale)
- "strongest graph baseline" → "leading graph baseline" (meno superlativo)
- "to fit the available GPU memory" → "to satisfy GPU memory constraints" (più preciso)

---

### Modifica 5.4: Context-aware metrics

**Originale (riga 331):**
> `On Yelp and Frappe, \modelname{} leads on most of the similarity, coverage, and context-weighted ranking metrics, which indicates that the gains seen in standard ranking are accompanied by stronger contextual alignment. On BGG, the model achieves its clearest gain on geometric alignment and context-weighted ranking, while some group-balanced or exact-match metrics remain high for simpler baselines such as Popularity. That is not a contradiction: it shows that the different metrics are measuring different failure modes.`

**Corretto:**
> `On Yelp and Frappe, \modelname{} achieves the highest scores on most similarity, coverage, and context-weighted ranking metrics, which indicates that the improvements observed in standard ranking are accompanied by stronger contextual alignment. On BGG, the model shows its most substantial improvement on geometric alignment and context-weighted ranking, while some group-balanced or exact-match metrics remain higher for simpler baselines such as Popularity. This is expected: the different metrics are designed to capture distinct failure modes, and their divergence confirms that the framework separates these cases rather than collapsing them into a single score.`

**[Motivazione:]** 
- "leads on" → "achieves the highest scores on" (formale)
- "clearest gain" → "most substantial improvement" (più preciso)
- "That is not a contradiction" → "This is expected" (elimina tonodifensivo, trasforma in affermazione di design)
- Aggiunta spiegazione su perché la divergenza è attesa

---

### Modifica 5.4: Overall paragraph

**Originale (riga 334):**
> `Third, the strongest gains are dataset dependent, which is exactly what we should expect from a context-sensitive method rather than a one-size-fits-all architecture.`

**Corretto:**
> `Third, the most substantial gains are dataset dependent, which is consistent with the behavior of a context-sensitive method that responds to dataset-specific structure rather than a general-purpose architecture.`

**[Motivazione:]** 
- "strongest" → "most substantial" (meno superlativo)
- "exactly what we should expect" → "consistent with the behavior of" (elimina tonodifensivo)
- "one-size-fits-all" → "general-purpose" (meno metaforico, più tecnico)

---

### Modifica 5.5: Ablation

**Originale (riga 347):**
> `On Yelp, the strongest configuration combines Temporal and Location features`

**Corretto:**
> `On Yelp, the best-performing configuration combines Temporal and Location features`

**[Motivazione:]** "strongest" → "best-performing" (più oggettivo, misurabile).

---

### Modifica 5.6: Qualitative validation

**Originale (riga 366):**
> `The result is intentionally modest: context-weighted validation changes the ranking behavior in some cases, but it does not produce a uniform hit-rate improvement across datasets. This is an important negative finding because it suggests that context-aware validation is not automatically better than standard ranking validation.`

**Corretto:**
> `The result is deliberately conservative: context-weighted validation changes the ranking behavior in some cases, but it does not produce a uniform improvement in hit rate across datasets. This negative result is informative because it indicates that context-aware validation is not uniformly superior to standard ranking validation.`

**[Motivazione:]** 
- "intentionally modest" → "deliberately conservative" (più tecnico, meno apologetico)
- "hit-rate improvement" → "improvement in hit rate" (più chiaro)
- "important negative finding" → "negative result is informative" (meno sovrastimato, più misurato)
- "automatically better" → "uniformly superior" (più formale, meno colloquiale)

---

### Modifica 5.7: Limitations

**Originale (riga 381):**
> `the results should be read as strong descriptive evidence rather than as statistically certified superiority.`

**Corretto:**
> `the results should be interpreted as descriptive evidence rather than as statistically validated claims of superiority.`

**[Motivazione:]** "read as" → "interpreted as" (più formale). "certified" → "validated" (più tecnico).

---

### Modifica 6.1: Conclusion — Risultati

**Originale (riga 397):**
> `The experiments show that the benefit of context-aware propagation is real but dataset dependent: it is strongest on Yelp and Frappe`

**Corretto:**
> `The experiments show that the benefit of context-aware propagation is substantial yet dataset dependent: it is most pronounced on Yelp and Frappe`

**[Motivazione:]** "real but" → "substantial yet" (più formale, meno colloquiale). "strongest" → "most pronounced" (superlativo meno aggressivo).

---

### Modifica 6.1: Conclusion — Chiusura

**Originale (riga 399):**
> `Overall, the paper supports a simple conclusion: context should be modeled as part of the interaction structure, but it should also be evaluated as part of the ranking task.`

**Corretto:**
> `Overall, the paper supports a clear conclusion: context should be modeled as part of the interaction structure and, correspondingly, evaluated as part of the ranking task.`

**[Motivazione:]** "simple conclusion" → "clear conclusion" ("simple" sminuisce; "clear" è assertivo senza essere arrogante). Struttura "X and, correspondingly, Y" più elegante di "X, but Y".

---

## Riepilogo delle correzioni per categoria

| Categoria | Termini originali | Sostituzioni |
|---|---|---|
| Promozionale | `attractive` | `well-suited`, `appealing from a practical standpoint` |
| Superlativi overclaiming | `strongest` (×5), `cleanest` | `most pronounced`, `most evident`, `best-performing`, `leading`, `most suitable` |
| Linguaggio sportivo | `leads on`, `tied with` | `achieves the highest`, `obtains the best`, `comparable to` |
| Colloquiale | `good sign`, `does not beat`, `good test`, `stress test`, `inject`, `real but` | `pattern is consistent`, `does not surpass`, `informative test case`, `challenging evaluation setting`, `encode`/`incorporate`, `substantial yet` |
| Difensivo | `not a contradiction`, `exactly what we should expect` | `this is expected`, `consistent with the behavior of` |
| Tonodebole | `simple conclusion`, `supports` | `clear conclusion` |
| Apologetico | `intentionally modest`, `important negative finding` | `deliberately conservative`, `informative negative result` |
| Gergale | `right complexity point`, `one-size-fits-all` | `appropriate complexity-efficiency trade-off`, `general-purpose` |
| Impreciso | `much lower` | `substantially lower`, `markedly lower` |
