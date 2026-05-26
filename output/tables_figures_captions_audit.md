# Indice Tabelle e Figure — Audit Caption A*

> **Criterio A\***: Una caption è **self-contained** (comprensibile senza leggere il testo circostante), **informativa** (variabili chiave, cutoff, abbreviazioni sciolte), **concisa ma completa**, con **notazione consistente**.

---

## Tabella 1 — §4 Metrics

| # | Label | Tipo | Caption corrente | A*? | Fix proposto |
|---|-------|------|------------------|-----|-------------|
| 1 | [`tab:metrics_summary`](overleaf/04_metrics.tex:141) | Tabella | *Complementarity of the context similarity metrics.* | ❌ | **Troppo breve.** Non spiega *cosa* rende le metriche complementari, non elenca le 5 metriche, non menziona le colonne (Approach, Focus). |

> **Fix**: `Complementarity of the proposed context similarity metrics. Each metric targets a distinct failure mode: exact matching (ACC), partial set overlap (CS), rare-feature alignment (WCS), geometric alignment (WCA), and feature-level agreement (Friction).`

---

## §5 Experiments — Metriche Standard (3 tabelle)

| # | Label | Tipo | Caption corrente | A*? | Fix proposto |
|---|-------|------|------------------|-----|-------------|
| 2 | [`tab:yelp_traditional_metrics`](overleaf/05_experiments.tex:90) | Tabella | *Traditional Ranking Metrics on Yelp. Bold values indicate the best-performing model.* | ~ | Manca cutoff $K$. La frase sul bold è standard ma ridondante. |
| 3 | [`tab:frappe_traditional_metrics`](overleaf/05_experiments.tex:123) | Tabella | *Traditional Ranking Metrics on Frappe.* | ❌ | Manca cutoff $K$ **e** manca la nota sul bold (presente in Yelp ma non qui — inconsistenza). |
| 4 | [`tab:bgg_traditional_metrics`](overleaf/05_experiments.tex:159) | Tabella | *Traditional Ranking Metrics on BGG.* | ❌ | Stesso problema di Frappe. |

> **Fix unificato** (applicare a tutte e tre):
> - Yelp: `Standard ranking metrics at cutoff $K=10$ on Yelp. Bold indicates the best result.`
> - Frappe: `Standard ranking metrics at cutoff $K=10$ on Frappe. Bold indicates the best result.`
> - BGG: `Standard ranking metrics at cutoff $K=10$ on BGG. Bold indicates the best result.`

---

## §5 Experiments — Metriche Context-Aware (2 tabelle + 3 sub-tabelle)

| # | Label | Tipo | Caption corrente | A*? | Fix proposto |
|---|-------|------|------------------|-----|-------------|
| 5 | [`tab:ca_metrics_all`](overleaf/05_experiments.tex:318) | Tabella (con sub-table) | *Context-aware metrics at cutoff $K=10$ on Yelp, Frappe, and BGG. Bold values indicate the best result. Fric. = Friction. WCA is excluded from Frappe (structurally saturated at 1.0).* | ✅ **A*** | Completa: cutoff, dataset, abbreviazioni, esclusione WCA motivata. |
| 5a | [`tab:ca_metrics_yelp`](overleaf/05_experiments.tex:333) | Sub-tabella | *Yelp* | ✅ **A*** | Sub-caption minima ma sufficiente perché la caption principale è esaustiva. |
| 5b | [`tab:ca_metrics_frappe`](overleaf/05_experiments.tex:365) | Sub-tabella | *Frappe* | ✅ **A*** | Idem. |
| 5c | [`tab:ca_metrics_bgg`](overleaf/05_experiments.tex:399) | Sub-tabella | *BGG* | ✅ **A*** | Idem. |
| 6 | [`tab:wcs_breakdown`](overleaf/05_experiments.tex:472) | Tabella | *Weighted Context Satisfaction (WCS) at cutoff $K=10$ breakdown per context group.* | ✅ **A*** | Chiara, specifica cutoff, spiega il contenuto. |

---

## §5 Experiments — Ablation (3 tabelle)

| # | Label | Tipo | Caption corrente | A*? | Fix proposto |
|---|-------|------|------------------|-----|-------------|
| 7 | [`tab:yelp_ablation`](overleaf/05_experiments.tex:537) | Tabella | *Yelp contextual feature subsets, ordered by nDCG (descending).* | ~ | OK ma manca cutoff $K$ per consistenza con le altre tabelle. |
| 8 | [`tab:frappe_ablation`](overleaf/05_experiments.tex:575) | Tabella | *Frappe contextual feature subsets.* | ❌ | Manca ordinamento (a differenza di Yelp) e cutoff $K$. Inconsistenza con Yelp. |
| 9 | [`tab:bgg_ablation`](overleaf/05_experiments.tex:628) | Tabella | *BGG contextual feature subsets.* | ❌ | Stesso problema di Frappe. |

> **Fix unificato**:
> - Yelp: `Yelp contextual feature subsets at cutoff $K=10$, ordered by nDCG (descending).`
> - Frappe: `Frappe contextual feature subsets at cutoff $K=10$, ordered by nDCG (descending).`
> - BGG: `BGG contextual feature subsets at cutoff $K=10$, ordered by nDCG (descending).`

---

## §5 Experiments — Validation Analysis (1 figura + 2 tabelle)

| # | Label | Tipo | Caption corrente | A*? | Fix proposto |
|---|-------|------|------------------|-----|-------------|
| 10 | [`fig:hit_rate_comparison`](overleaf/05_experiments.tex:672) | Figura (bar chart) | *Comparison of Hit Rate under standard (\textsc{Base}) and context-aware (\textsc{CA-Val}) validation across three datasets.* | ✅ **A*** | Chiara, specifica i due setup, menziona i dataset. |
| 11 | [`tab:ca_metrics_abl`](overleaf/05_experiments.tex:726) | Tabella | *Comparison of context similarity \& satisfaction metrics under standard (\textsc{Base}) and context-aware (\textsc{CA-Val}) validation. Fric. = Friction. WCA excluded from Frappe.* | ✅ **A*** | Completa: setup, abbreviazioni, esclusione motivata. |
| 12 | [`tab:rank_shift`](overleaf/05_experiments.tex:788) | Tabella | *Rank comparison on $\mathcal{U}_{\text{both}}$: fraction of users for whom \textsc{CA-Val} promotes, demotes, or preserves the rank of the positive item relative to \textsc{Base}.* | ✅ **A*** | Self-contained, spiega perfettamente le tre condizioni. |

---

## Riepilogo

| Esito | Conteggio |
|-------|-----------|
| ✅ **A\*** | 8 (5a, 5b, 5c, 6, 10, 11, 12, e la 5 principale) |
| ~ **Borderline** | 2 (tab:yelp_traditional_metrics, tab:yelp_ablation) |
| ❌ **Non A\*** | 4 (tab:metrics_summary, tab:frappe_traditional_metrics, tab:bgg_traditional_metrics, tab:frappe_ablation, tab:bgg_ablation) — ma note come 5 elementi? No: 1 + 2 + 2 = 5 ❌ |

**Aggiornamento**: 1 (metrics_summary) + 2 (frappe + bgg traditional) + 2 (frappe + bgg ablation) = **5 caption non A\***, **2 borderline**, **5 A\*** (contando la ca_metrics_all come una).

### Problemi sistemici

1. **Inconsistenza tra tabelle simili**: `frappe_traditional_metrics` e `bgg_traditional_metrics` mancano della nota sul bold che `yelp_traditional_metrics` ha.
2. **Cutoff $K$ mancante in 5 tabelle su 12**: tutte le traditional metrics (3) e ablation (3, eccetto Yelp che ha ordinamento ma non cutoff).
3. **Ordinamento non dichiarato in 2 ablation su 3**: Frappe e BGG non specificano "ordered by nDCG descending" come Yelp.
4. **Caption §4 troppo minimal**: non spiega la complementarietà, che è il punto centrale della tabella.
