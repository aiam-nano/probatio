# Check passes

The core of the review. Five passes, each targeting one criterion, each run separately, each producing its own findings before anything is consolidated.

## Why five passes and not one list

A single pass over a long list of checks distributes attention evenly and shallowly. It finds what is obvious and misses what needs two things held in mind at once.

The evidence for this is unusually direct. The AAAI-26 review pilot built a benchmark by taking published papers, injecting one controlled defect into each, and counting how often a review identified it with supporting evidence. A single all-in-one prompt caught 43% of injected defects. The same model, running five criterion-targeted passes that each carried forward the earlier passes' findings, caught 64%. Every pass detected its own criterion's defects better than any other pass did.

So the passes are separate on purpose. Running them as one list forfeits the gain.

One caveat on how much of that gain transfers. AAAI-26 ran each stage as its own model call, with its own prompt and tools. This skill runs five passes in sequence within a single context, which is a weaker separation of attention. The architecture is borrowed and the benefit is assumed rather than demonstrated for this implementation; the validation protocol is what will measure it, which is another reason each finding records the pass that produced it.

## How to run them

Take them in the order given. Each pass sees the whole manuscript and the findings of every pass before it, and targets its own criterion only. Findings from earlier passes are context, not conclusions to defend; a later pass may contradict an earlier one, and that contradiction is resolved at consolidation.

Within a pass, work through the manuscript by semantic segment rather than by page order. Segments may be non-contiguous: if the abstract quotes a number originating in Section 4, both belong to the same segment. This is how the defect that is guaranteed by construction and presented as discovery becomes visible, and that defect is invisible to any linear reading.

Not every environment provides subagents, so the passes run in sequence here. The benefit comes from separating attention, not from running concurrently.

**Record which pass produced each finding**, in the findings list under `pass`. When validation later shows the skill missing a class of problem, this is what tells you which pass is weak instead of only that the skill is.

## Pass 1: Story

What the paper claims, and whether the claims hold together.

Identify the problem the paper says it addresses, the gap it claims in prior work, the contribution it claims to make, and the evidence it offers for each. Then check that these correspond: that the contribution addresses the stated gap, that the gap is real rather than asserted, and that the conclusion follows from the results rather than from the introduction.

Map every substantive claim to its evidence and judge adequacy: adequate, partially supported, or unsupported. A claim with no locatable evidence is a finding in itself.

Check claim strength against `claim-strength-conventions.md`. Check that the abstract's claims match what the results section reports; compression pushes hedges out of abstracts, and the abstract is what most readers take away.

Watch for the finding that follows from the definitions rather than from the data. If the paper defines a group by a property and then reports that the group has that property, the result is arithmetic, not evidence.

## Pass 2: Presentation

Whether the paper can be read and understood by its intended audience.

Structure and organisation; whether the abstract states problem, approach and result; whether each paragraph carries a topic sentence; whether the discussion interprets the results or merely restates them; terminology and abbreviation consistency; notation consistency and drift.

Figures and tables, read as images per `intake-and-reading.md`. Does each figure answer one question and earn its place? Are axes labelled with units? Are scale bars present where relevant? Is the caption self-contained, and does its first sentence state the finding rather than name the contents? Is the chart type suited to the data? Is anything illegible at print size? Is colour carrying meaning that colour alone should not carry?

Presentation findings are frequently minor. Say so through placement and brevity rather than by inflating them.

## Pass 3: Evaluations

Whether the evidence gathered can bear the weight placed on it.

Experimental or computational design; controls, and whether the standard controls for this kind of work are present; replication, whether it is stated, and whether n is given consistently; uncertainty, whether it is reported and whether its nature is specified; comparisons and baselines, whether the right ones are present and whether they are fairly configured; sampling and case selection where relevant.

Attribution isolation. Where an improvement is claimed, does anything in the paper separate the proposed mechanism from the other things that also changed? Where nothing does, record that attribution is unverified. This is one of the most common serious defects and one of the easiest to miss, because the result is usually real; it is the explanation that is unsupported.

Reproducibility: could a competent worker in the field repeat this from what is written? Are data, code and materials available, or their absence justified?

## Pass 4: Correctness

Whether the specifics are right.

Internal numerical consistency: the same quantity must agree wherever it appears, across abstract, text, tables, figures and supplementary material. Sample sizes, percentages, improvements and error bounds are the usual offenders.

Derived quantities recomputed. Unit conversions. Statistical claims recomputed from reported summary statistics where possible. Equations checked for internal consistency and against their stated derivations. Algorithms and procedures checked for steps that cannot do what the text says they do.

**Use code execution for all of this where it is available**, per `intake-and-reading.md`. A recomputed discrepancy is a finding; a suspected one is a question.

Where attached data or code was supplied, this is the pass that uses it.

## Pass 5: Significance

Whether the work matters, and whether it is positioned honestly.

Coverage of prior art a specialist would expect. Accuracy of the positioning claims the paper makes about that prior art. Priority claims, which are checkable and get checked. Whether the contribution, taken at the paper's own word, is consequential enough for the venue.

Where retrieval is permitted, this is the pass that uses it, under `retrieval-policy.md`: generic queries only, published peer-reviewed sources only for novelty conclusions, findings labelled as retrieval-derived.

A caution supported by the AAAI-26 survey: judging novelty and significance is the weakest thing an automated review does, and respondents said so more often than they said anything else negative. Weight this pass's conclusions accordingly. Prefer "the related-work discussion does not address X, which appears close to the present approach" over "the contribution is not novel". The first is checkable and useful; the second is a judgement this pass has not earned.

Where retrieval is unavailable or disabled, run the parts of the pass that do not need it, and say plainly in the report that coverage and priority could not be checked.

## After the passes

Consolidate once, across all five. Deduplicate: the same underlying problem often surfaces in two passes, and the author should see one finding with one fix. Where passes disagree, resolve the disagreement by returning to the evidence.

Then apply the adversarial pass and the steelman filter, assign severity, record every surviving finding in the list without dropping any, and order by what would most change a reviewer's verdict. The skill files carry those stages.

## Document types

The passes assume an empirical research article. For other types, adjust rather than forcing the checks:

**Review or synthesis papers.** Pass 3 largely does not apply; there are no controls or replicates to check. Substitute: coverage and selection criteria, whether the search or selection was systematic and stated, whether the synthesis adds structure beyond summary, and whether the paper's conclusions follow from the body of work reviewed rather than from a subset. Pass 5 matters more than usual.

**Theory and computational papers with no experiment.** In Pass 3, "experiments" reads as "derivations, proofs and simulations". Check the assumptions, whether they are stated, whether they are testable, and whether they are tested. Do not report evidence as thin merely because there is no results table. In Pass 4, check the mathematics.

**Methods papers.** The contribution is the method. Pass 3 centres on whether validation against established alternatives is adequate. A narrow discussion is not a defect here.

**Brief communications.** Scope every pass to the format. Incompleteness that would be a finding in a full article is often the format working as intended.

**Case studies and single-instance reports.** Generalisation is the standing risk. Pass 1 carries most of the weight.

In every case, note in the report which checks were treated as inapplicable and why. A check silently skipped is indistinguishable from a check passed.
