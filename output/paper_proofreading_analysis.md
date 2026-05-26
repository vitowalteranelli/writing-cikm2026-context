# Paper Proofreading & American English Alignment Report

**Target:** Best Paper Award @ CIKM 2026  
**Analysis scope:** Typographical errors, awkward phrasing, American English disallineamenti  
**File analyzed:** [`overleaf/`](overleaf/) (all `.tex` sources)

---

## Indice

1. [Categoria A: Errori tipografici e di formattazione](#categoria-a-errori-tipografici-e-di-formattazione)
2. [Categoria B: American English vs British English disallineamenti](#categoria-b-american-english-vs-british-english-disallineamenti)
3. [Categoria C: Awkward / unclear phrasing](#categoria-c-awkward--unclear-phrasing)
4. [Categoria D: Hyphenation issues](#categoria-d-hyphenation-issues)
5. [Categoria E: Tense / agreement / grammatical inconsistencies](#categoria-e-tense--agreement--grammatical-inconsistencies)
6. [Categoria F: Stray LaTeX / markup issues](#categoria-f-stray-latex--markup-issues)
7. [Riepilogo statistico](#riepilogo-statistico)

---

## Categoria A: Errori tipografici e di formattazione

### A1 — Extra space before comma

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:27) | 27 | `FM-based models , all trained` | `FM-based models, all trained` |

Rimuovere lo spazio prima della virgola.

---

### A2 — Stray/unparsed number in table cell

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:156) | 156 | `NFM 0.2549 & 0.0312 & 0.0224 & 0.0069 & 0.0607 \\` | `NFM & 0.0312 & 0.0224 & 0.0069 & 0.0607 \\` |

Il numero `0.2549` è un residuo spurio che rompe l'allineamento della tabella. Va rimosso.

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

Manca il punto fermo alla fine della frase (prima della linea successiva).

---

### A5 — Redundant space before non-breaking space tilde

| File | Linea | Testo originale | Correzione proposta |
|------|-------|----------------|---------------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:49) | 49 | `Eq. ~\ref{eq:score}` | `Eq.~\ref{eq:score}` |

Lo spazio prima della tilde (`~`) è ridondante: la tilde stessa è un non-breaking space in LaTeX. Lo spazio extra può causare spaziatura anomala nell'output.

---

### A6 — Commented-out content with stray text references

Nel file [`04_metrics.tex`](overleaf/04_metrics.tex:52) è presente un blocco `\iffalse...\fi` (ll. 52–59) e un altro blocco `\iffalse` (l. 450) senza il corrispondente `\fi`. Non è un errore tecnico (LaTeX tollera `\iffalse` annidati), ma è disordine.

| File | Linee | Note |
|------|-------|------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:52) | 52–59 | Blocco `\iffalse` annidato |
| [`04_metrics.tex`](overleaf/04_metrics.tex:450) | 450–456 | Secondo blocco `\iffalse` |
| [`05_experiments.tex`](overleaf/05_experiments.tex:450) | 450–456 | `\iffalse` environment per `tablenotes` |

Si consiglia pulizia: eliminare i blocchi commentati non più necessari.

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

## Categoria B: American English vs British English disallineamenti

Il paper è complessivamente in American English, ma ci sono alcune oscillazioni.

### B1 — `nonlinear` vs `non-linear`

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`03_model.tex`](overleaf/03_model.tex:68) | 68 | `No nonlinear activations...` | ✅ American English (`nonlinear`) |
| [`03_model.tex`](overleaf/03_model.tex:90) | 90 (commentata) | `no non-linear activation` | ❌ British English (`non-linear`) |

La linea 90 è commentata, quindi nessun impatto sull'output. Da notare solo per consistenza futura.

### B2 — `over-smoothing` (hyphenated)

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`03_model.tex`](overleaf/03_model.tex:76) | 76 | `over-smoothing` | ❌ American English preferisce `oversmoothing` (non composto) |
| [`03_model.tex`](overleaf/03_model.tex:126) | 126 | `over-smoothing` | ❌ Idem |

In American English, quando un prefisso si salda alla parola base senza ambiguità, non va sillabato. `oversmoothing` è la forma preferita. Tuttavia `over-smoothing` è accettabile; la cosa più importante è la **consistenza**.

### B3 — `well-suited` (hyphenated)

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:13) | 13 | `well-suited` | ⚠️ American English: `well suited` (non predicativo) o `well-suited` (attributivo). In posizione predicativa ("are well suited"), la forma senza trattino è preferita in AmE. |

---

## Categoria C: Awkward / unclear phrasing

### C1 — "This capability provides important benefits"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:10) | 10 | `This capability provides important benefits, including greater adaptability to real-world scenarios and increased user satisfaction.` | `This makes recommendations more adaptable to real-world scenarios and increases user satisfaction.` |

"Provides important benefits" è tautologico (ogni capability fornisce benefits). Meglio un costrutto diretto.

---

### C2 — "high-order connectivity patterns" / "high-order collaborative structure"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:13) | 13 | `high-order collaborative structure` | `higher-order collaborative structure` |
| [`01_introduction.tex`](overleaf/01_introduction.tex:14) | 14 | `high-order connectivity patterns` | `higher-order connectivity patterns` |

Il paper usa sia `high-order` (ll. 13, 14) che `higher-order` (l. 76 `03_model.tex`, l. 32 `05_experiments.tex`). **Inconsistenza**: `higher-order` è la forma standard in ML/AI literature. Uniformare a `higher-order`.

---

### C3 — "propagation itself"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:14) | 14 | `...incorporate it in ways that do not affect propagation itself.` | `...ways that do not affect propagation.` |

`itself` è filler che non aggiunge informazione. Più conciso senza.

---

### C4 — "Together, the model and the metrics provide a consistent view of context-aware recommendation: one for learning, the other for evaluation."

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:19) | 19 | `Together, the model and the metrics provide a consistent view of context-aware recommendation: one for learning, the other for evaluation.` | `Together, the model and the metrics provide a consistent view of context-aware recommendation—the former for learning, the latter for evaluation.` |

Il costrutto "one for learning, the other for evaluation" è ambiguo: non è immediato quale si riferisca a cosa. Meglio "the former / the latter".

---

### C5 — "the benefit of contextual modeling is dataset dependent"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:22) | 22 | `the benefit of contextual modeling is dataset dependent` | `the benefits of contextual modeling are dataset-dependent` |

(1) `benefit` → `benefits` (concordanza plurale con il verbo "are" nella frase completa).  
(2) `dataset dependent` → `dataset-dependent` (compound adjective).  
(3) Verifica: la frase dice "is dataset dependent" ma poi "it becomes more nuanced" — meglio uniformare.

---

### C6 — "shallow side channels"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:10) | 10 | `...they are often incorporated as auxiliary features, shallow side channels, or post-hoc re-ranking signals...` | `...they are often incorporated as auxiliary features, shallow side-channel signals, or post-hoc re-ranking adjustments...` |

`shallow side channels` è una metafora vaga. In un paper per best paper award, ogni termine deve essere preciso.

---

### C7 — "relatively little architectural overhead"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:13) | 13 | `...model high-order collaborative structure with relatively little architectural overhead.` | `...model higher-order collaborative structure with low architectural overhead.` |

`relatively little` è colloquiale. `low` è più diretto e formale.

---

### C8 — "gets better or comparable with other competitors"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:221) | 221 | `Across all three datasets, \modelname{} gets better or comparable with other competitors on most of the context-aware metrics` | `Across all three datasets, \modelname{} performs favorably against competitors on most context-aware metrics` |

(1) `gets better` è colloquiale. (2) `comparable with` → `comparable to` in AmE. (3) `other competitors` è ridondante.

---

### C9 — "evidencing context-gated message passing is able to capture"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:225) | 225 | `...evidencing context-gated message passing is able to capture...` | `...demonstrating that context-gated message passing captures...` |

`evidencing` come verbo è atipico e percepito come British/legalese. `demonstrating` è più chiaro. Inoltre `is able to capture` → `captures` (più diretto).

---

### C10 — "the best concordance"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:227) | 227 | `...achieving the best concordance on the Environment group` | `...achieving the best alignment on the Environment group` |

`concordance` in questo contesto è inusuale. `alignment` è il termine standard per questo tipo di metrica.

---

### C11 — "much better fitted to the query context"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:232) | 232 | `...its recommendations are much better fitted to the query context` | `...its recommendations are better aligned with the query context` |

`fitted to` è grammaticalmente corretto ma `aligned with` è più idiomatico nel contesto ML/IR.

---

### C12 — "which is in line with its preference for recommending popular items that perfectly match different gaming moods"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:237) | 237 | `...which is in line with its preference for recommending popular items that perfectly match different gaming moods.` | `...which aligns with its tendency to recommend popular items that match different gaming moods.` |

`in line with its preference for recommending` è prolisso. Inoltre `perfectly` è overclaiming.

---

### C13 — "Non negligible fraction"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:843) | 843 | `A non negligible fraction of users` | `A non-negligible fraction of users` |

Manca il trattino in `non-negligible`. Inoltre, in AmE, `nonnegligible` (senza trattino) è la forma più compatta, ma `non-negligible` è più comune.

---

### C14 — "along a spectrum of strictness and perspective"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:16) | 16 | `The five metrics are designed along a spectrum of strictness and perspective.` | `The five metrics span a spectrum from strict exact-match to relaxed partial-alignment.` |

`strictness and perspective` è vago. Meglio descrivere gli estremi dello spettro.

---

### C15 — "Friction sits between the set-based and geometric approaches"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:16) | 16 | `Friction sits between the set-based and geometric approaches` | `Friction occupies an intermediate position between the set-based and geometric approaches` |

`sits between` è informale.

---

### C16 — "structurally saturate"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:44) | 44 | `...binary one-hot encodings make this measure structurally saturate` | `...binary one-hot encodings cause this measure to saturate structurally` |

`structurally saturate` è un po' forzato. Riformulare per chiarezza.

---

### C17 — "context-aware benefits"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`06_conclusions.tex`](overleaf/06_conclusions.tex:8) | 8 | `...showing that context-aware benefits extend beyond accuracy.` | `...showing that the benefits of context-awareness extend beyond accuracy.` |

`context-aware benefits` è ambiguo: sono i benefici dell'essere context-aware, non benefici che sono a loro volta context-aware.

---

### C18 — "does not tell us whether the retrieved items fit the query context"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:27) | 27 | `but they do not tell us whether the retrieved items fit the query context` | `but they do not capture whether the retrieved items are contextually appropriate for the query situation` |

`tell us` è colloquiale per un paper accademico. Meglio `capture` o `indicate`.

---

### C19 — "Model-agnostic, and computable without annotations"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:299) | 299 | `All metrics are bounded in $[0,1]$, model-agnostic, and computable without annotations beyond the contextual features already in the dataset.` | `All metrics are bounded in $[0,1]$, model-agnostic, and computable from only the contextual features present in the dataset, requiring no additional annotations.` |

La formulazione originale è grammaticalmente corretta ma leggermente gobba. La proposta separa meglio i concetti.

---

### C20 — "should be interpreted as a diagnostic quantity rather than as an optimization target"

| File | Linea | Testo originale | Proposta |
|------|-------|----------------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:44) | 44 | `...it should be interpreted as a diagnostic quantity rather than as an optimization target.` | `...it should be interpreted as a diagnostic indicator rather than an optimization target.` |

`quantity` è vago. `indicator` è più preciso.

---

## Categoria D: Hyphenation issues (compound adjectives)

### D1 — `context dependent` → `context-dependent`

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`00_main.tex`](overleaf/00_main.tex:239) | 239 | `makes the learned embeddings context dependent` | `makes the learned embeddings context-dependent` |

---

### D2 — `dataset dependent` → `dataset-dependent`

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:22) | 22 | `the benefit of contextual modeling is dataset dependent` | `the benefits of contextual modeling are dataset-dependent` |

---

### D3 — `Knowledge-Graph (KG)-conditioned` hyphenation

| File | Linea | Testo originale | Correzione |
|------|-------|----------------|------------|
| [`02_related_work.tex`](overleaf/02_related_work.tex:13) | 13 | `Knowledge-Graph (KG)-conditioned` | `knowledge graph (KG)-conditioned` |

Doppia hyphenation problematica. Inoltre `Knowledge-Graph` non va capitalizzato se non come nome proprio.

---

### D4 — `non-linear` (British) vs `nonlinear` (American)

| File | Linea | Uso | Giudizio |
|------|-------|-----|----------|
| [`03_model.tex`](overleaf/03_model.tex:68) | 68 | `nonlinear` | ✅ American English |
| [`03_model.tex`](overleaf/03_model.tex:90) | 90 (comm.) | `non-linear` | ⚠️ Solo in codice commentato |

---

## Categoria E: Tense / agreement / grammatical inconsistencies

### E1 — Missing subject-verb agreement

| File | Linea | Testo | Correzione |
|------|-------|-------|------------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:227) | 227 | `shows \modelname{} achieving the best concordance on the Environment group (0.4346), which contains the highest-cardinality features...` | OK grammaticalmente. Nessun errore. |

### E2 — Tense shift in same paragraph

| File | Linea | Testo | Note |
|------|-------|-------|------|
| [`05_experiments.tex`](overleaf/05_experiments.tex:225-227) | 225-227 | `evidencing ... is able to capture ... The WCS analysis ... shows ... achieving ...` | Presente coerente. OK. |

### E3 — `higher-order` vs `high-order` inconsistency

Come da C2. Nel resto del paper (es. [`05_experiments.tex`](overleaf/05_experiments.tex:32) l. 32) si usa `higher-order`. Le occorrenze in [`01_introduction.tex`](overleaf/01_introduction.tex:13-14) usano `high-order`. **Uniformare a `higher-order`** in tutto il paper.

---

## Categoria F: Stray LaTeX / markup issues

### F1 — Massive commented-out code blocks

Tutti i file contengono ingenti blocchi di testo commentato (precedenti版本). Questo è normale in fase di revisione ma va ripulito prima della submission. Segnalo i più estesi:

| File | Linee approssimative | Contenuto |
|------|---------------------|-----------|
| [`01_introduction.tex`](overleaf/01_introduction.tex:8-27) | 8-27 | Vecchie versioni del paragrafo |
| [`02_related_work.tex`](overleaf/02_related_work.tex:33-100) | 33-100 | Vecchie subsection intere |
| [`03_model.tex`](overleaf/03_model.tex:38-51,79-99) | 38-51, 79-99 | Vecchie versioni delle equazioni |
| [`04_metrics.tex`](overleaf/04_metrics.tex:52-143, 186-231, 255-296, 298-309) | 52-143, 186-231, 255-296, 298-309 | Grandi blocchi di vecchia versione |
| [`05_experiments.tex`](overleaf/05_experiments.tex:34, 242-327, 460-489, 788-793, 847-858) | var. | Vecchie tabelle e commenti |
| [`06_conclusions.tex`](overleaf/06_conclusions.tex:12-22) | 12-22 | Vecchia versione delle conclusioni |

---

### F2 — `\iffalse` environments without closing `\fi` in active code

| File | Linea | Problema |
|------|-------|----------|
| [`04_metrics.tex`](overleaf/04_metrics.tex:52) | 52 | `\iffalse` annidato (l. 52) con contenuto fino a l. 59. Tecnicamente funziona ma è fragile. |
| [`04_metrics.tex`](overleaf/04_metrics.tex:450) | 450 | `\iffalse` per tablenotes (fino a l. 456). OK. |
| [`05_experiments.tex`](overleaf/05_experiments.tex:450) | 450 | `\iffalse` environment. OK ma da verificare che `\fi` sia presente. |

Si consiglia di sostituire questi blocchi con semplici commenti `%` o eliminarli.

---

### F3 — Unused `\textcolor` imports

| File | Linea | Codice |
|------|-------|--------|
| [`00_main.tex`](overleaf/00_main.tex:137) | 137 | `\usepackage[x11names,dvipsnames,table]{xcolor}` |

`xcolor` è caricato ma al momento non ci sono `\textcolor{...}` attivi (sono tutti commentati). Se si rimuovono tutti i commenti colorati, la dependency diventa superflua. Tuttavia `colortbl` (l. 138) usa `xcolor`, quindi va tenuto.

---

## Riepilogo statistico

| Categoria | Conteggio | Priorità |
|-----------|-----------|----------|
| **A** — Errori tipografici/formattazione | 7 | 🔴 Alta (alcuni rompono il rendering) |
| **B** — AmE vs BrE disallineamenti | 3 | 🟡 Media |
| **C** — Awkward / unclear phrasing | 20 | 🟡 Media |
| **D** — Hyphenation issues | 4 | 🟢 Bassa |
| **E** — Grammatical inconsistencies | 1 | 🟢 Bassa |
| **F** — Stray LaTeX/markup | 3 | 🟡 Media |
| **Totale** | **38** | — |

**Priorità di intervento:**
1. 🔴 **A1, A2, A3, A4, A5** — problemi di rendering o formattazione visibile
2. 🟡 **C1–C20** — chiarezza espositiva (critico per Best Paper)
3. 🟡 **F1–F3** — pulizia del codice LaTeX
4. 🟡 **B1–B3, D1–D4, E1** — consistenza stilistica

---

*Analysis generated on 2026-05-24. Language: American English target.*
