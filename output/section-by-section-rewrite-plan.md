# Section-by-Section Rewrite Plan

This file turns the source paper reading into surgical rewrite instructions.

How to read it:
- Each modification names the exact file and line range to replace.
- Each item says why the change is needed.
- Each item includes a "best-paper gate" assessment.
- Copy-paste blocks are LaTeX-ready and meant to replace the referenced text unless stated otherwise.

Important dependency notes:
- I did not use `\ours{}` or `\URSp{}` because I do not see those macros defined in the visible source tree.
- The proposed model name is macroized as `\modelname` in `overleaf/00_main.tex`; use that macro everywhere the model name appears in the manuscript so future renaming is a one-line change.
- The related-work rewrite below avoids adding CA-KGCN, GEM, and IEDR by name because those BibTeX entries are not present in `overleaf/_references.bib` yet.
- Do not drop citations when rewriting prose. If a source passage cites a claim, the replacement block must preserve the same citation key or a stricter equivalent citation.
- Wherever I say "keep the equations/tables", I mean the surrounding prose only should change.

## 00_main.tex

### Modification 0.1: Fix the ACM front-matter placeholders
- Target: `overleaf/00_main.tex`, lines 69-79.
- Why: the current venue metadata still contains sample ACM values (`2016`, `2018`, placeholder ISBN/DOI). That is a submission-hygiene problem and it makes the file look unfinished.
- Best-paper gate: `PASS` if you replace all sample placeholders with the real CIKM 2026 metadata supplied by the venue template or rights form.
- Copy-paste LaTeX:

```latex
\acmConference[CIKM '26]{35th International ACM Conference on Information and Knowledge Management}{<official conference dates>}{Rome, Italy}
\acmISBN{<official ISBN or submission-safe placeholder>}
\acmDOI{<official DOI or submission-safe placeholder>}
```

### Modification 0.2: Rewrite the abstract around the actual contribution
- Target: `overleaf/00_main.tex`, lines 220-223.
- Why: the current abstract is generic, overclaims on BGG, and mentions the code link in a way that wastes scarce abstract space. A best-paper abstract should foreground the contribution, the evaluation gap, and the main empirical pattern.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
\begin{abstract}
Context-aware recommender systems aim to improve personalization by considering situational factors such as time or location. Yet many models still treat context as side information, and standard ranking metrics often ignore whether retrieved items fit the query situation. We address both problems with \modelname, a lightweight graph-based recommender that injects discrete contextual features into edge representations, gates message passing with context, and augments scoring with an explicit context-item compatibility term. The model preserves the efficiency of LightGCN-style propagation while making the learned embeddings context dependent. In parallel, we introduce a family of context-sensitive offline metrics that quantify exact match, partial overlap, weighted alignment, group balance, and context-weighted ranking quality. Across three benchmark datasets, \modelname improves standard ranking performance on Yelp and Frappe and remains competitive on BoardGameGeek under a tighter embedding budget, while the proposed metrics expose context effects that accuracy-only evaluation does not reveal. Overall, the paper shows that contextual gains depend on which feature groups are informative, how sparse the context space is, and how strongly context interacts with collaborative signal.
\end{abstract}
```

## 01_introduction.tex

### Modification 1.1: Replace the entire introduction opening with a tighter thesis-driven version
- Target: `overleaf/01_introduction.tex`, lines 8-16.
- Why: the current introduction is directionally correct but too generic, repeats survey-style background, and ends with an editor comment. A best-paper introduction should get to the gap, the method, and the evaluation contribution quickly.
- Best-paper gate: `PASS`.
- Integration guide:
- Replace the current opening paragraph that begins with `Context-aware recommender systems (CARS) constitute...` with paragraph 1 of the block below.
- Replace the current GNN background paragraph that begins with `In parallel, graph-based recommender systems...` with paragraph 2 of the block below.
- Replace the current gap/solution paragraph that begins with `Despite these advances...` with paragraph 3 of the block below.
- Replace the current ending sentence/roadmap paragraph with paragraph 4 of the block below.
- Copy-paste LaTeX:

```latex
Context-aware recommender systems (CARS) aim to improve personalization by conditioning recommendations on situational factors such as time, location, or activity~\cite{adomavicius2005incorporating,adomavicius2011cars}. This setting is important because user preferences are not stationary: the same user can legitimately want different items under different circumstances~\cite{adomavicius2011cars}. However, two practical problems remain unresolved. First, most context-aware models still treat context as a side signal rather than as part of the relational structure that drives representation learning~\cite{mateos2025systematic}. Second, standard ranking metrics often reward relevance while ignoring whether the retrieved items are appropriate for the query context~\cite{meng2022survey}.

Graph neural network (GNN) recommenders are attractive in this setting because they can model high-order collaborative structure with relatively little architectural overhead~\cite{wu2022graph,sattar2023graph,gao2023survey}. Yet existing GNN-based recommenders typically focus on user--item connectivity and either omit context or inject it in ways that do not affect propagation itself~\cite{mateos2025systematic}. This leaves open the question of how to make GNN recommendation context-sensitive without turning the model into a heavyweight architecture.

To address this gap, we propose \modelname, a lightweight context-aware graph recommender that embeds contextual features on interaction edges, uses those contextual embeddings to gate message passing, and adds an explicit context-item compatibility term at scoring time. In parallel, we introduce a family of offline metrics that measure not only whether a relevant item is retrieved, but also whether it matches the situational conditions of the query. Together, the model and the metrics provide a consistent view of context-aware recommendation: one for learning, one for evaluation.

We evaluate the approach on Yelp, Frappe, and BoardGameGeek. The results show that the benefit of contextual modeling is dataset dependent: it is strongest when the context space is informative and not too sparse, and it becomes more nuanced when memory constraints or highly balanced context groups limit the room for separation. The rest of the paper is organized as follows. Section~\ref{sec:related_work} discusses related work, Section~\ref{sec:model} presents the model, Section~\ref{sec:metrics} defines the metrics, Section~\ref{sec:experiments} reports the experiments, and Section~\ref{sec:conclusions} concludes the paper.
```

## 02_related_work.tex

### Modification 2.1: Replace the whole section preamble and CARS subsection with a concise positioning paragraph
- Target: `overleaf/02_related_work.tex`, lines 8-35.
- Why: the current text contains placeholders, editorial notes, and a thesis statement that is too close to the introduction. Related work should position the contribution, not restate it.
- Best-paper gate: `PASS` if the section keeps the structure below and preserves the citation support.
- Integration guide:
- Replace the current opening CARS paragraph and the following taxonomy paragraph with paragraphs 1-2 of the block below.
- Replace the current FM paragraph with paragraph 3 of the block below.
- Replace the current graph-recommender positioning paragraph with paragraph 4 of the block below.
- Replace the current concluding positioning sentence with paragraph 5 of the block below.
- Copy-paste LaTeX:

```latex
Context-aware recommender systems (CARS) extend the classical user--item paradigm by explicitly conditioning recommendations on situational variables such as time, location, activity, and social context~\cite{adomavicius2011cars,villegas2010characterizing}. This problem is typically organized into three families of methods: contextual pre-filtering, contextual post-filtering, and contextual modeling~\cite{adomavicius2011cars,raza2019progress}. Pre-filtering and post-filtering are attractive because they can reuse standard recommenders with limited engineering overhead, but both keep context outside the core representation-learning loop. Contextual modeling is more expressive because it incorporates context directly into the prediction function, although this comes with familiar trade-offs in sparsity, feature heterogeneity, and optimization complexity~\cite{raza2019progress,meng2022survey}.

Within contextual modeling, factorization machines and their neural extensions remain strong and widely used baselines for CARS~\cite{rendle2010fm,guo2017deepfm,he2017nfm,xiao2017afm,lian2018xdeepfm}. Their main strength is that they natively support sparse multi-field categorical inputs and can capture feature interactions with controlled complexity. However, these approaches mostly exploit context at the scoring layer, which can limit their ability to reshape collaborative representations through context-dependent relational propagation.

Graph-based recommenders, by contrast, have largely focused on non-contextual user--item interaction graphs~\cite{wu2022graph,gao2023survey}. Even when contextual variables are available, they are often injected as auxiliary features, shallow side channels, or post-hoc re-ranking signals rather than being integrated as first-class relational conditioning factors~\cite{sattar2023graph,mateos2025systematic}. This distinction is central to our positioning: we target the specific gap between (i) models that exploit context primarily in scoring and (ii) models that allow context to influence representation propagation itself.

Our contribution is therefore not a claim of a new recommendation paradigm. It is a lightweight contextualization of graph collaborative filtering in which context is attached to interactions and directly modulates message passing. This design aims to preserve the computational simplicity of LightGCN-style architectures while increasing contextual sensitivity where it matters most: in how user and item embeddings are formed from neighborhood evidence.
```

### Modification 2.2: Replace the GNN subsection and explicitly include the closely related citations
- Target: `overleaf/02_related_work.tex`, lines 39-75.
- Why: the current GNN subsection is useful but too close to a literature summary, and the evaluation subsection is mostly a placeholder. The best-paper version should use related work to explain why context-aware propagation and context-aware evaluation belong together.
- Best-paper gate: `PASS` after you replace the three `TODO_*` citation keys with real BibTeX keys.
- Integration guide:
- Replace the current GNN paragraph that starts with `Graph neural networks have become...` through the end of the section with the full block below.
- Keep the citation keys already present in the source (`Wang_2019`, `wu2022graph`, `he2020lightgcnsimplifyingpoweringgraph`, `zhang2025unveilingcontrastivelearningscapability`, `rendle2010fm`, `guo2017deepfm`, `he2017nfm`, `xiao2017afm`, `lian2018xdeepfm`, `manning2008introduction`, `krichene2020sampled`, `adomavicius2011cars`, `meng2022survey`).
- Replace only the three `TODO_*` placeholders with real keys after you add the BibTeX entries.
- Copy-paste LaTeX:

```latex
Graph neural networks have become a standard choice for collaborative filtering because they capture high-order connectivity through message passing while remaining relatively simple to train~\cite{Wang_2019,wu2022graph}. LightGCN showed that, for recommendation, much of the benefit of graph convolution comes from neighborhood aggregation itself, without nonlinear feature transforms or other components inherited from general-purpose GNNs~\cite{he2020lightgcnsimplifyingpoweringgraph}. LightCCF further simplified this design by replacing explicit graph convolution with a neighborhood-aggregation objective, demonstrating that contrastive learning can play a graph-aggregation role in recommender systems~\cite{zhang2025unveilingcontrastivelearningscapability}.

Our model builds on this line of work but makes context part of the propagation process. Instead of treating contextual information as a side feature or a post-hoc scoring adjustment, we encode it on interaction edges and use it to gate the messages exchanged between users and items. This choice preserves the efficiency and interpretability of LightGCN-style propagation while making the learned embeddings sensitive to the current situation.

This positioning is important for novelty calibration. Relative to FM-based contextual modeling~\cite{rendle2010fm,guo2017deepfm,he2017nfm,xiao2017afm,lian2018xdeepfm}, our method injects context into neighborhood propagation rather than only into the score function. Relative to generic GNN recommenders~\cite{wu2022graph,sattar2023graph}, it avoids heavyweight relational graph redesign and keeps a lightweight collaborative-filtering backbone.

To cover closely related context-aware graph recommenders, we explicitly position our approach against three representative lines of work. First, context-aware KG-conditioned recommenders~\cite{TODO_CA_KGCN}\footnote{\textit{Context-aware explainable recommendations over knowledge graphs} (search this title on DBLP and then map it to a real BibTeX key).} similarly condition aggregation on contextual/user signals, but they depend on an external knowledge-graph layer and additional relational modeling choices. Our setting is intentionally narrower: no KG dependency, pure user--item interaction graph, and context conditioning attached directly to interaction edges.

Second, feature-graph enhancement approaches~\cite{TODO_GEM}\footnote{\textit{Generalized Embedding Machines for Recommender Systems} (search this title on DBLP and then map it to a real BibTeX key).} share the intuition that context should participate in graph-based representation learning, but they construct graphs over feature fields and then feed downstream feature-interaction models. In contrast, our approach keeps the interaction graph as the primary substrate and uses context to modulate collaborative propagation itself. This difference matters for complexity, interpretability, and deployment constraints: feature-graph pipelines can be expressive, while edge-conditioned interaction-graph pipelines are often easier to scale in standard recommender stacks.

Third, disentanglement-oriented methods~\cite{TODO_IEDR}\footnote{\textit{IEDR: A Context-aware Intrinsic and Extrinsic Disentangled Recommender System} (search this title on DBLP and then map it to a real BibTeX key).} aim to separate intrinsic preference factors from extrinsic contextual factors. Their objective is conceptually complementary to ours: disentanglement seeks factor separation, whereas our model uses direct contextual gating to adapt propagation with minimal architectural overhead. We therefore position \modelname{} as a lightweight alternative for context adaptation, not as a replacement for disentanglement-based modeling.

Evaluation is the other half of the problem. Standard ranking metrics such as nDCG, Recall, MRR, and MAP measure retrieval quality~\cite{manning2008introduction,krichene2020sampled}, but they do not tell us whether the retrieved items fit the query context~\cite{adomavicius2011cars,meng2022survey}. This concern has also been emphasized in recent context-aware and POI-oriented analyses that discuss coverage and context-validity pitfalls in offline evaluation~\cite{TODO_POI_REFLECTION}\footnote{\textit{Point of Interest Recommendation: Pitfalls and Viable Solutions} (search this title on DBLP and then map it to a real BibTeX key).}. This motivates context-sensitive evaluation: metrics should expose exact contextual consistency, partial overlap, feature-group balance, and context-weighted ranking quality. Our metric family is intended for this role and should be interpreted as a complement to standard ranking metrics, not a replacement.

Overall, the related-work positioning is as follows: (i) we inherit lightweight graph collaborative filtering from LightGCN/LightCCF, (ii) we inject context directly into interaction-level propagation rather than only into feature scoring or external graph modules, and (iii) we evaluate context alignment explicitly rather than relying on accuracy-only proxies. This is the precise novelty scope we claim.
```

## 03_model.tex

### Modification 3.1: Replace the opening roadmap with a cleaner three-part structure
- Target: `overleaf/03_model.tex`, lines 10-13.
- Why: the current roadmap is fine but overly verbose and section-number heavy. A best-paper method section should be easy to scan, with a crisp promise of what each subsection does.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
In this section, we introduce \modelname, a context-aware recommendation model derived from LightCCF~\cite{zhang2025unveilingcontrastivelearningscapability}. The section is organized into three parts. First, we define the context-enriched graph representation and the contextual edge encoder. Second, we present the context-gated message-passing mechanism and the layer-combination strategy. Third, we describe the context-aware scoring function and the training objective.
```

### Modification 3.2: Tighten the problem formulation and contextual edge embedding prose
- Target: `overleaf/03_model.tex`, lines 24-39.
- Why: the current wording is correct but slightly informal. The revision should make it explicit that context lives on edges and that the edge encoder is shared between training and inference.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

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

### Modification 3.3: Reframe the message passing as a deliberate lightweight design choice
- Target: `overleaf/03_model.tex`, lines 43-65.
- Why: the current explanation is good but still reads like a derivation. The rewrite should explain *why* multiplicative gating is the right complexity point and why mean pooling is retained.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
Standard LightGCN~\cite{he2020lightgcnsimplifyingpoweringgraph} propagates node embeddings along graph edges without relational modulation. Inspired by feature-aware edge modulation~\cite{zhuo2025edgegflrethinkingedgeinformation}, we instead use the contextual edge vector $\mathbf{r}_{uv}$ as a feature-wise filter: every dimension of the neighbor embedding is scaled by the corresponding dimension of the context representation. This keeps the propagation linear and scalable while making message passing sensitive to the current context.

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
We do not apply nonlinear activations or additional feature transforms, because the goal is to preserve the efficiency and stability of LightGCN-style propagation while only adding context where it is needed.

After $L$ propagation layers, the final embedding is the mean of all layerwise representations, including the initial embedding:
\begin{equation}
    \mathbf{h}_u^* = \frac{1}{L+1}\sum_{l=0}^{L} \mathbf{h}^{(l)}_u, \qquad
    \mathbf{h}_v^* = \frac{1}{L+1}\sum_{l=0}^{L} \mathbf{h}^{(l)}_v.
    \label{eq:layer_combination}
\end{equation}
This layer combination captures both local and higher-order collaborative signals while avoiding the over-smoothing that typically appears when only the last layer is used~\cite{li2018deeperinsightsgraphconvolutional}.
```

### Modification 3.4: Make the scoring and objective sections more direct
- Target: `overleaf/03_model.tex`, lines 69-100.
- Why: the scoring paragraph should clearly separate inference-time context conditioning from the training objective, and the current training explanation repeats itself.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
\paragraph{Scoring.}
At inference time, the relevance score between user $u$ and item $v$ under query context $\mathbf{c}_q$ is
\begin{equation}
    \hat{y}_{uv} = \mathbf{h}_u^* \cdot \mathbf{h}_v^* + \mathbf{r}_q \cdot \mathbf{h}_v^*,
    \label{eq:score}
\end{equation}
where $\mathbf{r}_q$ is computed with the same contextual encoder used for edge embeddings. The first term captures general user--item affinity learned from context-gated propagation; the second adds an explicit context--item compatibility signal at prediction time.

\paragraph{Training Objective.}
We optimize the joint objective proposed by LightCCF~\cite{zhang2025unveilingcontrastivelearningscapability}:
\begin{equation}
    \mathcal{L} = \mathcal{L}_{\mathrm{BPR}} + \alpha\,\mathcal{L}_{\mathrm{NA}} + \lambda\,\|\mathbf{E}_0\|^2_F,
    \label{eq:loss}
\end{equation}
where $\alpha$ and $\lambda$ are hyperparameters and $\mathbf{E}_0$ denotes the base user/item embeddings. The BPR term ranks positive items above sampled negatives under the context-aware score in Eq.~\eqref{eq:score}. The neighborhood-aggregation term encourages users to remain close to their interacted items in the learned space, acting as a complementary signal to message passing. L2 regularization controls embedding growth and improves generalization.

Overall, the objective keeps the model aligned with the recommendation task while preserving the lightweight design of the propagation module.
```

## 04_metrics.tex

### Modification 4.1: Replace the section opening and Family 1 prose with a formal definition block
- Target: `overleaf/04_metrics.tex`, lines 10-89.
- Why: the current opening is too informal, the notion of representative context is underdefined, and the metrics read like a list rather than a measurement framework.
- Best-paper gate: `CONDITIONAL`. The rewrite is A*-level in wording and formalization, but the section only becomes fully convincing if the later experimental discussion stops overclaiming WCA/CGB behavior.
- Copy-paste LaTeX:

```latex
Standard ranking metrics such as nDCG, Recall, MAP, and MRR measure whether relevant items are retrieved~\cite{manning2008introduction,krichene2020sampled}, but they do not tell us whether those items fit the context of the query~\cite{adomavicius2011cars}. We therefore define a family of context-sensitive offline metrics that operate only on the contextual attributes already available in the dataset, without requiring additional annotations.

Let $c_q$ denote the query context of a held-out interaction and let $c_i=\phi(i)$ denote the representative context of item $i$. We define $\phi(i)$ as the per-feature mode over the historical contexts in which item $i$ appears; ties are broken first by global feature frequency and then by recency. All metrics below are computed over the ranked list $R_q^K$ for each query $q\in\mathcal Q$.

We organize the metrics into three complementary families. The first family measures exact or partial contextual agreement between the query and each recommended item. The second family diagnoses how context is distributed across feature groups. The third family injects context directly into classical ranking metrics.

\textit{Family 1 --- Context Similarity and Satisfaction Metrics} measure the degree of set-based or geometric alignment between the query context $c_q$ and the representative context $c_i$ of each recommended item. These metrics are intentionally complementary: ACC captures strict consistency, CS captures partial overlap, WCS discounts common features, WCA measures weighted geometric alignment, and Friction measures feature-wise agreement.

 \textbf{ACC@K} measures the fraction of recommended items whose contextual attributes exactly match the query context across all feature dimensions. It is a strict diagnostic: a model that is contextually close but not exact receives no partial credit.

 \textbf{CS} relaxes exact matching by using a modified Jaccard coefficient with penalty parameter $\alpha\geq 0$~\cite{jorro2024context}. It captures whether the item and query share a substantial part of the same context, even when the match is not perfect. In all experiments we use $\alpha=0.5$, which provides a moderate penalty for missing query features.

 \textbf{WCS} extends CS with IDF-based feature weights $w_f$, so that rare and discriminative features contribute more than common ones. This is important when some context dimensions are much more frequent than others, because a plain overlap score can otherwise be dominated by high-frequency features.

 \textbf{WCA} measures weighted cosine alignment between the query and item context vectors. It is the most geometric of the similarity metrics and therefore the most sensitive to how the context vectors are encoded. On datasets where one-hot or binary encodings make the measure structurally saturate, WCA should be interpreted as a diagnostic quantity rather than as a primary ranking signal.

 \textbf{Friction} is the complement of normalized Hamming distance. It measures the proportion of contextual features that match exactly between the query and the recommended item, which makes it easy to interpret as a feature-level match rate.
```

### Modification 4.2: Replace Family 2, Family 3, and the closing paragraph
- Target: `overleaf/04_metrics.tex`, lines 111-208.
- Why: the current discussion mixes definitions, interpretation, and claims about novelty. The revised version should make the diagnostic role of each metric explicit and avoid overstating what a metric can prove.
- Best-paper gate: `CONDITIONAL`. The text is A*-level, but the empirical section must stop describing saturated metrics as if they were universally discriminative.
- Copy-paste LaTeX:

```latex
\textit{Family 2 --- Advanced Context Dynamics} analyzes structural and distributional properties of the recommendation list with respect to contextual quality, beyond per-item alignment.

\textbf{CR@K (Context Recall)} shifts the evaluation focus from items to features. It measures the average fraction of query-context features covered by the top-$K$ items, and therefore answers a different question from CS: not "how similar is a single item?" but "how much of the requested context is covered by the list?" This makes CR useful when the user context is only partially satisfiable.

\textbf{CGB@K (Context Group Balance)} measures whether the recommendation list covers the predefined context groups evenly. Let $\mathcal{G}=\{G_1,\ldots,G_n\}$ be the set of feature groups and let $\mathrm{CR}_g@K$ denote the group-specific context recall for group $g$. Then
\begin{equation}
    \mathrm{CGB@K} = 1 - \min\!\left(\frac{\sigma_{\text{groups}}}{\sigma_{\max}},\, 1\right),
\end{equation}
where $\sigma_{\text{groups}}$ is the standard deviation of the group recalls and $\sigma_{\max}=\sqrt{(|\mathcal{G}|-1)/|\mathcal{G}|^2}$ is the maximum dispersion attainable when one group receives all the mass. High CGB means that the model does not overfit one context family at the expense of the others.

\textit{Family 3 --- Context-Weighted Ranking Metrics} injects contextual appropriateness directly into the relevance term of classical ranking metrics. Let
\begin{equation}
    \mathrm{rel}_{\mathrm{cw}}(k) = \mathrm{rel}(k)\cdot s(c_q,c_{i_k}),
\end{equation}
where $s(\cdot)$ is one of the context-similarity functions defined above. We use this context-weighted relevance to compute CW-nDCG@K and CW-MAP@K. The resulting scores are easy to interpret: if they are close to the standard ranking metrics, the model retrieves relevant items in contextually appropriate situations; if they are much lower, the model retrieves relevant items but in the wrong context.

Taken together, the metrics separate five distinct failure modes: exact mismatch, partial mismatch, feature imbalance, coverage imbalance, and context-aware ranking degradation. This is why we report them as a family rather than as a single number. Table~\ref{tab:metrics_summary} summarizes the role of each metric.
```

## 05_experiments.tex

### Modification 5.1: Condense the dataset descriptions and remove over-assertive phrasing
- Target: `overleaf/05_experiments.tex`, lines 12-59.
- Why: the dataset subsection is informative, but it spends too much space telling the reader what the datasets are instead of why each dataset is useful for the paper's claims. A best-paper experiment section uses dataset descriptions to set up the scientific contrast.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
We evaluate the proposed model on three benchmark datasets that differ in context sparsity, feature cardinality, and interaction density.

\smallskip\noindent\textbf{Frappe}~\cite{frappe} is a mobile-app recommendation dataset with eight contextual features organized into temporal, activity, and environment groups. It is useful because its context space is sparse and heterogeneous, which makes it a good test of whether context-gated propagation can exploit informative but irregular context signals.

\smallskip\noindent\textbf{Yelp}~\cite{yelp2024} is a large-scale local-business dataset with eleven contextual features organized into temporal, social/user, and spatial groups. Its high-cardinality spatial features make it the most contextually complex benchmark in the study and therefore a good stress test for context-aware evaluation.

\smallskip\noindent\textbf{BoardGameGeek (BGG)}~\cite{jorro2024boardgame} contains explicit contextual annotations for board-game recommendations and has a compact but semantically rich context space. It is the cleanest benchmark for studying context-aware ranking because the playing situation strongly determines which item is appropriate.
```

### Modification 5.2: Make the baseline paragraph neutral and remove the "state-of-the-art" tone
- Target: `overleaf/05_experiments.tex`, lines 63-95.
- Why: the current paragraph overstates certainty and keeps a slightly awkward phrasing ("models , all trained"). A best-paper paper should sound precise, not promotional.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
We compare \modelname{} against three non-contextual baselines and five context-aware FM-based models, all trained within the WarpRec framework~\cite{warprec}.

\smallskip\noindent\textbf{Non-contextual baselines.}
\emph{Random} assigns uniform random scores to all items and serves as a lower bound. \emph{Popularity} ranks items by global interaction count and is often strong in datasets with a heavy-tailed item distribution. \emph{LightCCF} is the graph-based recommender from which our model is derived.

\smallskip\noindent\textbf{Context-aware FM-based models.}
Following the contextual modeling paradigm, we select five representative FM-based baselines. \emph{FM} models pairwise feature interactions through shared latent factors~\cite{rendle2010fm}. \emph{DeepFM} combines an FM component with a deep MLP~\cite{guo2017deepfm}. \emph{NFM} replaces FM pooling with a Bi-Interaction layer followed by an MLP~\cite{he2017nfm}. \emph{AFM} adds attention over pairwise feature interactions~\cite{xiao2017afm}. \emph{xDeepFM} uses a Compressed Interaction Network to model bounded-degree feature interactions at the vector level~\cite{lian2018xdeepfm}.
```

### Modification 5.3: Clarify the evaluation methodology and explicitly state the capacity caveat once
- Target: `overleaf/05_experiments.tex`, lines 103-129.
- Why: the current methodology paragraph is doing too many things at once and contains a long sentence that is hard to parse. The rewrite should make the test protocol, context usage, and capacity caveat explicit.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

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

### Modification 5.4: Replace the results narrative with an honest, structured summary
- Target: `overleaf/05_experiments.tex`, lines 145-324.
- Why: the current narrative overstates a few wins, glosses over the BGG capacity caveat, and repeats the same claim in multiple places. The best-paper version should read like a disciplined analysis, not a victory lap.
- Best-paper gate: `CONDITIONAL`. This becomes A*-level only if the surrounding prose is made more measured and the tables are left to speak for themselves.
- Copy-paste LaTeX:

```latex
We report both standard ranking metrics and context-aware metrics. The main pattern is consistent across the section: the benefit of context gating is strongest when the dataset has informative context and enough structure for the context encoder to exploit, and it is less decisive when memory constraints or near-saturated context groups limit separation.

\paragraph{Standard ranking metrics.}
On Yelp, \modelname{} is the strongest model on all four standard ranking metrics, which suggests that context-aware propagation and context-aware scoring improve classic recommendation quality when the context space is rich but not excessively sparse. On Frappe, \modelname{} again leads on nDCG@10, MRR@10, and Recall@10, while Precision@10 is tied with AFM. This is a good sign: the model is not only effective on a large-scale dataset, but it also remains competitive on a smaller and sparser benchmark where contextual variation is important. On BGG, however, the ranking picture is more nuanced. \modelname{} remains competitive and outperforms the FM-based baselines, but it does not beat the strongest graph baseline in the standard ranking setting because its embedding size is reduced to fit the available GPU memory. We should therefore treat the BGG ranking results as a constrained but still informative comparison, not as a pure capacity-matched head-to-head.

\paragraph{Context-aware metrics.}
The context-aware metrics refine this picture. On Yelp and Frappe, \modelname{} leads on most of the similarity, coverage, and context-weighted ranking metrics, which indicates that the gains seen in standard ranking are accompanied by stronger contextual alignment. On BGG, the model achieves its clearest gain on geometric alignment and context-weighted ranking, while some group-balanced or exact-match metrics remain high for simpler baselines such as Popularity. That is not a contradiction: it shows that the different metrics are measuring different failure modes. In particular, high CGB on BGG should be read as balanced coverage across the three context groups, not as evidence that a model is contextually optimal. The metric family is useful precisely because it separates these cases.

\paragraph{Overall.}
Taken together, the results suggest three conclusions. First, encoding context directly in message passing can improve recommendation quality without abandoning the efficiency of graph-based collaborative filtering. Second, the context-aware metrics reveal information that standard ranking metrics hide, especially when the dataset is large or the context space is highly structured. Third, the strongest gains are dataset dependent, which is exactly what we should expect from a context-sensitive method rather than a one-size-fits-all architecture.
```

### Modification 5.5: Rewrite the contextual feature ablation discussion to be more analytical
- Target: `overleaf/05_experiments.tex`, lines 599-739.
- Why: the current ablation text is useful but reads like a raw result log. A best-paper ablation explains what the patterns mean, why they differ across datasets, and what the limits of the evidence are.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
The ablation study isolates which contextual feature groups are most useful for each dataset. The main message is that context utility is not uniform: the best subset depends on how the dataset was collected and on which contextual groups are most semantically informative.

\subsubsection{Yelp}
On Yelp, the strongest configuration combines Temporal and Location features, which is consistent with the intuition that restaurant or business recommendations depend heavily on when and where the interaction happens. Adding Atmosphere or static user attributes does not help and can even hurt, which suggests that redundant or noisy features can dilute the signal. This pattern is also consistent with prior context-aware studies on Yelp-like settings~\cite{nguyen2025item,lu2020multi,Gao2020GraphNN}. The key takeaway is not that more context is always better, but that the right context subset matters more than the full feature set.

\subsubsection{Frappe}
On Frappe, Environment features alone are the most informative, and the full feature set is only a close second. This means that the app-discovery setting is driven more by external situational conditions than by the other available groups, in line with earlier findings on context salience in app recommendation~\cite{zhong2023context}. The weaker performance of Temporal + Activity alone indicates that these groups do not always combine constructively unless they are grounded by environmental context.

\subsubsection{BoardGameGeek}
On BGG, Playtime + Mood is the best subset, with Social alone and Playtime + Social very close behind. Playtime by itself is clearly weaker, which suggests that duration is informative only when paired with additional situational cues. The ablation therefore supports the interpretation that contextual recommendation works best when the feature groups capture complementary aspects of the situation rather than a single coarse dimension.

\paragraph{Cross-model observation.}
For the context-aware FM baselines, performance does not change much across feature subsets. This is not evidence that context is irrelevant; it suggests that these models use context mainly at the score level, whereas \modelname{} injects context into propagation itself. That architectural difference makes the proposed model more sensitive to which contextual groups are selected.
```

### Modification 5.6: Rewrite the qualitative validation-signal discussion and add a limitations bridge
- Target: `overleaf/05_experiments.tex`, lines 748-760, plus a new subsection immediately after that block.
- Why: the current text is useful but incomplete. It should end with a clear finding and then transition to limitations instead of stopping at the figure description.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
Beyond the quantitative results, we ask whether optimizing the model with CW-nDCG@10 changes the user-level ranking behavior. To test this, we compare the standard validation setting (\textsc{Base}) with a context-weighted validation setting (\textsc{CA-Val}) under the same feature configuration. The result is intentionally modest: context-weighted validation changes the ranking behavior in some cases, but it does not produce a uniform hit-rate improvement across datasets. This is an important negative finding because it suggests that context-aware validation is not automatically better than standard ranking validation.

This negative result naturally motivates an explicit discussion of limitations and threats to validity, which we separate in a dedicated subsection below.
```

### Modification 5.7: Add a dedicated limitations section immediately after the experiments
- Target: `overleaf/05_experiments.tex`, immediately after the end of the qualitative analysis block.
- Why: the best-paper plan treats limitations as a mature, standalone section rather than a side remark. The rewrite plan should therefore make the limitations block explicit, not merely implied inside the experiments narrative.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
\subsection{Limitations and Threats to Validity}
\label{sec:experiments:limitations}

The current study has four main limitations. First, the model assumes discrete contextual variables and does not yet support continuous context representations directly. Second, the BGG benchmark exposes a memory-efficiency trade-off: context-aware propagation can force a smaller embedding size, which means that capacity-matched comparison is not always possible. Third, some of the proposed context-aware metrics can saturate or become weakly discriminative on particular encodings, so they should be interpreted as diagnostics rather than as universal optimization targets. Fourth, the empirical section does not report multi-seed variance or significance tests, so the results should be read as strong descriptive evidence rather than as statistically certified superiority.

These limitations do not undermine the central claim of the paper. They instead define the scope of the evidence and motivate future work on continuous contexts, memory-aware propagation, and more robust context-sensitive validation objectives.
```

## 06_conclusions.tex

### Modification 6.1: Replace the conclusion with a shorter, more honest synthesis
- Target: `overleaf/06_conclusions.tex`, lines 7-10.
- Why: the current conclusion repeats the results section and overstates "competitive or superior" performance without immediately acknowledging the dataset-dependent nature of the gains.
- Best-paper gate: `PASS`.
- Copy-paste LaTeX:

```latex
This work introduced \modelname{}, a context-aware graph recommender that integrates contextual information directly into propagation through context-gated message passing and explicit context-aware scoring. We also proposed a family of context-sensitive evaluation metrics that expose exact match, partial overlap, weighted alignment, group balance, and context-weighted ranking quality.

The experiments show that the benefit of context-aware propagation is real but dataset dependent: it is strongest on Yelp and Frappe, where the contextual signal is informative enough to improve standard ranking as well as context-sensitive metrics, and more nuanced on BGG, where memory constraints and balanced context groups limit the separation between models. The ablation study further shows that the best contextual feature subset depends on the dataset, which confirms that contextual recommendation is sensitive to which situational dimensions are actually informative.

Overall, the paper supports a simple conclusion: context should be modeled as part of the interaction structure, but it should also be evaluated as part of the ranking task. Future work should extend the method to continuous context, improve memory efficiency on large context spaces, and further refine context-sensitive validation objectives.
```

## Notes on what not to change yet

- Leave the numeric tables untouched unless you are also editing the underlying results text.
- Do not add missing citations to CA-KGCN, GEM, or IEDR until their BibTeX entries exist.
- Do not introduce `\ours{}` or `\URSp{}` unless you first add those macros to the paper source.

## Suggested editing order

1. `00_main.tex` front matter and abstract.
2. `01_introduction.tex`.
3. `02_related_work.tex`.
4. `03_model.tex`.
5. `04_metrics.tex`.
6. `05_experiments.tex`.
7. `06_conclusions.tex`.

If you want, the next useful step is to turn this plan into actual patches for the manuscript, one file at a time, starting from the abstract and introduction.
