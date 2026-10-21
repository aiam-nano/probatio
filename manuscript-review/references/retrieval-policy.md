# Retrieval policy

Governs every search made while reviewing. The capability is valuable and stays. What may leave the machine is tightly constrained.

## The problem

Checking whether a citation exists, and whether the field's relevant prior work has been covered, needs a literature search. A search sends text to a third party. An unpublished manuscript is confidential, and where it is one the user has been assigned to review, it is confidential by obligation rather than preference.

The risk is not the act of searching; it is what the query contains. A query built from the paper's own title, its distinctive phrasing or its headline numbers discloses the work as surely as sending the file would, and is recorded in the search provider's logs. The repository whose novelty check inspired this stage refuses on principle to paste manuscript text into a third-party service. That refusal is reproduced here.

## Query construction

Build every query only from **generic field vocabulary**: terms any specialist working in the area would type without having seen this manuscript.

Permitted: the field and subfield, material or system classes, standard method and technique names, established phenomena, instrument types, standard metric names, common application areas.

Never permitted: the manuscript's title or any part of it, author names or affiliations, verbatim sentences or clauses from the text, any phrasing distinctive enough to identify the work, specific numerical results, sample or specimen identifiers, grant or project names, funder names, named collaborators, unpublished compound, material or system names coined by the authors.

The test before sending: **could this query have been written by someone who has never seen this manuscript?** If not, rewrite it until it could.

## Worked contrast

A paper reports that a particular surface treatment raises the tensile modulus of a filled composite by 34%, using a named proprietary coupling agent.

Send: `interfacial coupling tensile modulus polymer composite`, or `silane surface treatment filler adhesion mechanical properties`.

Do not send: the paper's title; `34% modulus improvement coupling agent`; the proprietary agent's name; any sentence from the abstract.

The permitted queries find the same literature. They simply do not announce what was done or by whom.

## Two checks, two risk profiles

**Citation verification** is the safer half. Searching for a reference the paper already cites discloses nothing about the paper, because the cited work is public and the citation is not distinctive of this manuscript. Run it freely, subject only to the mode gate below. Verify that the work exists, that its details are as stated, and that it supports the claim attached to it.

**Novelty and coverage checking** is the exposed half, because the query must describe what the paper does. Apply the construction rule above strictly. Where the contribution cannot be described without identifying it, do not search: record instead that novelty could not be checked without disclosure, and say so in the report. That is an honest outcome and a useful one.

## Source restriction

When judging novelty and coverage, restrict conclusions to **published, peer-reviewed work at recognised venues**. Disregard preprints, theses, patents and grey literature for this purpose.

A preprint may later be withdrawn, may never pass review, and cannot support a finding that the authors have missed established prior art. The AAAI-26 pipeline applies the same restriction to its significance stage and reports that it improved precision.

Preprints may still be mentioned in a report as context for the authors, clearly labelled as unpublished. They may not be the basis of a major finding.

## What retrieval may and may not support

Retrieval supports judgements at the level of **existence, authorship, venue, date and general topic**.

It does not license quoting numbers, method details, results or conclusions out of search snippets into a review. A snippet is an uncontrolled fragment, often of an abstract, often stale. Treating one as evidence produces findings that are confidently wrong about papers that are real, which is the hardest kind of error for an author to refute.

Where a specific detail of a cited work matters to a finding, either retrieve the source properly and read it, or state the finding as a question for the authors rather than as an assertion.

## Retrieval is on by default

The manuscript is the user's own, so the disclosure decision is theirs. Apply the construction rule regardless: authors routinely underestimate how identifying their own phrasing is, and priority matters to them.

## Logging

Record every query you send in the findings list, under `queries_sent`, exactly as sent. This makes the constraint auditable rather than merely asserted: the user can see what left the machine.

Record alongside it which findings rest on retrieval. Those findings carry a different evidential weight from findings read directly off the page, and the user is entitled to know which is which.

## When retrieval is unavailable

Say so, once, in the report: citation verification and novelty checking were not performed, because no search capability was available.

Do not substitute a weaker version of the same conclusion drawn from memory. A recollection that a related paper exists, unchecked, is how a confidently named non-existent reference reaches an author. Nothing about a review is more damaging.
