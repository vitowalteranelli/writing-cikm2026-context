# Comprehensive Proofreading & Language Audit — Merged Report

**Paper:** *Graph Neural Networks for Context-Aware Recommendations under Context-Sensitive Evaluation Dimensions*  
**Target:** Best Paper Award @ CIKM 2026  
**Analysis date:** 2026-05-24  
**Language target:** American English

---

## Methodology

L'analisi è stata condotta in **due passate indipendenti** su tutti i file sorgenti in [`overleaf/`](overleaf/):

| Passata | Focus | Totale issue trovati |
|---------|-------|---------------------|
| **Pass 1** | Scansione sistematica: errori tipografici, formattazione, AmE/BrE, awkward phrasing, hyphenation, grammatica, LaTeX sporco | 38 |
| **Pass 2** | Rilettura completa di ogni file con attenzione a: problemi sottili, errori di consistenza, annotazioni LaTeX residue, riferimenti di linea errati, informalità residue | 22 nuovi |
| **Merge** | Unione delle due liste + deduplicazione vs [`output/paper_language_audit.md`](output/paper_language_audit.md) | **60 totali** |

Questa merge report include:
- Tutti i **38 issue della Pass 1** (con categorizzazione originale)
- **22 nuovi issue della Pass 2** (non presenti in nessuno dei report precedenti)
- Riferimenti incrociati al report parallelo [`output/paper_language_audit.md`](output/paper_language_audit.md) (che contiene ulteriori ~116 issue di stile, consistenza e contenuto)

> **Nota:** I due report sono complementari. Questo report si concentra su errori *diretti e verificabili* (typos, markup, phrasing, hyphenation). Il report `paper_language_audit.md` copre issues più ampi (consistenza tra sezioni, overclaiming, struttura argomentativa). Si raccomanda di usarli insieme.

---

## Indice

1. [Pass 1 — Issue trovati (38)](#pass-1--issue-trovati-38)
   - [A: Errori tipografici e di formattazione (7)](#a-errori-tipografici-e-di-formattazione)
   - [B: American English vs British English (3)](#b-american-english-vs-british-english)
   - [C: Awkward / unclear phrasing (20)](#c-awkward--unclear-phrasing)
   - [D: Hyphenation issues (4)](#d-hyphenation-issues)
   - [E: Grammatical inconsistencies (1)](#e-grammatical-inconsistencies)
   - [F: Stray LaTeX / markup (3)](#f-stray-latex--markup)
2. [Pass 2 — Nuovi issue trovati (22)](#pass-2--nuovi-issue-trovati-22)
   - [G: Errori di markup LaTeX (5)](#g-errori-di-markup-latex)
   - [H: Awkward phrasing aggiuntivi (6)](#h-awkward-phrasing-aggiuntivi)
   - [I: Inconsistenze e refusi (6)](#i-inconsistenze-e-refusi)
   - [J: Correzioni a report precedenti (2)](#j-correzioni-a-report-precedenti)
   - [K: Pulizia commenti residui (3)](#k-pulizia-commenti-residui)
3. [Riepilogo statistico](#riepilogo-statistico)
4. [Priorità di intervento](#priorità-di-intervento)

---

# Pass 1 — Issue trovati (38)

## Categoria A: Errori tipografici e di formattazione

### A1 — Extra space before comma

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:27) | 27 | `FM-based models , all trained` | `FM-based models, all trained` |

Rimuovere lo spazio prima della virgola. ✅ Già segnalato in `paper_language_audit.md` #44.

---

### A2 — Stray/unparsed number in table cell

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:156) | 156 | `NFM 0.2549 & 0.0312 & 0.0224 & 0.0069 & 0.0607 \\` | `NFM & 0.0312 & 0.0224 & 0.0069 & 0.0607 \\` |

Il numero `0.2549` è un residuo spurio che rompe l'allineamento della tabella. ✅ Già segnalato in `paper_language_audit.md` #56, #85.

---

### A3 — Missing space after word before `\textbf`

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:224) | 224 | `On\textbf{ Frappe}` | `On \textbf{Frappe}` |

Manca lo spazio prima del comando `\textbf`.

---

### A4 — Missing period at end of sentence

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:50) | 50 | `...is known at query time \cite{Rashed_2022}` | `...is known at query time \cite{Rashed_2022}.` |

Manca il punto fermo alla fine della frase. ✅ Già segnalato in `paper_language_audit.md` #49 (con ref. [21]).

---

### A5 — Redundant space before non-breaking space tilde

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:49) | 49 | `Eq. ~\ref{eq:score}` | `Eq.~\ref{eq:score}` |

Lo spazio prima della tilde (`~`) è ridondante.

---

### A6 — Commented-out content with stray `\iffalse` environments

| File | Linee | Note |
|------|-------|------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:52) | 52–59 | Blocco `\iffalse` annidato |
| [`05_experiments.tex`](overleaf/05_experiments.tex:450) | 450–456 | `\iffalse` environment per `tablenotes` |

Si consiglia pulizia.

> **ERRATA CORRIGE:** La prima analisi (Pass 1) indicava erroneamente un blocco `\iffalse` a `04_metrics.tex:450–456`. Il file [`04_metrics.tex`](overleaf/04_metrics.tex) termina alla linea 311 — tale riferimento non esiste. Vedi **G9** per dettagli.

---

### A7 — `\textcolor{red}` / `\textcolor{blue}` commenti non rimossi

Il paper contiene ancora commenti di revisione colorati:

| File | Linee | Testo |
|------|-------|-------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:25) | 25 | `%\textcolor{red}{Iván: I have revised abstract and intro...}` |
| [`02_related_work.tex`](overleaf/02_related_work.tex:13) | 13 | `%\textcolor{blue}{I explained this acronym...}` |
| [`02_related_work.tex`](overleaf/02_related_work.tex:30) | 30 | `%\textcolor{blue}{it may be strange...}` |
| [`04_metrics.tex`](overleaf/04_metrics.tex:7) | 7 | `%\textcolor{blue}{some introduction...}` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:60) | 60 | `%\textcolor{blue}{I don't think we have space...}` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:88) | 88 | `%\textcolor{blue}{proposal for tables...}` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:90) | 90 | `%\textcolor{blue}{how important is to report AUC?}` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:334) | 334 | `%\textcolor{blue}{Same as Table...}` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:495) | 495 | `%\textcolor{blue}{Same as Table...}` |

Vanno tutti rimossi prima della submission.

---

## Categoria B: American English vs British English

### B1 — `nonlinear` vs `non-linear`

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`03_model.tex`](overleaf/03_model.tex:68) | 68 | `No nonlinear activations...` | ✅ American English (`nonlinear`) |
| [`03_model.tex`](overleaf/03_model.tex:90) | 90 (comm.) | `no non-linear activation` | ❌ British English (`non-linear`) — solo in commento |

### B2 — `over-smoothing` (hyphenated)

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`03_model.tex`](overleaf/03_model.tex:76) | 76 | `over-smoothing` | ❌ AmE preferisce `oversmoothing` |
| [`03_model.tex`](overleaf/03_model.tex:126) | 126 | `over-smoothing` | ❌ Idem |

Uniformare a `oversmoothing` per coerenza con AmE.

### B3 — `well-suited` (hyphenated)

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:13) | 13 | `well-suited` | ⚠️ In posizione predicativa ("are well suited"), AmE preferisce senza trattino |

---

## Categoria C: Awkward / unclear phrasing

### C1 — "This capability provides important benefits"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:10) | 10 | `This capability provides important benefits, including greater adaptability to real-world scenarios and increased user satisfaction.` | `This makes recommendations more adaptable to real-world scenarios and increases user satisfaction.` |

"Provides important benefits" è tautologico.

### C2 — "high-order" → "higher-order"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:13) | 13 | `high-order collaborative structure` | `higher-order collaborative structure` |
| [`01_introduction.tex`](overleaf/01_introduction.tex:14) | 14 | `high-order connectivity patterns` | `higher-order connectivity patterns` |

Il paper usa sia `high-order` (ll. 13, 14) che `higher-order` (l. 76 `03_model.tex`, l. 32 `05_experiments.tex`). ✅ Già segnalato in `paper_language_audit.md` #7.

### C3 — "propagation itself"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:14) | 14 | `...incorporate it in ways that do not affect propagation itself.` | `...ways that do not affect propagation.` |

`itself` è filler.

### C4 — "one for learning, the other for evaluation"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:19) | 19 | `Together, the model and the metrics provide a consistent view of context-aware recommendation: one for learning, the other for evaluation.` | `Together, the model and the metrics provide a consistent view of context-aware recommendation—the former for learning, the latter for evaluation.` |

Costrutto ambiguo: meglio "the former / the latter".

### C5 — "the benefit of contextual modeling is dataset dependent"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:22) | 22 | `the benefit of contextual modeling is dataset dependent` | `the benefits of contextual modeling are dataset-dependent` |

✅ Già segnalato in `paper_language_audit.md` #3.

### C6 — "shallow side channels"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:10) | 10 | `...they are often incorporated as auxiliary features, shallow side channels, or post-hoc re-ranking signals...` | `...they are often incorporated as auxiliary features, shallow side-channel signals, or post-hoc re-ranking adjustments...` |

Metafora vaga.

### C7 — "relatively little architectural overhead"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:13) | 13 | `...with relatively little architectural overhead.` | `...with low architectural overhead.` |

`relatively little` è colloquiale.

### C8 — "gets better or comparable with other competitors"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:221) | 221 | `...gets better or comparable with other competitors...` | `...performs favorably against competitors on most context-aware metrics` |

✅ Già segnalato in `paper_language_audit.md` #60.

### C9 — "evidencing context-gated message passing is able to capture"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:225) | 225 | `...evidencing context-gated message passing is able to capture...` | `...demonstrating that context-gated message passing captures...` |

✅ Già segnalato in `paper_language_audit.md` #66.

### C10 — "the best concordance"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:227) | 227 | `...achieving the best concordance on the Environment group` | `...achieving the best alignment on the Environment group` |

`concordance` è inusuale in questo contesto.

### C11 — "much better fitted to the query context"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:232) | 232 | `...its recommendations are much better fitted to the query context` | `...its recommendations are better aligned with the query context` |

✅ Già segnalato in `paper_language_audit.md` #68.

### C12 — "which is in line with its preference for recommending popular items that perfectly match different gaming moods"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:237) | 237 | `...which is in line with its preference for recommending popular items that perfectly match different gaming moods.` | `...which aligns with its tendency to recommend popular items that match different gaming moods.` |

Prolisso + `perfectly` è overclaiming.

### C13 — "Non negligible fraction"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:843) | 843 | `A non negligible fraction of users` | `A non-negligible fraction of users` |

Manca il trattino.

### C14 — "along a spectrum of strictness and perspective"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:16) | 16 | `The five metrics are designed along a spectrum of strictness and perspective.` | `The five metrics span a spectrum from strict exact-match to relaxed partial-alignment.` |

`strictness and perspective` è vago.

### C15 — "Friction sits between the set-based and geometric approaches"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:16) | 16 | `Friction sits between the set-based and geometric approaches` | `Friction occupies an intermediate position between the set-based and geometric approaches` |

`sits between` è informale.

### C16 — "structurally saturate"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:44) | 44 | `...binary one-hot encodings make this measure structurally saturate` | `...binary one-hot encodings cause this measure to saturate structurally` |

Forzato.

### C17 — "context-aware benefits"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`06_conclusions.tex`](overleaf/06_conclusions.tex:8) | 8 | `...showing that context-aware benefits extend beyond accuracy.` | `...showing that the benefits of context-awareness extend beyond accuracy.` |

Ambiguo.

### C18 — "does not tell us whether the retrieved items fit the query context"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:27) | 27 | `but they do not tell us whether the retrieved items fit the query context` | `but they do not capture whether the retrieved items are contextually appropriate for the query situation` |

✅ Già segnalato in `paper_language_audit.md` — `tell us` è colloquiale.

### C19 — "model-agnostic, and computable without annotations"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:299) | 299 | `All metrics are bounded in $[0,1]$, model-agnostic, and computable without annotations beyond the contextual features already in the dataset.` | `All metrics are bounded in $[0,1]$, model-agnostic, and computable from only the contextual features present in the dataset, requiring no additional annotations.` |

Formulazione leggermente gobba.

### C20 — "diagnostic quantity rather than as an optimization target"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:44) | 44 | `...it should be interpreted as a diagnostic quantity rather than as an optimization target.` | `...it should be interpreted as a diagnostic indicator rather than an optimization target.` |

`quantity` è vago. `indicator` è più preciso.

---

## Categoria D: Hyphenation issues

### D1 — `context dependent` → `context-dependent`

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`00_main.tex`](overleaf/00_main.tex:239) | 239 | `makes the learned embeddings context dependent` | `makes the learned embeddings context-dependent` |

### D2 — `dataset dependent` → `dataset-dependent`

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:22) | 22 | `the benefit of contextual modeling is dataset dependent` | `the benefits of contextual modeling are dataset-dependent` |

### D3 — `Knowledge-Graph (KG)-conditioned` hyphenation

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:13) | 13 | `Knowledge-Graph (KG)-conditioned` | `knowledge graph (KG)-conditioned` |

Doppia hyphenation problematica. Inoltre `Knowledge-Graph` non va capitalizzato.

### D4 — `non-linear` (British) vs `nonlinear` (American)

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`03_model.tex`](overleaf/03_model.tex:68) | 68 | `nonlinear` | ✅ American English |
| [`03_model.tex`](overleaf/03_model.tex:90) | 90 (comm.) | `non-linear` | ⚠️ Solo in codice commentato |

---

## Categoria E: Grammatical inconsistencies

### E1 — `higher-order` vs `high-order` inconsistency

Già trattato in C2. Uniformare a `higher-order` in tutto il paper.

---

## Categoria F: Stray LaTeX / markup issues

### F1 — Massive commented-out code blocks

Tutti i file contengono ingenti blocchi di testo commentato:

| File | Linee approssimative |
|------|---------------------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:8-27) | 8–27 |
| [`02_related_work.tex`](overleaf/02_related_work.tex:33-100) | 33–100 |
| [`03_model.tex`](overleaf/03_model.tex:38-51,79-99) | 38–51, 79–99 |
| [`04_metrics.tex`](overleaf/04_metrics.tex:52-143, 186-231, 255-296, 298-309) | var. |
| [`05_experiments.tex`](overleaf/05_experiments.tex:34, 242-327, 460-489, 788-793, 847-858) | var. |
| [`06_conclusions.tex`](overleaf/06_conclusions.tex:12-22) | 12–22 |

### F2 — Unused `\textcolor` imports

| File | Linea | Codice |
|------|-------|--------|
| [`00_main.tex`](overleaf/00_main.tex:137) | 137 | `\usepackage[x11names,dvipsnames,table]{xcolor}` |

Da tenere perché serve a `colortbl` (l. 138).

### F3 — `\iffalse` environments senza `\fi` corrispondente

Come da A6: presente in [`04_metrics.tex:52`](overleaf/04_metrics.tex:52) e [`05_experiments.tex:450`](overleaf/05_experiments.tex:450). Sostituire con commenti `%` o eliminare.

---

# Pass 2 — Nuovi issue trovati (22)

## Categoria G: Errori di markup LaTeX

### G1 — Trailing comma in `\documentclass` options

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`00_main.tex`](overleaf/00_main.tex:48) | 48 | `\documentclass[natbib=false,sigconf,anonymous,review,screen,]{acmart}` | `\documentclass[natbib=false,sigconf,anonymous,review,screen]{acmart}` |

La virgola prima di `]{acmart}` è un residuo che alcuni parser LaTeX potrebbero segnalare come warning. Rimuovere.

🔴 **Priorità Alta** — potrebbe generare warning alla compilazione.

---

### G2 — Commented-out alternative titles dentro `\title{}`

| File | Linee | Problema |
|------|-------|----------|
| [`00_main.tex`](overleaf/00_main.tex:152) | 152–157 | Quattro linee di titoli alternativi commentati dentro il comando `\title{}` |

```latex
\title{Graph Neural Networks for Context-Aware Recommendations under Context-Sensitive
Evaluation Dimensions
%A Graph Neural Network Model and Offline Evaluation Metrics for Context-Aware Recommendations
% Graph Neural Networks for Context-Aware Recommendations under 
% %Novel 
% Context-Sensitive
% Evaluation Dimensions
}
```

Il codice è funzionale (i `%` commentano tutto), ma lascia residui di versioni precedenti. Pulire.

🟡 **Priorità Media**

---

### G3 — Inline `%judgment` comment che tronca la frase

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:233) | 233 | `Family~3 solves this by replacing the static relevance %judgment with context-weighted relevance` | `Family~3 solves this by replacing the static relevance judgment with context-weighted relevance` |

Il `%judgment` commenta la parola "judgment" e tutto ciò che segue sulla stessa linea. Il testo renderizzato è comunque grammaticale ("replacing the static relevance with context-weighted relevance"), ma:
1. La sorgente è disordinata
2. Se qualcuno sposta "with" alla linea successiva, la frase si rompe

Rimuovere il `%` o eliminare la parola "judgment" se non necessaria.

🟡 **Priorità Media**

---

### G4 — Inline `%collaborative` comment nell'abstract

| File | Linee | Testo originale |
|------|-------|----------------|
| [`00_main.tex`](overleaf/00_main.tex:242-243) | 242–243 | `...how strongly context interacts with the %collaborative \n user--item signal.` |

Il `%collaborative` commenta la parola "collaborative". Il rendering è corretto (il newline fornisce lo spazio), ma la sorgente è disordinata. Rimuovere il commento.

🟢 **Priorità Bassa**

---

### G5 — Stray `%\textcolor{red}{...}` comment nel titolo

| File | Linea | Testo |
|------|-------|-------|
| [`00_main.tex`](overleaf/00_main.tex:159) | 159 | `%\textcolor{red}{Designed/Dedicated/Purpose-Built/Situational/Sensitive}` |

Residuo di brainstorming sul nome del modello. Rimuovere.

🟢 **Priorità Bassa**

---

## Categoria H: Awkward phrasing aggiuntivi

### H1 — "conditioning them on situational factors" — antecedente ambiguo

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:9) | 9 | `...improve the relevance and personalization of recommendations by conditioning them on situational factors` | `...improve the relevance and personalization of recommendations by conditioning recommendations on situational factors` |

"them" ha antecedente ambiguo: si riferisce a "recommendations" ma "CARS" è il soggetto più vicino. Meglio ripetere "recommendations".

🟡 **Priorità Media**

---

### H2 — "as we said in Sec." — informale

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:204) | 204 | `as we said in Sec.~\ref{sec:experiments:methodology}` | `as described in Sec.~\ref{sec:experiments:methodology}` o `as noted in Sec.~\ref{sec:experiments:methodology}` |

✅ Già segnalato in `paper_language_audit.md` #57.

🟡 **Priorità Media**

---

### H3 — "ranking discrimination" — scelta lessicale

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|------------|
| [`03_model.tex`](overleaf/03_model.tex:120) | 120 | `This ensures that ranking discrimination accounts for contextual appropriateness` | `This ensures that ranking differentiation accounts for contextual appropriateness` |

"discrimination" in inglese ha connotazioni negative (discriminazione). In contesti ML/IR, "discrimination" è tecnicamente corretto (capacità di discriminare tra item) ma può essere frainteso da revisori non madrelingua del settore. "Differentiation" è più sicuro.

🟡 **Priorità Media**

---

### H4 — "ACC is marginally below AFM and DeepFM~(0.0023 vs.\ 0.0026), a direct consequence of all models on this dataset for which exact full-context matches are still quite infrequent"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:228) | 228 | `ACC is marginally below AFM and DeepFM~(0.0023 vs.\ 0.0026), a direct consequence of all models on this dataset for which exact full-context matches are still quite infrequent.` | `ACC is marginally below AFM and DeepFM (0.0023 vs.\ 0.0026), reflecting that exact full-context matches remain rare for all models on this dataset.` |

La frase originale è sintatticamente contorta: "a direct consequence of all models on this dataset for which..."

🟡 **Priorità Media**

---

### H5 — "suggesting that session duration is most informative only when paired with additional situational context"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:650) | 650 | `suggesting that session duration is most informative only when paired with additional situational context such as gaming mood.` | `suggesting that session duration is informative only when paired with additional situational context such as gaming mood.` |

"most informative only when" è logicamente contraddittorio (il superlativo "most" + "only" crea tensione). Rimuovere "most".

🟢 **Priorità Bassa**

---

### H6 — "the proposed metrics confirm stronger contextual alignment as well"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:240) | 240 | `the proposed metrics confirm stronger contextual alignment as well.` | `the proposed metrics also confirm stronger contextual alignment.` |

"as well" a fine frase è meno idiomatico di "also" prima del verbo in AmE.

🟢 **Priorità Bassa**

---

## Categoria I: Inconsistenze e refusi

### I1 — Yelp feature count inconsistency (11 vs 12)

| File | Linea | Problem |
|------|-------|---------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:19) | 19 | `11 contextual features` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:543) | 543 | `twelve contextual features` |

✅ Già ampiamente segnalato in `paper_language_audit.md` #41, #69, #79, #109.

🔴 **Priorità Alta**

---

### I2 — Yelp feature group naming inconsistency

| File | Sezione | Gruppi usati |
|------|---------|-------------|
| [`05_experiments.tex:19`](overleaf/05_experiments.tex:19) | 5.1 (descrizione dataset) | temporal, social and user, spatial |
| [`05_experiments.tex:543`](overleaf/05_experiments.tex:543) | 5.5.1 (ablation) | Temporal, Location, Atmosphere |

✅ Già segnalato in `paper_language_audit.md` #70.

🔴 **Priorità Alta**

---

### I3 — WCS = CS identici per BGG in Table 5

| File | Linee | Problema |
|------|-------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:435-445) | 435–445 | WCS e CS hanno valori identici per tutti i modelli su BGG |

Se è atteso (feature binarie con pesatura uniforme), va spiegato brevemente. Se è un bug, va corretto.

✅ Già segnalato in `paper_language_audit.md` #11.

🟡 **Priorità Media**

---

### I4 — "have each similar cardinality" — grammar

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:235) | 235 | `the three feature groups (Playtime, Mood, Social) have each similar cardinality` | `the three feature groups (Playtime, Mood, Social) have similar cardinalities` |

✅ Già segnalato in `paper_language_audit.md` #71.

🟡 **Priorità Media**

---

### I5 — "and thus implying" — grammar

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:234) | 234 | `and thus implying representational capacity restriction` | `which implies a representational capacity restriction` |

✅ Già segnalato in `paper_language_audit.md` #70.

🟡 **Priorità Media**

---

### I6 — "for all the cases" → "in all cases"

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:225) | 225 | `for all the cases` | `in all cases` |

✅ Già segnalato in `paper_language_audit.md` #65.

🟢 **Priorità Bassa**

---

## Categoria J: Correzioni a report precedenti

### J1 — Riferimento di linea errato in A6 (Pass 1)

| Issue | Dove | Errore | Correzione |
|-------|------|--------|------------|
| A6 | `output/paper_proofreading_analysis.md` | Indicava `04_metrics.tex:450–456` per un blocco `\iffalse` | Il file [`04_metrics.tex`](overleaf/04_metrics.tex) termina alla linea **311**. Quel riferimento non esiste. |

**Da rimuovere dal report precedente.**

🟢 **Priorità Bassa** (non impatta il paper, solo la correttezza del report)

---

### J2 — `\iffalse` in `05_experiments.tex:450` ha `\fi` corrispondente

| Issue | Dove | Linee | Stato |
|-------|------|-------|-------|
| A6/F3 | [`05_experiments.tex`](overleaf/05_experiments.tex:450) | 450–456 | ✅ Il `\fi` è presente a linea 456 |

Nell'analisi originale non era chiaro se il `\fi` fosse presente. È presente. Nessuna azione necessaria.

🟢 Solo nota informativa.

---

## Categoria K: Pulizia commenti residui

### K1 — Commenti editoriali "Iván:" / "Alejandro:" sparsi

Oltre ai `\textcolor{red/blue}` già segnalati in A7, ci sono commenti con nomi dei revisori:

| File | Linea | Testo |
|------|-------|-------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:13) | 13 | `%\textcolor{blue}{I explained this acronym, not sure if it is correct}` |
| [`02_related_work.tex`](overleaf/02_related_work.tex:30) | 30 | `%\textcolor{blue}{it may be strange to only point out Section 4}` |
| [`02_related_work.tex`](overleaf/02_related_work.tex:42) | 42 (comm.) | `\textcolor{red}{Iván: I have changed this subsection...}` |
| [`04_metrics.tex`](overleaf/04_metrics.tex:7) | 7 (comm.) | `%\textcolor{blue}{some introduction for the need...}` |

🔴 **Priorità Alta** — In anonymous submission, nomi di autori/revisori nei commenti violano il double-blind.

---

### K2 — Commenti di discussione interna in `02_related_work.tex`

| File | Linee | Contenuto |
|------|-------|-----------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:24) | 24 | `% Together, these` con commento `\textcolor{blue}{I don't understand this sentence: '3 contrasts'}` |

Rimuovere prima della submission.

🔴 **Priorità Alta**

---

### K3 — Commenti su tabelle in `05_experiments.tex`

| File | Linea | Testo |
|------|-------|-------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:88) | 88 | `%\textcolor{blue}{proposal for tables: lightccf should be after pop...}` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:90) | 90 | `%\textcolor{blue}{how important is to report AUC? can we remove it?}` |

Residui di discussioni sull'ordinamento delle tabelle. Rimuovere.

🟡 **Priorità Media**

---

## Riepilogo statistico

| Categoria | Conteggio | Priorità |
|-----------|-----------|----------|
| **A** — Errori tipografici/formattazione | 7 | 🔴 Alta (alcuni rompono il rendering) |
| **B** — AmE vs BrE | 3 | 🟡 Media |
| **C** — Awkward phrasing | 20 | 🟡 Media |
| **D** — Hyphenation | 4 | 🟢 Bassa |
| **E** — Grammatical inconsistencies | 1 | 🟢 Bassa |
| **F** — Stray LaTeX/markup | 3 | 🟡 Media |
| **G** — Errori markup LaTeX (nuovi) | 5 | 🔴 Alta |
| **H** — Awkward phrasing (nuovi) | 6 | 🟡 Media |
| **I** — Inconsistenze (nuovi) | 6 | 🔴 Alta |
| **J** — Correzioni a report | 2 | 🟢 Bassa |
| **K** — Commenti residui (nuovi) | 3 | 🔴 Alta |
| **Totale** | **60** | — |

### Priorità di intervento

1. 🔴 **Rendering/crash**: G1 (trailing comma), A2 (NFM stray number)
2. 🔴 **Double-blind violation**: K1, K2 (nomi nei commenti)
3. 🔴 **Consistenza dati**: I1, I2 (Yelp feature count/groups)
4. 🟡 **Chiarezza espositiva**: C1–C20, H1–H6 (phrasing)
5. 🟡 **Pulizia codice**: A6, A7, F1–F3, G2–G5, K3 (commenti)
6. 🟢 **AmE consistency**: B1–B3, D1–D4

### Riferimenti incrociati

Questo report è complementare a [`output/paper_language_audit.md`](output/paper_language_audit.md), che contiene ulteriori ~116 issue focalizzati su:
- Consistenza tra sezioni (feature counts, group names)
- Overclaiming e calibrazione delle affermazioni
- Struttura argomentativa e tono
- Qualità delle referenze bibliografiche
- Formule matematiche e notazione

**Raccomandazione:** utilizzare entrambi i report in parallelo durante la revisione finale.

---

*Report generato il 2026-05-24. Lingua target: American English.*
