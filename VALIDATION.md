# Validation summary

This file summarises how the skill was evaluated before release, and what the results do and do not show. The full method and results, including the per-paper data, will be in the preprint. The figures here were measured between September and October 2026, on skill versions 0.8.x to 0.9.2, as noted for each test. Test papers are not named.

## 1. What counts as truth

No review of a real paper has a complete answer key. So the evaluation uses four kinds of truth, each with a known weakness:

| Truth | How it is built | Weakness |
|---|---|---|
| **Planted defects** | known errors inserted into papers rebuilt from their LaTeX source, with the key written before any run | complete by construction, but the plants are cleaner and easier to find than real errors |
| **Known errors** | objective errors raised by any of three independent Opus runs, each confirmed against the page (value, contradiction, arithmetic) by a separate checking model | limited to what at least one run found; a run is scored leave-one-out against the other two |
| **Consensus problems** | problems found by all three (C) or by two (D) independent runs, after a check against the paper | built from Opus runs, so they favour an Opus-like reading |
| **Checked claims** | every objective claim in a findings list, judged confirmed, false or unverifiable against the page by a checking model | the checker can be wrong, and is the same model family |

Checkers and scorers are Opus sub-agents working from written briefs. Human adjudication of a sample of checks and scores will be reported shortly in a preprint. Until then, every figure below is an internal, model-graded estimate.

## 2. Recall

### Planted defects (skill 0.9.0, Opus 5.5, October 2026)

- **The papers:** four public arXiv papers with LaTeX sources, chosen to differ:
  - one single-column with tables, published after the model's training cutoff;
  - one figure-only;
  - one two-column and heavy on equations;
  - one two-column and heavy on tables.
- **The copies:** each paper was rebuilt as two planted copies with six defects each, and one unmodified control: 12 files under random names, 48 plants. The plants were:
  - by severity: 8 substantive, 26 moderate, 14 minor;
  - by kind: 15 text against a figure, 14 calculations and equations, 14 claims against the paper's own evidence, 5 text against text, a table or a caption.
- **The runs:** 24, two per file, each a fresh Opus sub-agent with only its PDF; no web, no memory.
- **The scoring:** two independent scorers agreed on all 96 run-plant pairs.

| Measure | Result |
|---|---|
| Recall per run (partial = 0.5) | 96.4% (95% CI 91.7–99.5) |
| Recall over two runs | 97.9% (47 of 48) |
| Substantive / moderate / minor, per run | 100% / 97% / 93% |
| By kind: calculations, text vs text, claims vs evidence, text vs figure | 100%, 100%, 98%, 90% |
| New findings beyond the plants on planted copies | 24: 22 valid, 2 plausible, 0 false |

Both plants never found need a value read off a figure. The paper published after the training cutoff scored 100% in all four runs, so the result does not rest on memory of the papers. Runs often graded a plant's severity differently from the key.

### Known errors and consensus problems in 30 preprints (skill 0.9.0, Opus 5.5)

The 30 preprints are the latest posted on four preprint servers as of 1 October 2026, taken regardless of topic. Each was run three times; each run is scored against the reference set built from the other two.

| Measure | Result |
|---|---|
| Known errors found per run (319) | 84.3% |
| Consensus problems found per run (874) | 87.2% |
| Findings per run | 21.8 |
| Fabricated quotations | none |

## 3. Precision

### Claim checking (skill 0.9.0 findings, verified under 0.9.2 rules, October 2026)

There were 115 Opus runs on papers in several states: preprints, accepted manuscripts and published versions, including pairs and series of versions of the same paper. Every objective claim in them was checked against the page.

| | Without claim verification | With claim verification (0.9.2) |
|---|---|---|
| Real errors raised (1,296) stated as fact | 100% | 92.9% |
| Real errors softened to a question or outside-knowledge label | 0 | 6.6% (they still reach the author) |
| Real errors removed | 0 | **0** |
| False claims stated as fact, per 10 runs | 16.6 | 9.9 |
| **Share of claims stated as fact that are false** | 12.8% | **8.6%** |
| Claims the checker could not settle, shown as a question or labelled | 0 | 75% |

**Why verification never removes a claim.** An earlier design (0.9.1) removed claims the verifier doubted. On the same runs it removed false claims about six times as often as real ones, but each real error it removed was lost to the author for good, while each false one left in costs the author seconds to dismiss. 0.9.2 turns a doubted claim into a question that cites the evidence, and removes nothing.

### Quotation integrity (skill 0.8.x to 0.9.0)

Every flagged quotation was checked against the rendered page. Under strict scoring, no Claude Opus or Sonnet run has produced a fabricated quotation:
- in the early development tracks: 44 runs and 939 findings, including 11 documents chosen for their layout from nine typesetting engines;
- in the 30-preprint set;
- in the claim-checked runs.

In a three-model comparison in one harness (Opus, Grok and GPT, 351 findings), none was found either. For other models, see §4.

## 4. Models and harnesses (skill 0.9.0, 10 of the 30 preprints, one run per model)

These are the same papers, scored the same way as Opus, against reference sets built from three Opus runs.

| Model | Harness | Known errors (127) | C + D (325) | Findings per run | False findings | Reports with a false sentence | Fabricated quotations |
|---|---|---|---|---|---|---|---|
| Claude Opus 5.5 (leave-one-out) | Claude app | 85.5% | 88.5% | about 22 | about 0.6% | – | 0 |
| Claude Sonnet 5.5 | Claude app | 71.7% | 80.8% | 24.5 | 1 of 245 | 2 of 10 | 0 |
| Gemini 4 Argon (effort not selectable) | Gemini app | 61.4% | 55.4% | 10.4 | 31 of 104 | 10 of 10 | 6 |
| GPT-6.1 Sol (effort not selectable) | Microsoft 365 Copilot | 52.8% | 65.4% | 24.0 | 3 of 240 | 3 of 10 | 0 |
| Grok 4.7 (high) | Cursor | 52.0% | 55.2% | 13.4 | 8 of 134 | 8 of 10 | 0 |
| Gemini 3.8 Flash (high) | Antigravity | 44.9% | 37.2% | 13.3 | 8 of 133 | 9 of 10 | 0 |
| GPT-5.6 Sol (high) | Cursor | 33.1% | 46.8% | 13.3 | 3 of 133 | 2 of 10 | 0 |
| GPT-6 Luna | GitHub Copilot | 18.5% | 22.0% | 8.2 | 2 of 82 | 5 of 10 | 0 |
| Claude Haiku 4.5 | Claude app | 3.1% | 13.8% | 12.7 | 34 of 127 | 10 of 10 | 1 |

**Harness effects, measured separately:**
- Opus in the Claude app against Opus in Cowork: known errors 81.1% against 83.0% on the same papers, within run-to-run variation.
- Sonnet in Cursor against Sonnet in the Claude app, on five papers: 83.8% against 79.6% known errors.

**Patterns the scorers saw:**
- The weaker models miss figure-reading errors most.
- The models with many false findings mostly misread the page: symbols lost in text extraction reported as typos, and values misread from figures and tables.

## 5. The 1.0.0 release build (October 2026)

1.0.0 is 0.9.2 with features removed: journal compliance, text-overlap checks, research-assessment readiness, and the field packs then in development. The review pipeline is unchanged. A regression check ran 1.0.0 (Opus sub-agents, single-context verification):
- on 3 of the 30 preprints;
- on three versions of a fourth paper (draft, revision with a response file, published version).

| Check | Result |
|---|---|
| Known errors, 3 preprints | 85.9% (0.9.0: 85.5%) |
| Consensus problems, 3 preprints | 86.1% |
| False findings | 0 of 73 on the preprints; 0 to 1 per run on the fourth paper |
| Fabricated quotations | none |
| Substantive and moderate errors on the fourth paper | all found in 3 of 4 runs; one moderate error missed once |
| Minor equation typos on the fourth paper | fewer than the earlier 0.9.0 runs on its draft and revision, more on its published version |
| Revision round | 18 of 18 earlier findings carried with a status; the declined finding not raised; the claimed change checked against the revised text |
| Removed features | absent from every output; a request for one is answered once as out of scope |

## 6. What this does not show

- **Truth is model-built.** The same model family that reviews also checks and scores. Human adjudication will be reported shortly in a preprint.
- **Recall is bounded by what some run found.** Known-error recall cannot count errors every run missed. Only the planted-defect test has a complete key, and its defects are easier than real ones.
- **One run per model** in the comparison, with model, harness and effort mixed.
- **Field coverage.** The preprints are broad, but most test papers are in materials science, chemistry and physics.
- **No test of significance or novelty judgement.** These are the parts of a review where a specialist referee matters most, and the skill makes no claim on them beyond raising questions.
