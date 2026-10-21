# Findings list template

The second artefact, held separately from the prose report, for the user's triage and for the next review round. Write it as a file; do not paste it into the prose.

Unlike the report, this is structured, labelled, and exposes the internal fields. It is a working document, not a deliverable to a third party.

---

## Header

```markdown
# Findings: <manuscript short title>

**Skill:** manuscript-review
**Date:** <date>
**Document type:** <research article | review | methods | communication | case study | theory>
**Pack:** <pack name and type (field/house), or "none, broad-scope review">
**Target length:** <n> words
**Document state:** draft | proof, <evidence> | published, <journal, year, DOI>
**Review round:** <n>  (omit on a published document)
**Previous round:** none | <findings file name>, round <n−1>, <date> | set aside, published document
**Response file:** supplied, <name> | not supplied | not applicable

## Scope of this review
**Read as:** PDF text layer + rasterised pages | text layer only, <reason>
**Layout:** word-processed single column | typeset single column | typeset two column | mixed, <where>
**Figures inspected:** yes | partially, <which> | no, <reason>
**Render verified:** yes, figures confirmed present on rasterised pages | no, <what happened>
**Supplementary material:** reviewed | referenced, not supplied | none referenced
**Attached data or code:** <what was supplied and what was done with it> | none
**Computation:** available, used for arithmetic | unavailable
**Claim verification:** isolated | single context | single context, partial: <findings not verified> | not run, <reason>
**Retrieval:** on | off, reason
**Checks inapplicable to this document type:** <which, and why>

## Embedded instructions
**Scan run over extracted text:** yes | no, reason
**Fired:** yes, see F1 | no
```

Note the last field under Embedded instructions. It records that the scan was run, which is different from recording that the manuscript was clean. The report never tells the user a clean scan is reassuring; the findings list records only the procedure.

## Summary

```markdown
## Summary
Critical: <n> · Major: <n> · Minor: <n>
Entries: <n>  (scientific review only; the list is complete, there is no cap)
Dropped: none
Verification: <n> objective claims checked · <n> confirmed · <n> question · <n> outside knowledge
Discussed individually in the report: <n> of <n>
Pack entries: <n> of <n> cite the pack  (only where a pack is loaded)
Proof fixes: <n> proof correction · <n> needs editor's agreement  (proof only)
Earlier findings: <n> addressed · <n> partially · <n> not addressed · <n> declined · <n> no longer applicable  (round 2 onward)
New this round: <n> (of which introduced in revision: <n>)  (round 2 onward)
```

## Findings

```markdown
### F1 · CRITICAL · <short name>
**Pass:** story | presentation | evaluations | correctness | significance | intake
**Location:** <section, page, figure, table>
**Quote:** "<verbatim text from the manuscript>"
**Problem:** <what is wrong, in one or two sentences>
**Fix:** <concrete, actionable>
**Wrong if:** <what would have to be true for this finding to be mistaken>
**Source:** manuscript | retrieval | pack: <pack> §<section> | attached data
**Kind:** objective | judgement
**Rests on outside knowledge:** <the fact>  (only where claim verification found the finding depends on it)
**Verified by:** recomputation | full-text search | re-rendered figure | page comparison | direct reading | unverified, phrased as a question
**Check:** confirmed | question | outside knowledge | n/a  (one per sub-claim where there are several: `confirmed (1, 3); question (2)`)
**Raised:** round <n> | round <n>, introduced in revision
**Status:** open
**Proof fix:** proof correction | needs editor's agreement  (proof only)
```

## Field notes

**Pass** is what makes validation diagnostic. When a benchmark run shows the skill missing a class of defect, this field says which pass is weak rather than only that the skill missed something. Use `intake` for findings that arose before the passes, including embedded instructions.

**Location** must be specific enough to navigate to. "The introduction" is not a location; "Section 1, final paragraph" is.

**Quote** is verbatim. Where the problem is an absence, quote the surrounding text where the missing content should have appeared and mark it `[absence]` inside the field. The label is always `**Quote:**`, never a variant such as `**Quote (absence):**`, so that the field can be found.

**Fix** is what the author does on Monday morning. If it cannot be written concretely, the finding is not yet understood well enough to report.

**Wrong if** is one clause. It prevents overconfident criticism, and writing it dissolves some findings before they reach the list, which is the point.

**Source** matters for later rounds and for honesty. A finding from retrieval carries different weight from one read off the page, and a pack finding is only as good as the pack. A pack source names the pack and its section, `pack: graphene §3.5`, so the user can check the requirement the finding rests on; see `references/output-contract.md`.

**Verified by** separates what was recomputed from what was suspected. A recomputed discrepancy is reported firmly; unverified arithmetic is phrased as a question to the authors.

## Verification fields

Claim verification (Stage 7a, `references/claim-verification.md`) sets these after the passes, before the report is written.

**Kind** says whether a finding asserts an objective error (something in the manuscript is wrong, checkably so from the manuscript alone) or makes a judgement (a missing control, overclaiming, novelty, clarity). A finding with both is `objective` if any objective sub-claim survives verification. The tag tells the author which points are checkable facts and which are arguable.

**Verified by** records the evidence the verification stage used, not the route the passes used. In single-context mode, `direct reading` alone does not confirm an objective claim.

**Check** is the verification verdict, recorded for each sub-claim; judgement findings read `n/a`. The finding is stated as firmly as the sub-claim that carries its point: a confirmed main point stays a firm statement in the list and the report even where a side point is a question, and that side point is phrased as a question within it. A confirmed mismatch keeps any reconciling reading the verifier offered, as a note for the author. The field is internal: the prose report never shows it, and carries the verdict by how firmly it states the point.

**Rests on outside knowledge** names the fact a finding depends on that the manuscript does not state: a cited source's content, a standard, a constant, a field convention. Such a finding is at most major and is not the report's principal concern.

**Removed at verification.** Claim verification removes no claim: one it doubts stays, as a question citing its evidence. The only removal is a finding whose quotation is not on the page (integrity gate item 1), recorded after the findings:

```markdown
## Removed at verification
1. F11 (whole finding): "<the claim>". Quotation not found on page <n>
```

These are not drops: `Dropped:` still reads `none`. The report never mentions this block. Where nothing was removed, write `none`.

## Query log

```markdown
## Queries sent
1. `interfacial coupling tensile modulus polymer composite`
2. `silane surface treatment filler adhesion mechanical properties`
```

Every search sent, exactly as sent. This makes the retrieval constraint auditable rather than asserted: the user can see what left the machine and check it against the rule in `retrieval-policy.md`. Where no searches were sent, record `none`.

## Ordering

Order by what would most change a reviewer's verdict, not by severity tag alone and not by position in the manuscript. A major finding that undermines the central claim outranks a critical finding in a peripheral section. The numbering should reflect the order the author should work in.

## Completeness

**This list is the complete record.** Every finding that survived the steelman filter appears here, however long that makes it. Nothing is dropped for length, and `Dropped:` reads `none` in every properly produced list.

Aggregate minor findings into single entries listing several locations, and merge findings sharing a root cause, because the author fixes those in one pass. Never merge two problems requiring two different fixes.

The prose report is the bounded document and may group or pass over individual entries; this one may not. Record in the summary how many entries the report discusses individually, so the user knows which document is the census.

## Later rounds

In round 2 onward, follow `references/rounds-and-states.md`. Carry the earlier list forward rather than starting fresh: every earlier finding keeps its ID and gains an updated status, checked against the **revised manuscript**, not against the response file, which is the author's account of the revision rather than evidence of it.

```markdown
### F1 · CRITICAL · <short name>
**Raised:** round 1
**Status:** open | addressed | partially addressed | not addressed | declined by author | no longer applicable
**Author response:** "<the author's words, quoted>" | none given | none
**Reason check:** the manuscript does not bear this out: <quote or located absence>
**Verified against:** <location in the revised manuscript>
**Assessment:** <what changed, and what remains>
```

`Author response:` reads `none given` for a decline with no reason and `none` where the response does not mention the finding. `Reason check:` appears at most once in the life of a finding, in the round the decline is first recorded, and only where a stated reason is contradicted by the manuscript.

Then append the new findings, numbered on from the highest earlier ID so both rounds read together, and list any response entries that match no earlier finding:

```markdown
## Unmatched response entries
1. "<the entry, quoted>"
```
