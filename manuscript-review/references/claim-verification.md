# Claim verification

Stage 7a. It runs after the findings list is complete and **before the prose report is written**. Its job is to check what the findings say about the manuscript, as a reader who did not write them would. It relabels findings; it never adds new ones and never removes a claim.

The development data behind this stage come from 2,096 findings, 98 runs and three sets of checked papers:
- about one claimed error in nine was false, and one in seven could not be settled from the paper;
- most false claims were not misreadings of numbers but **strict readings of approximate or reconcilable statements (61%)**, and **points the paper answers elsewhere (24%)**;
- critical findings were the most reliable, and minor and evaluations-pass findings the least.

So this stage looks for reasons a claim might not hold, and it looks across the whole paper.

## How it runs

**Inputs: the manuscript (with its SI) and the findings list file. Nothing else.** Not the report draft, not the notes or reasoning from the passes. A verifier that sees why a finding was written tends to agree with it.

**Isolated mode, where the harness can start a sub-agent** (Cowork, Claude Code and similar):
- Start one sub-agent.
- Give it this file, the path to the manuscript and SI, and the path to the findings file.
- It returns a verdict for each finding and changes no file itself.
- The writer applies the verdicts and records `**Claim verification:** isolated` in the scope block.

**Single-context mode, everywhere else** (claude.ai chat, harnesses without sub-agents):
- Run this stage as a separate step.
- Re-open the findings file from disk and work from it, not from memory of the passes.
- Do not start the report until the stage is complete.
- **In this mode a claim is confirmed only on tool evidence:** a full-text search hit list, a code recomputation, or a freshly rendered crop. A conclusion you reach by reasoning alone does not confirm a claim here, because the context that produced the claim is still present.
- Record `**Claim verification:** single context`.

If neither mode can run (no code execution and no sub-agent), record `**Claim verification:** not run, <reason>`. In that case every objective claim not already recomputed is phrased as a question, per item 19 of the integrity gate.

## Part A: grounding, for every finding

These are integrity-gate items 1 to 3 and 20, moved here so that a reader who did not write the findings runs them.

1. **The quotation is on the page, verbatim.** Check it against the rendered page, which is the authority, and against the text layer. A quotation that cannot be found: remove the finding (gate item 1).
2. **The location exists** and points to the quoted passage (gate item 3).
3. **Absence claims are searched.** For "X is not reported" or "no Y is given", search the whole text, the captions, the tables and the SI for X or Y, and its synonyms and symbols.
   - If it is there, the claim becomes a question that cites the hit: "X appears to be given at <location>; check whether this covers it."
   - If the search could not cover everything (for example, figures without a text layer), narrow the claim to the ground actually searched (gate item 2).
4. **Figure claims are earned.** Any value, trend, label or presence or absence read from a figure must come from a render you have looked at in this stage, at a resolution where it is legible (gate item 20).

## Part B: claim verification, for every objective claim

**An objective claim** says that something in the manuscript is wrong, and checkably so, from the manuscript alone. Examples:
- a number that does not follow from the paper's own data;
- text against a table, figure or the SI;
- a unit, an equation, a label or cross-reference;
- a reference wrong on its face;
- methods that contradict themselves;
- duplicated data;
- impossible statistics.

Judgement findings (missing controls, overclaiming, weak novelty, unclear writing) are not re-checked here; they already passed the steelman filter.

**Set the `Kind` of every finding:** `objective` if it makes at least one objective claim, `judgement` otherwise.

**Split before checking.** A finding often makes several claims: "X contradicts Table 2, and the same value also conflicts with Figure 4". Check each one separately. False sub-claims inside otherwise valid findings were the most common failure.

For each claim:

1. **Restate it as one checkable sentence.** "Section 3.2 gives A for Q; Table 2 gives B for the same Q; A ≠ B."
2. **Gather the evidence with tools, before forming a view:**
   - **Search the whole text, captions, tables and SI** for every occurrence of the key quantity, symbol, sample name or term. Read every hit in context. Most missed-context failures are an answer sitting in another section, a caption or a footnote.
   - **Recompute any arithmetic with code,** from the values as printed. Respect the rounding of the inputs: a result that follows from unrounded inputs is not an error.
   - **For a claim read off a figure,** render that region afresh at 200 dpi or more and read it again. Where the figure is vector graphics, extract the plotted coordinates if you can.
   - **Compare the passage on the rendered page with the text layer,** so that an extraction artefact (a ligature, a superscript, a dropped glyph) is not mistaken for the authors' error.
3. **Try to make the finding's `Wrong if` true.** It states what would refute the finding, so look for exactly that.
4. **Look for a reasonable reading under which the manuscript is right.** In particular:
   - **Approximate wording** ("~", "about", "approximately", "comparable", rounded ranges, "orders of magnitude") is not contradicted unless the data fall outside what the approximation allows.
   - **Different things compared.** Are the two values from different samples, specimens, experiments, conditions, data sources or definitions? Two values for different things do not conflict.
   - **Relative statements.** "Increased" or "higher" relative to what? Check the comparator the paper actually uses.
   - **The paper's own definitions and conventions,** stated anywhere in it, including the SI.
   - **A wording slip that misstates nothing.** If a wording slip changes no stated fact, it is not an objective error.

   **A confirmed mismatch stays confirmed.** Where the claim is that two places in the manuscript disagree, and you have confirmed that each place says what the finding quotes, the verdict is `confirmed`, even if one of the readings above might reconcile them. Put that reading in the evidence line (`possibly <rounding / different samples / approximate wording>`). The writer adds it to the finding for the author and may lower the severity to minor. The author knows which reading is meant; the verifier does not.
5. **Give a verdict** (below), with one line of evidence: the search hits, the recomputed value, or what the crop shows.

## Verdicts

| Verdict | When | What happens to the finding |
|---|---|---|
| `confirmed` | The tool evidence shows the error, and no reasonable reading removes it; or the claim is a mismatch whose two readings you have confirmed | Kept. `Verified by` is set from the evidence route used in this stage |
| `question` | It cannot be settled from the manuscript (the data are not reported, a quantity is undefined, the text is ambiguous), or the manuscript appears to show it does not hold (a search hit resolves it, the recomputation agrees with the paper, the crop shows otherwise) | Kept, rephrased as a question to the authors: what to check and why. Where the evidence points against the claim, the question cites it: "the paper gives X at <location>, which may resolve this". The writer reassesses severity per `severity-taxonomy.md`: one level lower by default, unless the unresolved point blocks the central claim |
| `outside knowledge` | It rests on a fact not stated in the manuscript: a cited source, a datasheet or standard, a constant, a field convention | Kept, labelled `Rests on outside knowledge: <the fact>`, severity at most major, and not the report's principal concern. Where the outside fact came from retrieval in this session, say so |

**Apart from a finding whose quotation is not on the page (Part A, item 1), nothing is removed at this stage.** A claim you doubt reaches the author as a question carrying your evidence: a true error is never lost, and a false one costs the author a moment. When uncertain between `confirmed` and `question`, take `question`, except for a confirmed mismatch (above).

**Give the verdict per sub-claim.** The finding is stated as firmly as the sub-claim that carries its point; a questioned side point does not turn a confirmed error into a question.

**Severity flags for the writer.** The verifier does not reassign severity, but it flags two cases for the writer:
- a confirmed claim that contradicts a number or conclusion in the abstract while tagged minor or major (possible under-calling);
- a critical finding whose central claim became a question.

## What this stage reports

**Isolated mode:** the sub-agent's reply. **Single-context mode:** the working record of the stage. Either way the output is one line per finding:

```
F<n> | kind: objective/judgement | grounding: ok / removed / narrowed
     | claims: <k> confirmed, <k> question, <k> outside (per sub-claim: 1 confirmed, 2 question, ...)
     | evidence: <search hits / recomputation / crop / page>
     | flag: <severity flag or none>
```

This is a working record, not a deliverable. The writer applies it, and its traces in the findings list are:
- `Kind`;
- `Verified by`;
- `Check`;
- the outside-knowledge label;
- the scope line.

## Limits, stated plainly

- **This stage checks claims against the manuscript.** It cannot find errors the passes missed, and it does not try.
- **Run by the same model, it shares that model's blind spots,** most of all in reading figures and in outside facts. That is why figure claims are re-rendered and outside facts are labelled rather than asserted.
- **Cost:** in development data, about 40% of findings made an objective claim, about nine claims per run. Check those, and do not re-read the whole paper.
