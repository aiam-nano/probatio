# Probatio

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23540017.svg)](https://doi.org/10.5281/zenodo.23540017)

*Latin: a testing, a proof.* An agent skill that reviews your own scientific manuscript before the referees do.

Give it the PDF of a draft. You get two documents:
- **a prose report** naming the problems a referee would raise, each anchored to a quotation from your manuscript, each with a concrete fix, ordered by what would most change a referee's verdict;
- **a complete findings list**, one entry per problem.

When you revise, run it again with the findings list and a note of what you changed. It checks what was addressed before looking for anything new.

The skill is a folder of plain-text instructions in the open Agent Skills format (`SKILL.md`). It runs in the Claude app, Claude Code, Cowork, Cursor, GitHub Copilot, the Gemini app and other agents that read that format. Its skill id is `manuscript-review`.

**Version 1.0.0**, released for public testing. **MIT licence.** A preprint describing the skill and its full evaluation is in preparation, and this README will link it.

---

## Contents

- [What it does](#what-it-does)
- [Install](#install)
- [Use](#use)
- [Which model to use](#which-model-to-use)
- [How well it works](#how-well-it-works)
- [How a review runs](#how-a-review-runs)
- [What it does not do](#what-it-does-not-do)
- [Your manuscript and your data](#your-manuscript-and-your-data)
- [Field packs](#field-packs)
- [Feedback](#feedback)
- [Design decisions](#design-decisions)
- [Sources and credits](#sources-and-credits)
- [Licence and citation](#licence-and-citation)

---

## What it does

It reads the manuscript the way a careful referee does, and then checks its own work before handing it over.

**What it finds.** It finds what an author most needs to hear before submission:
- claims the paper's own evidence does not support;
- numbers that disagree between the abstract, text, tables, figures and supplementary information;
- arithmetic that does not add up;
- methods described too thinly to reproduce;
- missing controls and statistics;
- figure and caption errors;
- and the slips that make a referee trust everything else less.

**Every finding is anchored.** Each carries a verbatim quotation and its location. No quotation, no finding. Each also carries a severity, a concrete fix, and a statement of what would have to be true for the finding to be wrong.

**Every factual claim is checked before you see it.** A claim verification stage re-reads each finding against the whole manuscript:
- quotations are confirmed on the page;
- arithmetic is recomputed;
- figures are re-rendered.

Where the platform allows, a fresh model context that did not write the findings does this. A claim the paper cannot settle reaches you as a question citing the evidence, not as an assertion. A claim resting on outside knowledge is labelled as such. Nothing is deleted at this stage, because a real error removed by an over-cautious checker is one you would never see.

**It is iterative.** A manuscript goes through several rounds. In round 2 and later:
- every earlier finding is carried forward with a status: addressed, partially addressed, not addressed, declined, or no longer applicable;
- a claimed change is checked against the revised text, not taken on trust;
- a finding you decline is closed for good.

---

## Install

The skill is the `manuscript-review/` folder. Download `manuscript-review-1.0.0.zip` from the [latest release](https://github.com/aiam-nano/probatio/releases/latest), or clone this repository.

| Where | How |
|---|---|
| **Claude app** (web, desktop) and **Cowork** | Settings → Capabilities → Skills → upload `manuscript-review-1.0.0.zip`. Code execution must be enabled. |
| **Claude Code** | Copy `manuscript-review/` into `~/.claude/skills/` (all projects) or `.claude/skills/` in a project, then start a new session. |
| **Gemini app** | Settings → Skills → Install, then choose the zip. |
| **Cursor** | Copy `manuscript-review/` into `~/.cursor/skills/` (or the project's skills folder), then restart Cursor. |
| **GitHub Copilot, Codex, Antigravity and other agents** | Put `manuscript-review/` wherever the agent loads Agent Skills from; see its documentation. |
| **Microsoft 365 Copilot** | Add the skill's files to a declarative agent (Agent Builder). `SKILL.md` is about 18,800 characters, inside the 20,000-character instruction limit. |

Menus move between app versions. If a path above has changed, the vendor's help pages have the current one.

**To check it loaded,** ask: "what does the manuscript-review skill check for?" An answer that describes the five passes and claim verification came from the skill.

---

## Use

Give the skill the manuscript as a PDF, and the supplementary information as a PDF if the paper refers to it.

**In a chat app** (the Claude app, the Gemini app, Microsoft 365 Copilot), attach the files and ask:

```
@manuscript-review review this manuscript using the manuscript review skill.
```

**In an agent that works in a folder** (Cowork, Claude Code, Cursor, Antigravity), put the files in the working folder and name them in the prompt:

```
@manuscript-review review this manuscript using the manuscript review skill. The files are in this folder: paper.pdf and paper-SI.pdf.
```

Plain requests work too ("review this before I submit it", "what would a referee say about this?"), but naming the skill makes sure it loads. Some models answer from their own competence when it is not named.

| You want | Say |
|---|---|
| A review in British English, or a longer one | "…in British English" / "…in about 1,500 words" |
| A field pack | "…using the `<name>` pack" (none ships with 1.0.0; see [Field packs](#field-packs)) |
| The next round | Supply the revised PDF, the earlier findings list and a response (a table or a free-form letter), and say "this is the revision" |
| Numbers checked against your data | Supply the data or analysis code, in any format |

**PDF only.** Word, LaTeX and plain text are refused, with the reason. A PDF is what a referee sees: figures placed, equations typeset, tables laid out. In other formats these fail silently. For example, a Word file with vector figures can convert to a PDF that has the right page count and no figures. Supplementary information must be a PDF too. A response file can be a table or a letter, as text or PDF. Data and code are accepted in any form, though checks against attached data were tested less than the rest.

**What comes back:**
- **The report** is flowing prose: 600 words for a brief communication, 900 to 1,000 for a standard article, 1,200 to 1,500 for a long one. US English by default.
- **The findings list** is complete, with no cap. The report says once that the list is the full record.
- **The chat** gets two or three sentences pointing at what matters most.

---

## Which model to use

The skill is a set of instructions. The model does the reading and the reasoning, and it is the larger variable. In our comparison, the same skill on the same ten papers found anywhere from 3% to 85% of the known errors, depending on the model (below).

**Use a frontier reasoning model.**
- **Claude Opus 5.5** is what the skill was built and validated on.
- **Claude Sonnet 5.5** is the best of the rest we tested, at somewhat lower recall with very few false findings.
- **Below that tier,** expect much lower recall. Some models also produce many false findings, which waste your time and discredit the true ones.

The table below says which. Read every finding critically on any model, and treat the review as one careful reader, not a verdict.

**Capabilities the harness needs:**

| Capability | Used for | Without it |
|---|---|---|
| PDF text extraction and page rendering | everything: the text layer is the search index and the rendered page is the authority | the skill cannot run |
| Code execution | recomputing arithmetic, checking values against attached data, rendering figures | arithmetic checks become questions to the author |
| Web search | checking that citations exist, and coverage of prior work | those checks are skipped, and the report says so |
| Sub-agents | claim verification by a context that did not write the findings | verification runs as a separate stage in the same context, on tool evidence only |

Claude Code and Cowork provide all four. The Claude app provides the first three.

---

## How well it works

**Measured October 2026,** on skill 0.9.0 for detection and 0.9.2 for claim verification. 1.0.0 removes some features that this validation did not cover and changes nothing in the review pipeline, and a regression check confirmed it performs the same (below). Full detail is in [VALIDATION.md](VALIDATION.md) and will be in a forthcoming preprint.

**How truth was established.** Every number below is graded against labels built by models:
- **known errors:** objective errors in the paper, each confirmed against the page by a separate checking model;
- **consensus problems:** problems that independent runs agreed on;
- **planted defects:** errors we inserted ourselves, so the answer key is complete.

The checking and scoring models are from the same family as the reviewer (Claude Opus). Human adjudication of a sample will be reported shortly in a preprint. Until then, read these as careful internal estimates, not independent measurements.

### Recall

| Test | Result |
|---|---|
| **Planted defects** (4 public arXiv papers rebuilt from source: 48 single-point inconsistencies planted across 8 copies, plus an unmodified control of each; 24 runs; the key fixed before any run) | **96.4%** found in a single run (95% CI 91.7–99.5), **97.9%** over two runs; all 8 substantive plants found in every run |
| **Known errors in 30 preprints** (the latest posted on four preprint servers, any topic; 3 Opus runs per paper; each run scored against the errors found by the other two and confirmed on the page; 319 known errors) | **84%** found per run |
| **Consensus problems in the same 30 preprints** (874 items) | **87%** found per run |

The planted defects are the error class the skill is built for: each is one clean inconsistency checkable from the paper itself. Real errors are often harder, spread across sections or needing outside knowledge, so the known-error recall is the more realistic figure.

**What it misses most:** errors that need a value read off a figure (90% per run on planted figure defects, against 98–100% for the other kinds), and small typographical slips in equations.

### Precision

| Measure | Result |
|---|---|
| **False claims among those stated as fact** (115 runs whose every objective claim was checked against the page) | **8.6%**; before claim verification, 12.8% |
| **Real errors stated plainly** (same runs, 1,296 confirmed errors) | 92.9% stated as fact; 6.6% softened to a question or an outside-knowledge label, so they still reach the author; **none removed** |
| **Fabricated quotations** (every run on every model scored so far, quotations checked against the rendered page) | **None** in Claude Opus or Sonnet runs; see the table below for other models |
| **New problems on planted copies,** beyond the plants | 24 raised: 22 valid, 2 plausible, 0 false |

Expect about one or two claims per review that do not hold up when you check them. They are easy to dismiss and are the price of not dropping real ones. Claims the checker could not settle reach you as questions, which tells you where to look.

### Models compared

The same skill (0.9.0), the same 10 preprints, one run per model, scored by the same method against reference sets built from three Opus runs. The bracketed figures are 95% CIs over papers.

| Model | Harness | Known errors found (127) | Consensus problems found (325) | False findings | Fabricated quotations |
|---|---|---|---|---|---|
| Claude Opus 5.5 (leave-one-out over 3 runs) | Claude app | 85.5% | 88.5% | about 0.6% | 0 |
| Claude Sonnet 5.5 | Claude app | 71.7% (60–82) | 80.8% (76–86) | 1 of 245 | 0 |
| Gemini 4 Argon | Gemini app | 61.4% (50–73) | 55.4% (49–62) | 31 of 104 (30%) | 6 |
| GPT-6.1 Sol | Microsoft 365 Copilot | 52.8% (45–61) | 65.4% (59–72) | 3 of 240 | 0 |
| Grok 4.7 (high) | Cursor | 52.0% (40–66) | 55.2% (50–61) | 8 of 134 (6%) | 0 |
| Gemini 3.8 Flash (high) | Antigravity | 44.9% (34–56) | 37.2% (34–41) | 8 of 133 (6%) | 0 |
| GPT-5.6 Sol (high) | Cursor | 33.1% (23–43) | 46.8% (42–52) | 3 of 133 | 0 |
| GPT-6 Luna | GitHub Copilot | 18.5% (9–28) | 22.0% (19–25) | 2 of 82 | 0 |
| Claude Haiku 4.5 | Claude app | 3.1% (1–6) | 13.8% (10–18) | 34 of 127 (27%) | 1 |

**Read with care:**
- **One run per model.** Where the harness hides the effort setting (the Gemini app, Microsoft 365 Copilot), the model's default was used.
- **Model, harness and effort are mixed in each row,** so a row describes that setup, not the model alone.
- **The reference sets come from Opus runs,** which favours an Opus-like reading of each paper.
- **Same harness or different harness:** in a separate test, Opus in the Claude app and in Cowork found known errors at the same rate within run-to-run variation (81.1% and 83.0%). Sonnet in Cursor scored about level with Sonnet in the Claude app, on five papers.

### The 1.0.0 regression check

1.0.0 was run on 3 of the preprints above and on three versions of a fourth paper (draft, revision and published version), with a revision round between the first two.

| Check | Result |
|---|---|
| Known errors on the 3 preprints | 85.9% (Opus 0.9.0: 85.5%) |
| Consensus problems on the 3 preprints | 86.1% |
| False findings | 0 of 73 on the preprints; 0 to 1 per run elsewhere |
| Fabricated quotations | none |
| The revision round | all 18 earlier findings carried forward with a status; the declined one never raised again; the claimed change checked against the revised text |

On the fourth paper, 1.0.0 found every substantive and moderate error the earlier checks had confirmed, in all but one run, and fewer of its minor equation typos than the earlier 0.9.0 runs had.

---

## How a review runs

1. **Intake.** The PDF is read twice, as extracted text and as rendered pages. The layout is identified first, because two-column extraction interleaves columns and a quotation must be taken from the page. Supplementary material is requested if referenced and missing. The text layer is scanned for concealed instructions.
2. **Five passes,** each targeting one criterion: story, presentation, evaluations, correctness, significance. Separate passes find substantially more than one all-in-one pass: in the AAAI-26 review pilot, 64% of injected defects against 43%.
3. **Adversarial pass, then a steelman filter.** The strongest criticisms are generated, then each is defended against. Anything that misreads the paper, is already answered in it, or rests on a convention the field does not hold is dropped, not softened.
4. **Findings,** each with a quotation, location, severity, fix, and what would make it wrong.
5. **Claim verification,** as above.
6. **Integrity gate:** a silent pre-delivery check that every quotation is verbatim, no reference is invented, severity follows the taxonomy, retrieval queries were generic, the report holds its length band, and the banned-vocabulary scan was run on the report itself.

---

## What it does not do

- **It does not referee.** It produces author-facing feedback, not a referee report, and no accept-or-reject verdict. If you have been asked to referee someone else's manuscript, this skill is the wrong tool. Most major publishers prohibit sharing a manuscript under review with AI tools, and that obligation is yours personally.
- **No numeric quality score** and no "AI-written" detection. The first has no calibration behind it; the second has detectors too poor to accuse anyone with.
- **It never edits your manuscript.** It reads and reports. Revisions are a separate task.
- **Not in 1.0.0:** checks against a journal's author guidelines, text-overlap checks against prior work, and research-assessment readiness. Asked for one, the skill says once that it is out of scope and runs the scientific review.
- **One pass is not a census.** A review finds a great deal, but not everything. The findings list is complete in that nothing found is withheld, not in that nothing was missed.

---

## Your manuscript and your data

**Where your manuscript goes.** The skill runs inside your AI tool, so the manuscript goes wherever that tool sends it, under that provider's terms. Check them before using it on unpublished work. Nothing in the skill sends your manuscript anywhere else.

**Literature searches** (used to check citations and prior work) are built only from generic field vocabulary: never the title, the authors, your sentences or your results. Every query is logged in the findings list, so you can audit what was sent.

**Embedded instructions.** Text planted in a PDF to steer AI reviewers ("ignore previous instructions", white or microscopic text) is treated as data, never as instruction. It is reported as a critical finding in its own section, and is otherwise disregarded.

---

## Field packs

A field pack is an optional checklist of a discipline's norms: the methods details, standards, claim conventions and red flags a generalist reviewer would miss. Packs load only when you name one, never on inferred content, because the wrong field's expectations produce criticism that is confident, specific and wrong. A pack adds checks and never removes one.

**No pack ships with 1.0.0.** A graphene materials pack and its modelling companion will follow in a minor release.
- To write your own, start from `manuscript-review/packs/PACK-INTERFACE.md`, and use `TEMPLATE-field.md` (a discipline's norms, each requirement sourced) or `TEMPLATE-house.md` (one group's conventions, reported as such).
- Contributions are welcome; see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Feedback

This is a public test release, and reports of what it gets wrong are the most useful thing you can send.

- **[A false finding](https://github.com/aiam-nano/probatio/issues/new?template=false-finding.yml)**: the skill said something is wrong that is not.
- **[A missed problem](https://github.com/aiam-nano/probatio/issues/new?template=missed-problem.yml)**: something a referee raised, or you found, that the review did not.
- **[A bug or a harness problem](https://github.com/aiam-nano/probatio/issues/new?template=bug.yml)**: it did not load, did not write its files, or broke in a particular tool.
- **[Discussions](https://github.com/aiam-nano/probatio/discussions)**, for general feedback, questions and experience with particular models.

**Never paste text from an unpublished manuscript into an issue or discussion.** Issues are public. Describe the problem in your own words, give the section and the kind of error, and if you can, show it on a published paper instead. A report without the manuscript is still useful.

Security issues, for example a way to make the skill follow instructions hidden in a PDF: see [SECURITY.md](SECURITY.md).

---

## Design decisions

- **No quotation, no finding.** Vague criticism is the commonest failure of automated review. A verbatim quotation makes fabrication detectable and forces specificity.
- **The wrongness clause.** Stating what would make a finding wrong dissolves some findings before they reach you.
- **A complete list, a bounded report.** Thoroughness that is not prioritised hands the prioritising back to the author. So the report stays within its band and leads with what matters most, and the list records everything.
- **Verification relabels and never deletes.** Testing showed that removal was where real errors were lost. A doubted claim reaching you as a question costs you seconds; a real error removed costs you the referee's objection.
- **Length and tone are enforced.** Drift to several times the requested length, and a first pass so harsh it must be redone, are both documented failures of AI review.
- **US English by default** because most target journals use it; British English on request. This repository's own prose is British.

---

## Sources and credits

Mechanisms adapted from prior work. Nothing here is a fork: every mechanism was re-implemented from its published description, and no source code or text was copied. Licences are recorded so the terms of reuse are visible.

- **Criterion-targeted staged review; self-critique before delivery; code execution for numerical checks; restricting novelty conclusions to published work; the perturbation-benchmark method:** Biswas, J. et al. (2026), *AI-Assisted Peer Review at Scale: The AAAI-26 AI Review Pilot*, arXiv:2604.13940. CC BY 4.0; this entry is the attribution. The pilot's prompts were withheld by its authors and are not reproduced.
- **Segmented analysis with whole-text context:** `whoisraibolt/paper-skills`, implementing the architecture of Google Research's Paper Assistant Tool (arXiv:2606.28277). MIT. Its authors ask that the archived release be cited: Zenodo DOI 10.5281/zenodo.21982661.
- **Quote-required findings; the wrongness field; refusing to paste manuscript text into third-party services:** `whoisraibolt/paper-skills`, original to that repository. MIT.
- **Paradigm branching before review; the banned-vocabulary scan:** `hkustdial/supervisor-skills`, `pre-submission-reviewer`. **CC BY 4.0**, an attribution requirement that survives adaptation. This entry and the notice in `LICENSE` give that credit.
- **Author-defence and steelman filter; comparing what a design establishes against what a paper claims:** B. G. Popescu, *Agentic AI for Social Science Research*, `argument-review`. No licence stated, so only the ideas were used, re-implemented from scratch.
- **Blind parallel review with corroboration:** `AlexWortega/ai-peer-review-skill`, adapting `poldrack/ai-peer-review`. MIT for the adaptation.
- **Numerical consistency across abstract, text, tables and figures:** `Aperivue/medsci-skills`, by Yoojin Nam. MIT.
- **Claim, evidence, adequacy as the backbone of the story pass:** `jkitchin/skillz`, `scientific-reviewer`, by John Kitchin. MIT.
- **Line-pinned citation discipline:** K-Dense "Paperclip", from `K-Dense-AI/scientific-agent-skills`. MIT.
- **Untrusted-materials rule and the read-only constraint:** `imbad0202/academic-research-skills`.
- **The ladder of evaluative authority; validation before deployment:** the 2026 survey of AI in peer review, and Baumann, J. et al. (2026), *Stop Automating Peer Review Without Rigorous Evaluation*, arXiv:2605.03202. Cited as framing.

This is a good-faith record, not legal advice. Check the sources before relying on it.

---

## Licence and citation

[MIT](LICENSE), with the attribution notice in `LICENSE`. Copyright (c) 2026 Aravind Vijayaraghavan.

If the review contributes to your work, an acknowledgement is welcome. To cite the skill, use [`CITATION.cff`](CITATION.cff) (GitHub's "Cite this repository" button) or a Zenodo DOI: [10.5281/zenodo.23540018](https://doi.org/10.5281/zenodo.23540018) for version 1.0.0, or [10.5281/zenodo.23540017](https://doi.org/10.5281/zenodo.23540017) for all versions (it always resolves to the latest).

**Skills run in your agent's environment.** Read `SKILL.md` and the files beside it before installing this or any other skill.
