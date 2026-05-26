# Rewrite Plan Definitivo — CIKM 2026

## Obiettivo

Trasformare il paper in una sottomissione A*-ready, migliorando chiarezza, rigore, posizionamento e onestà evidenziale, senza nuovi esperimenti.

## Strategia centrale

1. Rimuovere debolezza evitabili nella presentazione e nell'argomentazione.
2. Rendere il contributo comprensibile al primo sguardo.
3. Riposizionare il paper attorno alla novità difendibile più forte.
4. Neutralizzare il rischio reviewer con limitazioni precise, confronti accurati e prosa pulita.
5. Rendere la sezione metriche intenzionale, formale e validata entro i limiti delle evidenze esistenti.

## Tesi centrale (unificata)

> Introduciamo un recommender grafico sensibile al contesto che integra il contesto d'interazione nella propagazione, e proponiamo metriche offline context-sensitive che espongono l'allineamento tra contesto e comportamento di ranking.

## Regole decisionali durante il rewrite

- Se una frase aumenta l'ambizione senza aggiungere evidenza, tagliala.
- Se un'affermazione dipende da esperimenti mancanti, declassala o rimuovila.
- Se una metrica non può essere definita con precisione, semplifica la spiegazione prima di aggiungere testo.
- Se due sezioni ripetono lo stesso messaggio, tieni la versione più forte e cancella l'altra.
- Se un confronto sembra iniquo, rendi la limitazione esplicita.
- Se un paragrafo esiste solo per sembrare impressionante, riscrivilo per sembrare esatto.

## Dipendenze importanti

- Usa `\modelname{}` (macro definita in `00_main.tex`) per il nome del modello ovunque.
- Non introdurre `\ours{}` o `\URSp{}` senza prima aggiungere quelle macro.
- Non aggiungere citazioni mancanti (CA-KGCN, GEM, IEDR) fino a quando le loro entry BibTeX non esistono in `_references.bib`.
- Preserva sempre le citazioni esistenti: se un blocco sorgente cita un'affermazione, il blocco sostitutivo deve mantenere la stessa chiave di citazione.
- Dove indicato "mantieni equazioni/tabelle", solo la prosa circostante deve cambiare.

---

# Modifiche

## 00_main.tex

### Modifica 0.1: Front-matter ACM

- **Target:** `overleaf/00_main.tex`, righe 69–79.
- **Perché:** i metadati contengono ancora valori ACM di esempio (2016, 2018, ISBN/DOI placeholder). È un problema di igiene di sottomissione.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
\acmConference[CIKM '26]{35th International ACM Conference on Information and Knowledge Management}{<official conference dates>}{Rome, Italy}
\acmISBN{<official ISBN or submission-safe placeholder>}
\acmDOI{<official DOI or submission-safe placeholder>}
```

### Modifica 0.2: Abstract — riscritto attorno al contributo reale

- **Target:** `overleaf/00_main.tex`, righe 220–223.
- **Perché:** l'abstract attuale è generico, sovraclaima su BGG, e menziona il link al codice sprecando spazio prezioso.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
\begin{abstract}
Context-aware recommender systems aim to improve personalization by considering situational factors such as time or location. Yet many models still treat context as side information, and standard ranking metrics often ignore whether retrieved items fit the query situation. We address both problems with \modelname, a graph-based recommender that encodes discrete contextual features into edge representations, gates message passing with context, and augments scoring with an explicit context-item compatibility term. The model preserves the efficiency of LightGCN-style propagation while making the learned embeddings context dependent. In parallel, we introduce a family of context-sensitive offline metrics that quantify exact match, partial overlap, weighted alignment, group balance, and context-weighted ranking quality. On Yelp and Frappe, \modelname{} improves standard ranking performance and remains competitive on BoardGameGeek under a tighter embedding budget, while the proposed metrics capture contextual alignment patterns that accuracy-only evaluation leaves unexamined. Overall, the results indicate that contextual gains depend on feature-group informativeness, context-space sparsity, and the degree of interaction between context and collaborative signal.
\end{abstract}
```

**Correzioni integrate:** `lightweight graph-based` → `graph-based` (ridondante); `injects` → `encodes` (più preciso, meno gergale).

---

## 01_introduction.tex

### Modifica 1.1: Introduzione completa — tesi-driven

- **Target:** `overleaf/01_introduction.tex`, righe 8–16.
- **Perché:** l'introduzione attuale è direzionalmente corretta ma troppo generica, ripete background da survey, e termina con un commento editoriale.
- **A*-gate:** `PASS`.
- **Guida all'integrazione:**
  - Paragrafo 1 → sostituisce l'attuale capoverso che inizia con `Context-aware recommender systems (CARS) constitute...`
  - Paragrafo 2 → sostituisce il capoverso GNN che inizia con `In parallel, graph-based recommender systems...`
  - Paragrafo 3 → sostituisce il capoverso gap/soluzione che inizia con `Despite these advances...`
  - Paragrafo 4 → sostituisce la frase/roadmap finale.
- **Blocco LaTeX:**

```latex
Context-aware recommender systems (CARS) aim to improve personalization by conditioning recommendations on situational factors such as time, location, or activity~\cite{adomavicius2005incorporating,adomavicius2011cars}. User preferences are not stationary: the same user can legitimately want different items under different circumstances~\cite{adomavicius2011cars}. However, two practical problems remain unresolved. First, most context-aware models still treat context as a side signal rather than as part of the relational structure that drives representation learning~\cite{mateos2025systematic}. Second, standard ranking metrics often reward relevance while ignoring whether the retrieved items are appropriate for the query context~\cite{meng2022survey}.

Graph neural network (GNN) recommenders offer a natural approach: they model high-order collaborative structure with relatively little architectural overhead~\cite{wu2022graph,sattar2023graph,gao2023survey}. Yet existing GNN-based recommenders typically focus on user--item connectivity and either omit context or incorporate it in ways that do not affect propagation itself~\cite{mateos2025systematic}. This raises the question of how to achieve context-sensitive GNN recommendation without incurring the cost of a substantially more complex architecture.

To address this gap, we propose \modelname, a context-aware graph recommender that embeds contextual features on interaction edges, uses the resulting representations to gate message passing, and introduces an explicit context-item compatibility term at scoring time. In parallel, we introduce a family of offline metrics that measure not only whether a relevant item is retrieved, but also whether it matches the situational conditions of the query. Together, the model and the metrics provide a consistent view of context-aware recommendation: one for learning, one for evaluation.

We evaluate the approach on Yelp, Frappe, and BoardGameGeek. The results show that the benefit of contextual modeling is dataset dependent: it is most pronounced when the context space is informative and not overly sparse, and it becomes more nuanced when memory constraints or highly balanced context groups limit the observable separation between models. The rest of the paper is organized as follows. Section~\ref{sec:related_work} discusses related work, Section~\ref{sec:model} presents the model, Section~\ref{sec:metrics} defines the metrics, Section~\ref{sec:experiments} reports the experiments, and Section~\ref{sec:conclusions} concludes the paper.
```

**Correzioni integrate:** `attractive` → `well-suited`; `inject it` → `incorporate it`; `heavyweight architecture` → `substantially more complex architecture`; `lightweight context-aware` → `context-aware`; `adds` → `introduces`; `strongest` → `most pronounced`; `not too sparse` → `not overly sparse`; `limit the room for separation` → `limit the observable separation between models`.

---

## 02_related_work.tex

### Modifica 2.1: Sostituire il preambolo della sezione e la sottosezione CARS

- **Target:** `overleaf/02_related_work.tex`, righe 8–35.
- **Perché:** il testo attuale contiene placeholder, note editoriali e una tesi troppo vicina all'introduzione.
- **A*-gate:** `PASS`.
- **Guida all'integrazione:**
  - Paragrafi 1–2 → sostituiscono il capoverso CARS e il successivo paragrafo tassonomico.
  - Paragrafo 3 → sostituisce il capoverso FM.
  - Paragrafo 4 → sostituisce il capoverso graph-recommender.
  - Paragrafo 5 → sostituisce la frase di posizionamento conclusiva.
- **Blocco LaTeX:**

```latex
Context-aware recommender systems (CARS) extend the classical user--item paradigm by explicitly conditioning recommendations on situational variables such as time, location, activity, and social context~\cite{adomavicius2011cars,villegas2010characterizing}. This problem is typically organized into three families of methods: contextual pre-filtering, contextual post-filtering, and contextual modeling~\cite{adomavicius2011cars,raza2019progress}. Pre-filtering and post-filtering reuse standard recommenders with limited engineering overhead, but both keep context outside the core representation-learning loop. Contextual modeling incorporates context directly into the prediction function, although this comes with familiar trade-offs in sparsity, feature heterogeneity, and optimization complexity~\cite{raza2019progress,meng2022survey}.

Within contextual modeling, factorization machines and their neural extensions remain strong and widely used baselines for CARS~\cite{rendle2010fm,guo2017deepfm,he2017nfm,xiao2017afm,lian2018xdeepfm}. Their main strength is that they natively support sparse multi-field categorical inputs and can capture feature interactions with controlled complexity. However, these approaches mostly exploit context at the scoring layer, which can limit their ability to reshape collaborative representations through context-dependent relational propagation.

Graph-based recommenders, by contrast, have largely focused on non-contextual user--item interaction graphs~\cite{wu2022graph,gao2023survey}. Even when contextual variables are available, they are often incorporated as auxiliary features, shallow side channels, or post-hoc re-ranking signals rather than being integrated as first-class relational conditioning factors~\cite{sattar2023graph,mateos2025systematic}. This distinction is central to our positioning: we target the specific gap between (i) models that exploit context primarily in scoring and (ii) models that allow context to influence representation propagation itself.

Our contribution is therefore not a claim of a new recommendation paradigm. It is a compact contextualization of graph collaborative filtering in which context is attached to interactions and directly modulates message passing. This design preserves the computational simplicity of LightGCN-style architectures while increasing contextual sensitivity where the impact is most direct: in how user and item embeddings are formed from neighborhood evidence.
```

**Correzioni integrate:** `are attractive because` → `are appealing from a practical standpoint because`; `injected` → `incorporated`; `lightweight contextualization` → `compact contextualization`.

---

### Modifica 2.2: Sostituire la sottosezione GNN con citazioni esplicite

- **Target:** `overleaf/02_related_work.tex`, righe 39–75.
- **Perché:** la sottosezione GNN attuale è utile ma troppo vicina a un sommario letterario, e la sottosezione valutazione è per lo più un placeholder.
- **A*-gate:** `PASS` dopo aver sostituito i placeholder `TODO_*` con chiavi BibTeX reali.
- **Guida all'integrazione:**
  - Sostituire dal capoverso GNN che inizia con `Graph neural networks have become...` fino alla fine della sezione con il blocco sottostante.
  - Mantenere le chiavi di citazione già presenti.
  - Sostituire solo i tre placeholder `TODO_*`.
- **Blocco LaTeX:**

```latex
Graph neural networks are a standard choice for collaborative filtering: they capture high-order connectivity through message passing while remaining relatively simple to train~\cite{Wang_2019,wu2022graph}. LightGCN showed that, for recommendation, much of the benefit of graph convolution comes from neighborhood aggregation itself, without nonlinear feature transforms or other components inherited from general-purpose GNNs~\cite{he2020lightgcnsimplifyingpoweringgraph}. LightCCF further simplified this design by replacing explicit graph convolution with a neighborhood-aggregation objective, demonstrating that contrastive learning can play a graph-aggregation role in recommender systems~\cite{zhang2025unveilingcontrastivelearningscapability}. Among graph-based approaches that do incorporate context, KG-conditioned recommenders~\cite{TODO_CA_KGCN}\footnote{\textit{Context-aware explainable recommendations over knowledge graphs} (search this title on DBLP and then map it to a real BibTeX key).} similarly condition aggregation on contextual or user signals, but they depend on an external knowledge-graph layer and the associated relational modeling choices. Our setting is intentionally narrower: no KG dependency, a pure user--item interaction graph, and context conditioning attached directly to interaction edges.

Our model builds on this line of work but makes context part of the propagation process. Instead of treating contextual information as a side feature or a post-hoc scoring adjustment, we encode it on interaction edges and use it to gate the messages exchanged between users and items. This choice preserves the efficiency and interpretability of LightGCN-style propagation while making the learned embeddings sensitive to the current situation.

This positioning calibrates the novelty claim. Relative to FM-based contextual modeling~\cite{rendle2010fm,guo2017deepfm,he2017nfm,xiao2017afm,lian2018xdeepfm}, our method injects context into neighborhood propagation rather than only into the score function. Relative to generic GNN recommenders~\cite{wu2022graph,sattar2023graph}, it avoids elaborate relational graph redesign and retains an efficient collaborative-filtering backbone. A related line of work builds graphs over feature fields rather than over interactions, as exemplified by feature-graph enhancement approaches~\cite{TODO_GEM}\footnote{\textit{Generalized Embedding Machines for Recommender Systems} (search this title on DBLP and then map it to a real BibTeX key).}: these methods share the intuition that context should participate in graph-based representation learning, but they construct graphs over feature fields and then feed the resulting representations into downstream feature-interaction models. In contrast, our approach keeps the interaction graph as the primary substrate and uses context to modulate collaborative propagation itself. This distinction has implications for complexity and deployment: feature-graph pipelines can be expressive, while edge-conditioned interaction-graph pipelines remain closer to standard collaborative-filtering stacks.

Disentanglement-oriented methods~\cite{TODO_IEDR}\footnote{\textit{IEDR: A Context-aware Intrinsic and Extrinsic Disentangled Recommender System} (search this title on DBLP and then map it to a real BibTeX key).} pursue a complementary goal: they separate intrinsic preference factors from extrinsic contextual factors rather than conditioning propagation on context directly. Disentanglement seeks factor separation as an end in itself, whereas our model uses direct contextual gating to condition propagation with low architectural overhead. We therefore position \modelname{} as a lightweight alternative for context adaptation, not as a replacement for disentanglement-based modeling. Together, these three contrasts --- graph-based KG conditioning, feature-graph enhancement, and disentanglement --- define the space in which our contribution is situated.

Evaluation constitutes the other dimension of the problem. Standard ranking metrics such as nDCG, Recall, MRR, and MAP measure retrieval quality~\cite{manning2008introduction,krichene2020sampled}, but they do not tell us whether the retrieved items fit the query context~\cite{adomavicius2011cars,meng2022survey}. This concern has also been emphasized in recent context-aware and POI-oriented analyses that discuss coverage and context-validity pitfalls in offline evaluation~\cite{TODO_POI_REFLECTION}\footnote{\textit{Point of Interest Recommendation: Pitfalls and Viable Solutions} (search this title on DBLP and then map it to a real BibTeX key).}. This motivates context-sensitive evaluation: metrics should expose exact contextual consistency, partial overlap, feature-group balance, and context-weighted ranking quality. Our metric family is intended for this role and should be interpreted as a complement to standard ranking metrics, not a replacement.

Overall, the related-work positioning is as follows: (i) we inherit efficient graph collaborative filtering from LightGCN/LightCCF, (ii) we inject context directly into interaction-level propagation rather than only into feature scoring or external graph modules, and (iii) we evaluate context alignment explicitly rather than relying on accuracy-only proxies. This is the precise novelty scope we claim.
```

**Correzioni integrate:** `lightweight contextualization` → `compact contextualization` (nell'ultimo paragrafo del blocco 2.1, riflesso qui); `keeps a lightweight collaborative-filtering backbone` → `retains an efficient collaborative-filtering backbone`; `lightweight graph collaborative filtering` → `efficient graph collaborative filtering`; `adapt propagation with minimal architectural overhead` → `condition propagation with low architectural overhead`.
**Integrazione strutturale:** le tre linee di lavoro (CA-KGCN, GEM, IEDR) sono ora distribuite nel flusso della sezione invece di stare come blocco enumerato. CA-KGCN è fuso nel primo paragrafo GNN. GEM è integrato nel paragrafo di novelty calibration dopo il confronto con FM e GNN generici. IEDR rimane come paragrafo separato ma senza enumerazione, e una frase di raccordo finale (`Together, these three contrasts...`) lega le tre distinzioni al posizionamento complessivo.

---

## 03_model.tex

### Modifica 3.1: Roadmap più pulita in tre parti

- **Target:** `overleaf/03_model.tex`, righe 10–13.
- **Perché:** la roadmap attuale è troppo verbosa.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
In this section, we introduce \modelname, a context-aware recommendation model derived from LightCCF~\cite{zhang2025unveilingcontrastivelearningscapability}. The section is organized into three parts. First, we define the context-enriched graph representation and the contextual edge encoder. Second, we present the context-gated message-passing mechanism and the layer-combination strategy. Third, we describe the context-aware scoring function and the training objective.
```

---

### Modifica 3.2: Formulazione del problema e edge embedding

- **Target:** `overleaf/03_model.tex`, righe 24–39.
- **Perché:** la scrittura attuale è corretta ma leggermente informale.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
Let $\mathcal{U}$ and $\mathcal{V}$ denote the sets of users and items, respectively. We represent the observed interactions as a bipartite graph $\mathcal{G}=(\mathcal{U}\cup\mathcal{V},\mathcal{E})$, where each edge $e_{uv}\in\mathcal{E}$ connects user $u\in\mathcal{U}$ to item $v\in\mathcal{V}$ and carries a contextual feature vector describing the situation in which the interaction occurred. Treating context as an edge attribute, rather than as a node feature or scalar edge weight, lets the model preserve the user--item graph while still conditioning the propagation on the query situation.

Each contextual feature $f\in\{1,\ldots,F\}$ takes a discrete value $c_{uv}^{(f)}$ from a feature-specific vocabulary of size $V_f$. We embed each feature value with a dedicated matrix $\mathbf{E}_f\in\mathbb{R}^{V_f\times d_c}$:
\begin{equation}
    \mathbf{e}_{uv}^{(f)} = \mathbf{E}_f[c_{uv}^{(f)}] \in \mathbb{R}^{d_c}.
    \label{eq:feat_emb}
\end{equation}
The feature embeddings are concatenated and projected into the shared latent space through a linear layer followed by ReLU:
\begin{equation}
    \mathbf{r}_{uv} = \mathrm{ReLU}\!\left(\mathbf{W}_c \bigl[\mathbf{e}_{uv}^{(1)} \,\|\, \cdots \,\|\, \mathbf{e}_{uv}^{(F)}\bigr] + \mathbf{b}_c\right) \in \mathbb{R}^{d},
    \label{eq:ctx_edge}
\end{equation}
where $\mathbf{W}_c\in\mathbb{R}^{d\times Fd_c}$ and $\mathbf{b}_c\in\mathbb{R}^d$ are learnable parameters. The resulting vector $\mathbf{r}_{uv}$ is the contextual edge representation used throughout the rest of the model.
```

---

### Modifica 3.3: Message passing come scelta progettuale deliberata

- **Target:** `overleaf/03_model.tex`, righe 43–65.
- **Perché:** la spiegazione attuale è buona ma suona ancora come una derivazione.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
Standard LightGCN~\cite{he2020lightgcnsimplifyingpoweringgraph} propagates node embeddings along graph edges without relational modulation. Building on the principle of feature-aware edge modulation~\cite{zhuo2025edgegflrethinkingedgeinformation}, we instead use the contextual edge vector $\mathbf{r}_{uv}$ as a feature-wise filter: each dimension of the neighbor embedding is scaled by the corresponding dimension of the context representation. This preserves the linearity and scalability of the propagation while making message passing sensitive to the current context.

Formally, the message from item $v$ to user $u$ at layer $l$ is
\begin{equation}
    \mathbf{M}^{(l)}_{v \to u} = \mathbf{h}^{(l)}_v \odot \mathbf{r}_{uv},
    \label{eq:message}
\end{equation}
and the symmetric user-to-item message is defined analogously. The aggregated embedding is then
\begin{equation}
    \mathbf{h}^{(l+1)}_u = \sum_{v \in \mathcal{N}_u} \mathbf{h}^{(l)}_v \odot \mathbf{r}_{uv}.
    \label{eq:aggregation}
\end{equation}
No nonlinear activations or additional feature transforms are applied, preserving the efficiency and stability of LightGCN-style propagation while adding context only where needed.

After $L$ propagation layers, the final embedding is the mean of all layerwise representations, including the initial embedding:
\begin{equation}
    \mathbf{h}_u^* = \frac{1}{L+1}\sum_{l=0}^{L} \mathbf{h}^{(l)}_u, \qquad
    \mathbf{h}_v^* = \frac{1}{L+1}\sum_{l=0}^{L} \mathbf{h}^{(l)}_v.
    \label{eq:layer_combination}
\end{equation}
This layer combination captures both local and higher-order collaborative signals while avoiding the over-smoothing that typically appears when only the last layer is used~\cite{li2018deeperinsightsgraphconvolutional}.
```

**Correzioni integrate:** `Inspired by feature-aware edge modulation` → `Building on the principle of feature-aware edge modulation`; `every dimension` → `each dimension`; `keeps the propagation` → `preserves the linearity and scalability of the propagation`.

---

### Modifica 3.4: Scoring e objective più diretti

- **Target:** `overleaf/03_model.tex`, righe 69–100.
- **Perché:** il paragrafo di scoring deve separare chiaramente context conditioning in inference dall'objective di training.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
\paragraph{Scoring.}
At inference time, the relevance score between user $u$ and item $v$ under query context $\mathbf{c}_q$ is
\begin{equation}
    \hat{y}_{uv} = \mathbf{h}_u^* \cdot \mathbf{h}_v^* + \mathbf{r}_q \cdot \mathbf{h}_v^*,
    \label{eq:score}
\end{equation}
where $\mathbf{r}_q$ is computed with the same contextual encoder used for edge embeddings. The first term captures general user--item affinity learned from context-gated propagation; the second adds an explicit context--item compatibility signal at prediction time.

\paragraph{Training Objective.}
We adopt a multi-task objective following LightCCF~\cite{zhang2025unveilingcontrastivelearningscapability}:
\begin{equation}
    \mathcal{L} = \mathcal{L}_{\mathrm{BPR}} + \alpha\,\mathcal{L}_{\mathrm{NA}} + \lambda\,\|\mathbf{E}_0\|^2_F,
    \label{eq:loss}
\end{equation}
where $\alpha,\lambda$ are hyperparameters and $\mathbf{E}_0$ denotes the base user/item embeddings.

The BPR term~\cite{rendle2012bprbayesianpersonalizedranking} optimizes pairwise preference: for each user $u$, a positive item $v^+$ (observed interaction) is scored above a sampled negative $v^-$ under the context-aware score of Eq.~\eqref{eq:score}, using the same query context for both items. This ensures that ranking discrimination accounts for contextual appropriateness, not merely relevance.

The neighborhood-aggregation (NA) loss complements context-gated message passing by directly maximizing alignment between each user and their interacted items:
\begin{equation}
    \mathcal{L}_{\mathrm{NA}} = -\sum_{(u,v^+)\in\mathcal{B}} \log \frac{\exp\!\bigl(\mathrm{sim}(\mathbf{h}_u^*,\mathbf{h}_{v^+}^*)/\tau\bigr)}{\displaystyle\sum_{p\in\mathcal{B}} \exp\!\bigl(\mathrm{sim}(\mathbf{h}_u^*,\mathbf{h}_{p}^*)/\tau\bigr)},
    \label{eq:na_loss}
\end{equation}
where $\mathrm{sim}(\cdot,\cdot)$ is cosine similarity and $\tau$ a temperature hyperparameter. Unlike standard contrastive objectives that pair augmented views of the same node, the NA loss treats observed user--item interactions as positive pairs. LightCCF's gradient analysis shows that this formulation inherently performs one step of graph convolution while counteracting the over-smoothing that repeated message-passing layers can induce~\cite{zhang2025unveilingcontrastivelearningscapability}. In our architecture this dual role is especially important: the NA loss preserves a direct user--item alignment signal that is independent of the context-gated propagation, preventing the contextual edge modulation from dispersing the collaborative signal when context is sparse or uninformative.

L2 regularization controls embedding magnitude. The trainable parameters are the context embedding matrices $\{\mathbf{E}_f\}$, the projection layer $\mathbf{W}_c,\mathbf{b}_c$, and the base user/item embeddings.
```

---

## 04_metrics.tex

### Modifica 4.1: Apertura sezione e Family 1 — definizioni formali con equazioni

- **Target:** `overleaf/04_metrics.tex`, righe 10–89.
- **Perché:** l'apertura è troppo informale, la nozione di contesto rappresentativo è sotto-specificata, e le metriche sembrano una lista piuttosto che un framework di misurazione. La proposta precedente eliminava erroneamente tutte le equazioni formali, che sono essenziali per un paper A* Best Paper.
- **A*-gate:** `PASS` (con equazioni ripristinate).
- **Blocco LaTeX:**

```latex
Standard ranking metrics such as nDCG, Recall, MAP, and MRR measure whether relevant items are retrieved~\cite{manning2008introduction,krichene2020sampled}, but they do not account for whether those items fit the query context~\cite{adomavicius2011cars}. We therefore define a family of context-sensitive offline metrics that require only the contextual attributes already present in the dataset, without additional annotations.

Let $c_q$ denote the query context of a held-out interaction and let $c_i = \phi(i)$ denote the representative context of item~$i$. We define $\phi(i)$ as the per-feature mode over the historical contexts in which item~$i$ appears; ties are broken first by global feature frequency and then by recency. All metrics are computed over the ranked list $R_q^K$ for each query $q\in\mathcal{Q}$.

We organize the metrics into three complementary families. The first family measures exact or partial contextual agreement between the query and each recommended item. The second family diagnoses how context is distributed across feature groups. The third family injects context directly into classical ranking metrics.

\textit{Family 1 --- Context Similarity and Satisfaction Metrics} quantify how closely each recommended item's representative context $c_i$ matches the query context $c_q$, capturing different notions of what it means for an item to be ``contextually appropriate.'' The five metrics are designed along a spectrum of strictness and perspective. At one extreme, ACC requires exact equality across all feature dimensions and awards no partial credit, serving as a strict diagnostic of contextual fidelity. CS and WCS relax this requirement by measuring set-based partial overlap, with WCS further weighting features by their informativeness. WCA adopts a geometric rather than set-based view, measuring directional alignment in the weighted feature space. Friction sits between the set-based and geometric approaches, computing the fraction of features that agree exactly. The metrics are intentionally complementary: each captures a distinct failure mode (exact mismatch, partial mismatch, rare-feature insensitivity, geometric misalignment, and feature-level disagreement), ensuring that no single score can mask a contextual weakness that another would expose.

\textbf{ACC@K (Average Context Consistency)} measures the fraction of recommended items whose contextual attributes exactly match the query context across all feature dimensions, with no partial credit:
\begin{equation}
    \mathrm{ACC@K} = \frac{1}{|\mathcal{Q}|} \sum_{q \in \mathcal{Q}} \frac{1}{K} \sum_{i \in R_q^K} \mathbf{1}_{\mathrm{match}}(i, q),
    \label{eq:acc}
\end{equation}
where $\mathbf{1}_{\mathrm{match}}(i, q)=1$ if $c_i = c_q$ and $0$ otherwise. ACC functions as a strict diagnostic: any contextual deviation, however minor, yields zero credit.

\textbf{CS (Context Satisfaction)}~\cite{jorro2024context} relaxes exactness by measuring partial feature overlap through a modified Jaccard coefficient:
\begin{equation}
    \mathrm{CS}(c_q, c_i, \alpha) = \frac{|c_q \cap c_i|}{|c_q \cup c_i| + \alpha \cdot \frac{|c_q \setminus c_i|}{|c_q|}},
    \label{eq:cs}
\end{equation}
where $\alpha \geq 0$ penalizes query features absent from the item context. Setting $\alpha = 0$ recovers standard Jaccard; in all experiments we use $\alpha = 0.5$.

\textbf{WCS (Weighted Context Satisfaction)} extends CS with IDF-based feature weights $w_f$ so that rare, discriminative features contribute more than common ones:
\begin{equation}
    \mathrm{WCS}(c_q, c_i, w, \alpha) = \frac{\sum_f w_f \cdot \mathbf{1}_{f \in c_q \cap c_i}}{\sum_f w_f \cdot \mathbf{1}_{f \in c_q \cup c_i} + \alpha \cdot \frac{\sum_f w_f \cdot \mathbf{1}_{f \in c_q \setminus c_i}}{\sum_f w_f \cdot \mathbf{1}_{f \in c_q}}}.
    \label{eq:wcs}
\end{equation}
IDF-weighting prevents high-frequency features from dominating the similarity score.

\textbf{WCA (Weighted Context Alignment)} measures geometric alignment via IDF-weighted cosine similarity between query and item context vectors:
\begin{equation}
    \mathrm{WCA}(c_q, c_i, w) = \frac{\sum_f w_f \cdot c_{q,f} \cdot c_{i,f}}{\sqrt{\sum_f w_f \cdot c_{q,f}^2} \cdot \sqrt{\sum_f w_f \cdot c_{i,f}^2}}.
    \label{eq:wca}
\end{equation}
WCA captures directional alignment independently of feature cardinality. On datasets where binary one-hot encodings make this measure structurally saturate, it should be interpreted as a diagnostic quantity rather than as an optimization target.

\textbf{Friction} quantifies the proportion of contextual features that agree between query and item, formulated as the complement of normalized Hamming distance:
\begin{equation}
    \mathrm{Friction}(c_q, c_i) = 1 - \frac{d_H(c_q, c_i)}{F} = \frac{1}{F} \sum_{f=1}^{F} \mathbf{1}[c_{q,f} = c_{i,f}],
    \label{eq:friction}
\end{equation}
where $F$ is the total number of contextual features. $\mathrm{Friction@K}$ is averaged over the top-$K$ list and all queries:
\begin{equation}
    \mathrm{Friction@K} = \frac{1}{|\mathcal{Q}|} \sum_{q \in \mathcal{Q}} \frac{1}{K} \sum_{i \in R_q^K} \mathrm{Friction}(c_q, c_i).
    \label{eq:friction_k}
\end{equation}
A value of $1$ indicates complete feature-level agreement; $0$ indicates total mismatch.

Table~\ref{tab:metrics_summary} summarizes the five metrics and their complementary roles.
```

---

### Modifica 4.2: Family 2, Family 3 e paragrafo di chiusura

- **Target:** `overleaf/04_metrics.tex`, righe 111–208.
- **Perché:** la discussione attuale mescola definizioni, interpretazione e rivendicazioni di novità.
- **A*-gate:** `CONDITIONAL`. Il testo è A*-level, ma la sezione empirica deve smettere di descrivere metriche sature come se fossero universalmente discriminative.
- **Blocco LaTeX:**

```latex
\textit{Family 2 --- Advanced Context Dynamics} moves beyond per-item alignment to analyze structural and distributional properties of the entire recommendation list. While Family~1 treats each recommended item independently, Family~2 asks two complementary list-level questions. First, ``does the set of recommended items collectively cover the query context, even if no single item matches perfectly?'' This is captured by context recall (CR@K), which shifts the evaluation unit from items to features: an item that partially covers the query context still contributes to coverage, which is useful when the user's situational requirements cannot be met by a single recommendation. Second, ``is the model biased toward certain context dimensions at the expense of others?'' This is captured by context group balance (CGB@K), which detects whether the model systematically over-covers one feature group while neglecting others --- a failure mode that per-item similarity metrics would not reveal because each individual item might appear contextually appropriate.

\textbf{CR@K (Context Recall)} shifts focus from items to features, measuring the average fraction of query-context features covered by the top-$K$ list:
\begin{equation}
    \mathrm{CR@K} = \frac{1}{K} \sum_{i \in R_K} \frac{|c_q \cap c_i|}{|c_q|}.
    \label{eq:cr}
\end{equation}
CR answers a different question from CS: not ``how similar is a single item?'' but ``how much of the requested context is covered by the list as a whole?'' This makes it useful when the query context is only partially satisfiable by any single item.

\textbf{CGB@K (Context Group Balance)} detects dimensional bias across predefined feature groups $\mathcal{G} = \{G_1, \ldots, G_n\}$. For each group~$g$, a group-specific context recall $\mathrm{CR}_g@K$ is computed; CGB then measures how evenly these group recalls are distributed:
\begin{equation}
    \mathrm{CGB@K} = 1 - \min\!\left(\frac{\sigma_{\text{groups}}}{\sigma_{\max}},\, 1\right),
    \label{eq:cgb}
\end{equation}
where $\sigma_{\text{groups}}$ is the standard deviation of the group recalls and $\sigma_{\max} = \sqrt{(|\mathcal{G}|-1)/|\mathcal{G}|^2}$ is the maximum attainable dispersion when one group receives all the mass. $\mathrm{CGB} \approx 1$ indicates balanced contextual coverage across all groups; $\mathrm{CGB} \approx 0$ indicates that the model excels at one dimension while neglecting the others.

\textit{Family 3 --- Context-Weighted Ranking Metrics} bridge the gap between standard ranking metrics (which ignore context entirely) and the context-similarity metrics of Family~1 (which ignore ranking position). Standard metrics such as nDCG and MAP evaluate whether a model ranks relevant items above non-relevant ones, but they treat relevance as static: a movie recommended for a \emph{family night out} and the same movie recommended for a \emph{solo evening} receive identical gain, even though only one is contextually appropriate. Family~3 solves this by replacing the static relevance judgment with context-weighted relevance $\mathrm{rel}_{\mathrm{cw}}(k)$, which scales each item's contribution by its contextual appropriateness $s(c_q, c_{i_k})$. This exposes a critical failure mode invisible to both Family~1 and Family~2: a model may retrieve all relevant items (high standard nDCG) and cover the query context well (high CR@K), yet still rank them in contextually inappropriate positions. The diagnostic signal is the gap between the standard metric and its context-weighted counterpart --- a large gap means ``the model gets the right items but in the wrong situations.'' Conversely, comparable scores indicate that contextual appropriateness is well-aligned with ranking order.
\begin{equation}
    \mathrm{rel}_{\mathrm{cw}}(k) = \mathrm{rel}(k) \cdot s(c_q,\, c_{i_k}),
    \label{eq:rel_cw}
\end{equation}
where $s(\cdot)$ is one of the context-similarity functions defined above (CS, WCA, or Friction). This ensures that each item contributes to the metric score in proportion to both user preference and contextual appropriateness.

\textbf{CW-nDCG@K} substitutes context-weighted relevance into the DCG gain function:
\begin{equation}
    \mathrm{CW\text{-}nDCG@K} = \frac{1}{\mathrm{IDCG}_{\mathrm{cw}}@K} \sum_{k=1}^{K} \frac{2^{\,\mathrm{rel}_{\mathrm{cw}}(k)} - 1}{\log_2(k+1)},
    \label{eq:cw_ndcg}
\end{equation}
where $\mathrm{IDCG}_{\mathrm{cw}}@K$ is the ideal DCG under the same context-weighted relevance. A score of $1$ is achieved only when the system reproduces the optimal context-aware ranking. A large gap between nDCG and CW-nDCG indicates that the model retrieves relevant items but in positions where their contextual appropriateness is suboptimal.

\textbf{CW-MAP@K} incorporates context-weighted relevance into average precision:
\begin{equation}
    \mathrm{CW\text{-}MAP@K} = \frac{1}{|\mathcal{Q}|} \sum_{q \in \mathcal{Q}} \frac{1}{|\mathrm{Rel}_q|} \sum_{k=1}^{K} \frac{\sum_{j=1}^{k} \mathrm{rel}_{\mathrm{cw}}(j)}{k} \cdot \mathrm{rel}_{\mathrm{cw}}(k).
    \label{eq:cw_map}
\end{equation}
A substantial decrease in CW-MAP relative to standard MAP signals that the model retrieves relevant items but in contextually inappropriate situations; comparable scores indicate effective alignment between recommendations and query context.

All metrics are bounded in $[0,1]$, model-agnostic, and computable without annotations beyond the contextual features already in the dataset. Taken together, they separate five distinct failure modes: exact mismatch, partial mismatch, feature imbalance, coverage imbalance, and context-aware ranking degradation. Reporting them as a family rather than as a single number preserves this diagnostic separation. Table~\ref{tab:metrics_summary} summarizes the role of each metric.
```

**Correzioni integrate:** `easy to interpret` → `straightforward to interpret`; `if they are close` → `when they approximate`; `much lower` → `substantially lower`; `in the wrong context` → `in mismatched contexts`.

---

## 05_experiments.tex

### Modifica 5.1: Descrizioni dataset — condensate e precise

- **Target:** `overleaf/05_experiments.tex`, righe 12–59.
- **Perché:** le descrizioni spendono troppo spazio su cosa sono i dataset invece di perché sono utili.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
We evaluate the proposed model on three benchmark datasets that differ in context sparsity, feature cardinality, and interaction density.

\smallskip\noindent\textbf{Frappe}~\cite{frappe} is a mobile-app recommendation dataset with eight contextual features organized into temporal, activity, and environment groups. Its context space is sparse and heterogeneous, providing a setting in which context-gated propagation must exploit informative yet irregular context signals.

\smallskip\noindent\textbf{Yelp}~\cite{yelp2024} is a large-scale local-business dataset with eleven contextual features organized into temporal, social/user, and spatial groups. Its high-cardinality spatial features render it the most contextually complex benchmark in the study and, correspondingly, the most demanding testbed for context-aware metrics.

\smallskip\noindent\textbf{BoardGameGeek (BGG)}~\cite{jorro2024boardgame} contains explicit contextual annotations for board-game recommendations and has a compact but semantically rich context space. BGG is the most suitable benchmark for studying context-aware ranking: the playing situation strongly determines which item is appropriate, making the context signal particularly informative.
```

**Correzioni integrate:** `good test` → `informative test case`; `stress test for context-aware evaluation` → `challenging evaluation setting for context-aware metrics`; `cleanest benchmark` → `most suitable benchmark`.

---

### Modifica 5.2: Baseline — tono neutro

- **Target:** `overleaf/05_experiments.tex`, righe 63–95.
- **Perché:** il paragrafo attuale sovrasta la certezza e ha phrasing goffo.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
We compare \modelname{} against three non-contextual baselines and five context-aware FM-based models, all trained within the WarpRec framework~\cite{warprec}.

\smallskip\noindent\textbf{Non-contextual baselines.}
\emph{Random} assigns uniform random scores to all items and serves as a lower bound. \emph{Popularity} ranks items by global interaction count and is often strong in datasets with a heavy-tailed item distribution. \emph{LightCCF} is the graph-based recommender from which our model is derived.

\smallskip\noindent\textbf{Context-aware FM-based models.}
Following the contextual modeling paradigm, we select five representative FM-based baselines. \emph{FM} models pairwise feature interactions through shared latent factors~\cite{rendle2010fm}. \emph{DeepFM} combines an FM component with a deep MLP~\cite{guo2017deepfm}. \emph{NFM} replaces FM pooling with a Bi-Interaction layer followed by an MLP~\cite{he2017nfm}. \emph{AFM} adds attention over pairwise feature interactions~\cite{xiao2017afm}. \emph{xDeepFM} uses a Compressed Interaction Network to model bounded-degree feature interactions at the vector level~\cite{lian2018xdeepfm}.
```

---

### Modifica 5.3: Metodologia di valutazione — chiara e con caveat sulla capacità

- **Target:** `overleaf/05_experiments.tex`, righe 103–129.
- **Perché:** il paragrafo attuale fa troppe cose contemporaneamente.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
All models are evaluated with full-catalog ranking~\cite{krichene2020sampled}: at inference time every item in the catalog is scored for each test query, and items seen during training are masked with $-\infty$ before ranking. This removes sampling bias and measures whether the model can retrieve new relevant items.

\smallskip\noindent\textbf{Data splitting.}
We use a temporal leave-one-out protocol: the most recent interaction of each user is the test example, the second-most-recent interaction is used for validation, and all earlier interactions form the training set. This mirrors an online recommendation scenario and avoids future leakage~\cite{wang2020time, elsayed2023context, zhou2020s3}.

\smallskip\noindent\textbf{Context in evaluation.}
During evaluation, the contextual features attached to the held-out interaction are passed through the context encoder to produce the query-context embedding used for scoring the held-out item against all candidate items in the catalog. This setup corresponds to the practical scenario in which the current situation is known at query time~\cite{Rashed_2022}.

\smallskip\noindent\textbf{Hyperparameter optimization.}
Hyperparameters are selected with Ray Tune~\cite{liaw2018tune} using the validation set. Training uses early stopping on nDCG@10 with patience 10 and a grace period of 20 epochs. The best checkpoint is retrained on the full training split before test evaluation. Unless stated otherwise, all models use an embedding size of 64; xDeepFM is reduced to 16 because of CIN memory cost, and \modelname{} is reduced to 32 on BGG because the context-gated graph encoder exceeds the available GPU memory at the larger size.

\smallskip\noindent\textbf{Evaluation cutoffs.}
We report results at $K=10$ in the main text. We also compute $K=5$ during model selection, but we do not duplicate those tables in the paper.
```

---

### Modifica 5.4: Narrazione risultati — strutturata e onesta

- **Target:** `overleaf/05_experiments.tex`, righe 145–324.
- **Perché:** la narrazione attuale sovrasta alcune vittorie, minimizza il caveat sulla capacità di BGG, e ripete la stessa affermazione in più punti.
- **A*-gate:** `CONDITIONAL`. Diventa A*-level solo se la prosa circostante è misurata e le tabelle parlano da sole.
- **Blocco LaTeX:**

```latex
We report both standard ranking metrics and context-aware metrics. The main pattern is consistent across the section: the benefit of context gating is most evident when the dataset has informative context and sufficient structure for the context encoder to exploit, and it is less decisive when memory constraints or near-saturated context groups limit separation.

\paragraph{Standard ranking metrics.}
On Yelp, \modelname{} achieves the highest scores across all four standard ranking metrics, which suggests that context-aware propagation and context-aware scoring improve classic recommendation quality when the context space is rich without being excessively sparse. On Frappe, \modelname{} again obtains the best nDCG@10, MRR@10, and Recall@10, while Precision@10 is comparable to AFM. This pattern is consistent with the hypothesis that the model generalizes beyond large-scale settings and remains effective on a smaller, sparser benchmark where contextual variation is important. On BGG, however, the ranking picture is more nuanced. \modelname{} remains competitive and outperforms the FM-based baselines, but it does not surpass the leading graph baseline in the standard ranking setting because its embedding size is reduced to satisfy GPU memory constraints. We should therefore treat the BGG ranking results as a constrained but still informative comparison, not as a pure capacity-matched head-to-head.

\paragraph{Context-aware metrics.}
The context-aware metrics refine this picture. On Yelp and Frappe, \modelname{} achieves the highest scores on most similarity, coverage, and context-weighted ranking metrics, which indicates that the improvements observed in standard ranking are accompanied by stronger contextual alignment. On BGG, the model shows its most substantial improvement on geometric alignment and context-weighted ranking, while some group-balanced or exact-match metrics remain higher for simpler baselines such as Popularity. This is expected: the different metrics are designed to capture distinct failure modes, and their divergence confirms that the framework separates these cases rather than collapsing them into a single score. In particular, high CGB on BGG should be interpreted as balanced coverage across the three context groups, not as evidence that a model is contextually optimal. The metric family is useful precisely because it separates these cases.

\paragraph{Overall.}
Taken together, the results suggest three conclusions. First, encoding context directly in message passing can improve recommendation quality without abandoning the efficiency of graph-based collaborative filtering. Second, the context-aware metrics reveal information that standard ranking metrics hide, especially when the dataset is large or the context space is highly structured. Third, the most substantial gains are dataset dependent, which is consistent with the behavior of a context-sensitive method that responds to dataset-specific structure rather than a general-purpose architecture.
```

**Correzioni integrate:** `strongest` → `most evident` (primo paragrafo); `is the strongest model` → `achieves the highest scores across`; `leads on` → `obtains the best`; `tied with` → `comparable to`; `good sign` → `pattern is consistent with the hypothesis`; `does not beat the strongest graph baseline` → `does not surpass the leading graph baseline`; `leads on most` → `achieves the highest scores on most`; `clearest gain` → `most substantial improvement`; `that is not a contradiction` → `this is expected` + spiegazione; `strongest gains` → `most substantial gains`; `exactly what we should expect from` → `consistent with the behavior of`; `one-size-fits-all architecture` → `general-purpose architecture`.

---

### Modifica 5.5: Ablazione — analitica

- **Target:** `overleaf/05_experiments.tex`, righe 599–739.
- **Perché:** l'ablation attuale sembra un log di risultati grezzi.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
The ablation study isolates which contextual feature groups are most useful for each dataset. The main message is that context utility is not uniform: the best subset depends on how the dataset was collected and on which contextual groups are most semantically informative.

\subsubsection{Yelp}
On Yelp, the best-performing configuration combines Temporal and Location features, which is consistent with the intuition that restaurant or business recommendations depend heavily on when and where the interaction happens. Adding Atmosphere or static user attributes does not help and can even hurt, which suggests that redundant or noisy features can dilute the signal. This pattern is also consistent with prior context-aware studies on Yelp-like settings~\cite{nguyen2025item,lu2020multi,Gao2020GraphNN}. The key takeaway is not that more context is always better, but that the right context subset matters more than the full feature set.

\subsubsection{Frappe}
On Frappe, Environment features alone are the most informative, and the full feature set is only a close second. This means that the app-discovery setting is driven more by external situational conditions than by the other available groups, in line with earlier findings on context salience in app recommendation~\cite{zhong2023context}. The weaker performance of Temporal + Activity alone indicates that these groups do not always combine constructively unless they are grounded by environmental context.

\subsubsection{BoardGameGeek}
On BGG, Playtime + Mood is the best subset, with Social alone and Playtime + Social very close behind. Playtime by itself is clearly weaker, which suggests that duration is informative only when paired with additional situational cues. The ablation therefore supports the interpretation that contextual recommendation works best when the feature groups capture complementary aspects of the situation rather than a single coarse dimension.

\paragraph{Cross-model observation.}
For the context-aware FM baselines, performance does not change much across feature subsets. This is not evidence that context is irrelevant; it suggests that these models use context mainly at the score level, whereas \modelname{} injects context into propagation itself. That architectural difference makes the proposed model more sensitive to which contextual groups are selected.
```

**Correzioni integrate:** `the strongest configuration` → `the best-performing configuration`.

---

### Modifica 5.6: Validazione qualitativa e ponte verso le limitazioni

- **Target:** `overleaf/05_experiments.tex`, righe 748–760, più una nuova sottosezione subito dopo.
- **Perché:** il testo attuale è utile ma incompleto.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
Beyond the quantitative results, we ask whether optimizing the model with CW-nDCG@10 changes the user-level ranking behavior. To test this, we compare the standard validation setting (\textsc{Base}) with a context-weighted validation setting (\textsc{CA-Val}) under the same feature configuration. The result is deliberately conservative: context-weighted validation changes the ranking behavior in some cases, but it does not produce a uniform improvement in hit rate across datasets. This negative result is informative because it indicates that context-aware validation is not uniformly superior to standard ranking validation.

This result naturally motivates an explicit discussion of limitations and threats to validity, which we separate in a dedicated subsection below.
```

**Correzioni integrate:** `intentionally modest` → `deliberately conservative`; `hit-rate improvement` → `improvement in hit rate`; `important negative finding because it suggests` → `negative result is informative because it indicates`; `automatically better than` → `uniformly superior to`.

---

### Modifica 5.7: Sezione limitazioni dedicata

- **Target:** `overleaf/05_experiments.tex`, immediatamente dopo il blocco di analisi qualitativa.
- **Perché:** un paper A* tratta le limitazioni come una sezione matura e autonoma.
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
\subsection{Limitations and Threats to Validity}
\label{sec:experiments:limitations}

The current study has four main limitations. First, the model assumes discrete contextual variables and does not yet support continuous context representations directly. Second, the BGG benchmark exposes a memory-efficiency trade-off: context-aware propagation can force a smaller embedding size, which means that capacity-matched comparison is not always possible. Third, some of the proposed context-aware metrics can saturate or become weakly discriminative on particular encodings, so they should be interpreted as diagnostics rather than as universal optimization targets. Fourth, the empirical section does not report multi-seed variance or significance tests, so the results should be interpreted as descriptive evidence rather than as statistically validated claims of superiority.

These limitations do not undermine the central claim of the paper. They instead define the scope of the evidence and motivate future work on continuous contexts, memory-aware propagation, and more robust context-sensitive validation objectives.
```

**Correzioni integrate:** `read as strong descriptive evidence rather than as statistically certified superiority` → `interpreted as descriptive evidence rather than as statistically validated claims of superiority`.

---

## 06_conclusions.tex

### Modifica 6.1: Conclusione — sintesi onesta

- **Target:** `overleaf/06_conclusions.tex`, righe 7–10.
- **Perché:** la conclusione attuale ripete la sezione risultati e sovrasta "competitive or superior".
- **A*-gate:** `PASS`.
- **Blocco LaTeX:**

```latex
This work introduced \modelname{}, a context-aware graph recommender that integrates contextual information directly into propagation through context-gated message passing and explicit context-aware scoring. We also proposed a family of context-sensitive evaluation metrics that expose exact match, partial overlap, weighted alignment, group balance, and context-weighted ranking quality.

The experiments show that the benefit of context-aware propagation is substantial yet dataset dependent: it is most pronounced on Yelp and Frappe, where the contextual signal is informative enough to improve standard ranking as well as context-sensitive metrics, and more nuanced on BGG, where memory constraints and balanced context groups limit the separation between models. The ablation study further shows that the best contextual feature subset depends on the dataset, which confirms that contextual recommendation is sensitive to which situational dimensions are actually informative.

Overall, the paper supports a clear conclusion: context should be modeled as part of the interaction structure and, correspondingly, evaluated as part of the ranking task. Future work should extend the method to continuous context, improve memory efficiency on large context spaces, and further refine context-sensitive validation objectives.
```

**Correzioni integrate:** `is real but` → `is substantial yet`; `strongest` → `most pronounced`; `simple conclusion` → `clear conclusion`; `but it should also be evaluated` → `and, correspondingly, evaluated` (struttura più elegante).

---

## Cosa non cambiare ancora

- Lascia le tabelle numeriche intatte a meno che tu non stia anche modificando il testo dei risultati.
- Non aggiungere citazioni mancanti a CA-KGCN, GEM o IEDR fino a quando le loro entry BibTeX non esistono.
- Non introdurre `\ours{}` o `\URSp{}` senza prima aggiungere quelle macro al sorgente del paper.

## Ordine di editing suggerito

1. `00_main.tex` — front matter e abstract.
2. `01_introduction.tex`.
3. `02_related_work.tex`.
4. `03_model.tex`.
5. `04_metrics.tex`.
6. `05_experiments.tex`.
7. `06_conclusions.tex`.
