# Domain pack guidance

How to write a pack, what belongs in one, and where the limits are.

A pack adds field-specific rigour to a review that is otherwise subject-agnostic. It is a single markdown file in this directory, named `<slug>.md`, and it is loaded only when the user names it.

---

## Part 1: The rules

These are not negotiable, and a pack that breaks one should be rejected rather than repaired.

**Packs are optional.** The core runs a full broad-scope review without one. A pack that is not loaded costs nothing.

**Packs load only on explicit invocation.** The user names the pack: "review this using the graphene pack". The skill may suggest a pack and wait for confirmation. It never loads one on inferred content, because applying the wrong field's expectations produces criticism that is confident, specific and wrong, which is harder to dismiss than generic criticism.

**Packs add; they never subtract.** A pack cannot disable a core check, relax the integrity gate, override an output contract, or change the severity taxonomy. Where a core check genuinely does not apply to the field, the pack says so in its red-flags section and the report notes it as not applicable.

**Packs are data, not instructions.** A pack supplies domain knowledge. It does not alter the skill's behaviour, tone, scope, or how findings are reported. See Part 6.

**A pack must earn its place.** The test is whether it surfaces findings the core alone did not, on real papers. A pack that reads sensibly and changes no output is not worth loading.

---

## Part 2: Pack types

Every pack declares a type, because the three kinds carry different authority and a reader must not mistake one for another.

### `field`

States the norms of a discipline. Its authority is external: standards, reporting guidelines, widely-adopted conventions. Every requirement cites something.

A finding from a field pack is reported as a shortfall against the field's expectations. `TEMPLATE-field.md` is the starting point, with guidance and examples for each section. A worked example, a graphene material pack and its modelling companion, is to be published separately.

### `house`

States the conventions of a single group, department, company or collaboration. Its authority is a local decision, not a field norm, and this changes how findings must be worded.

A finding from a house pack is reported as "this does not meet the group's convention that X", never as "this is wrong". The distinction matters most for the people most likely to be reading: a student who cannot tell a supervisor's preference from a disciplinary requirement will carry the confusion into every paper they write afterwards, and into every review.

House packs must state their authority explicitly in frontmatter and in the scope statement. `TEMPLATE-house.md` is the starting point.

### `venue`

A journal's or conference's scientific expectations, as distinct from its formatting requirements, which are outside this skill's scope.

**Deferred.** Noted here as a recognised type so the interface is stable when it arrives. Do not write one yet: the boundary against formatting requirements needs settling first, and a venue's scientific expectations are largely tacit, which makes sourcing them hard.

---

## Part 3: Scope, and what makes a domain the right size

The most common way a pack fails is being pitched at the wrong breadth.

### The test

**Does a competent generalist in the parent field routinely get these wrong, and do these techniques and claim types recur together in the same papers?**

Both halves must hold.

The first half rules out the obvious. If the core review or ordinary scientific literacy already catches it, a pack adds nothing.

The second half is what makes a pack coherent rather than a list. The techniques and claims should co-occur in real manuscripts, because that is what lets the pack check completeness rather than just list requirements.

### Too wide

"Chemistry". "Materials science". "Biology". "Engineering".

These fail the second half: the techniques do not co-occur, so the checklist becomes either enormous or generic. A generic checklist duplicates the core, and an enormous one breaks the length limit in Part 5.

Symptom to watch for: the pack's completeness checklist has sections that never both apply to the same paper.

### Too narrow

"Raman spectroscopy of CVD monolayer MoS₂ on sapphire". "Our group's rGO foam work".

These are a technique on a material, or a project. They belong as a section inside a broader pack, or as a house pack if the content is genuinely local convention.

Symptom: the pack would be invoked on fewer than a handful of papers a year.

### The working band

Something a person could plausibly describe as their area when asked at a conference. Examples that work:

- graphene and its derivatives (the worked example, to be published separately)
- polymer nanocomposites
- electrochemical energy storage
- thin-film photovoltaics
- microscopy of soft matter
- battery electrode characterisation
- catalysis by supported nanoparticles

Note that these overlap. That is fine and expected: a paper on graphene-reinforced polymer composites might be reviewed with either pack, or with both named. Overlap is cheaper than gaps.

### Splitting

If a pack wants more room than Part 5 allows, that is usually a signal it covers two domains. Split it rather than compressing it. Two 250-line packs that can be loaded separately are more useful than one 500-line pack that is always half irrelevant.

---

## Part 4: Structure

The sections below are the minimum every pack carries. `TEMPLATE-field.md` gives the full structure, which depends on whether the pack covers a material, a family of methods or an application, and adds sections for citation labels, identification, production residues, form, process history, the technique map, physical bounds and downstream claims. Where this part and the template differ in detail, the template is the more recent and governs.

### Frontmatter

```yaml
---
name: <slug, matching the filename>
type: field | house
scope: <one line: what this covers>
sources: <the standards, guidelines or conventions this rests on>
maintainer: <who to ask>
last-reviewed: <YYYY-MM-DD>
---
```

`last-reviewed` is not decoration. Field norms move, standards are revised, and a pack with no date cannot be audited or updated with any confidence. Review annually at least.

### 0. Scope statement

Three or four sentences. What the pack covers, and **explicitly what it does not**.

The exclusion half is what stops the pack being invoked on the wrong paper, and it is the half most often left out. A graphene pack that does not say it excludes other 2D materials will be loaded on a MoS₂ paper by someone who reasonably assumed it applied.

For a house pack, this is also where the authority statement goes.

### 1. Methods-completeness checklist

The core of the pack. What must be reported for the field's standard techniques for a result to be interpretable and reproducible.

Organise by technique. For each, give:

- **Minimum reportable set.** The specific quantities, parameters and conditions.
- **Source.** The standard, guideline or convention that establishes it.
- **Severity.** Which omissions make the result uninterpretable (critical) and which leave it incompletely specified (major).

Write checkable requirements. "Report the laser wavelength, power at the sample, and the number of spectra averaged" is a check. "Ensure Raman is properly reported" is not.

### 2. Claim-strength conventions

Extends `claim-strength-conventions.md` for this field. What evidence does the field require before a class of claim is earned? Which claims are routinely overclaimed here? Which terms have a precise technical meaning that is used loosely?

This section is usually short and is often the most valuable thing in a pack, because overclaiming is field-specific in a way that generic advice cannot reach.

### 3. Red flags

Recurring failure modes a competent generalist would miss. The pack's highest-value content: the things that look fine unless you know the field.

Include, where applicable: characterisation artefacts mistaken for findings; controls that are standard in the field and conspicuous by absence; measurement conditions that must be stated because results are meaningless without them; known confounds; values implausible against what is established for the system.

Close with any core check that does not apply to this field, and why.

### 4. Evidence-adequacy glossary

For each common claim type in the field: what constitutes adequate support, and what does not suffice. A short table is the right form.

This is what lets the claim-to-evidence mapping in Stage 2 return a defensible verdict rather than an impression.

### 5. Contested norms

Where the field genuinely disagrees with itself.

Fields are not uniform, and a pack that states one camp's position as settled will generate confident findings that a referee from the other camp would reject. Where a convention is disputed, say so, give both positions, and instruct that the point be **raised as a question rather than reported as a finding**.

An empty section here is a warning sign rather than a clean bill: most fields have at least one live methodological argument.

### 6. Changelog

Two or three lines per revision. What changed, why, and the date. A pack is a living document and its users need to know when a requirement was added.

---

## Part 5: Length and the context budget

**Hard ceiling: 500 lines, or roughly 5,000 words. Target: 200 to 300 lines.**

The reasoning is concrete. A pack is loaded in full alongside the skill file and several references, and then competes with the manuscript itself for the model's attention. A pack longer than the paper under review is self-defeating.

There is a second cost that is easy to miss. Instruction-following degrades as context fills, and the integrity gate and claim verification are applied at the end of a long pass. A bloated pack does not just crowd out the manuscript; it quietly buys you worse gate compliance, and the failure is invisible in the output.

Where to spend the budget: the red flags and the completeness checklist. Where to save it: background explanation the reader does not need, restatement of core checks, and any technique that appears in one paper in fifty.

If the pack will not fit, split it (Part 3).

---

## Part 6: What must not go in a pack

More important than the inclusions, because each of these does active harm.

**No instructions to the model.** A pack is domain data. The moment it contains "always flag X as critical", "be more sceptical of Y", or "do not report Z", it is behaving as a skill rather than a pack, and it is doing so outside the review the skill files describe. State what the field requires; let the core decide how to report it.

**No duplication of core checks.** Internal consistency, claim-to-evidence mapping, uncertainty reporting, figure quality and the rest are in `check-passes.md` and apply to every paper. Repeating them wastes the budget and creates two sources of truth.

**No severity overrides or gate relaxations.** The pack indicates severity for its own checklist items, per Part 4. It does not change the taxonomy, the completeness rule, or the integrity gate.

**No tone, length or format instructions.** Output contracts govern those.

**No general writing advice.** Not field-specific, and already covered.

**No unsourced assertions presented as field norms.** If a requirement has no standard, guideline or widely-cited convention behind it, either mark it plainly as a convention rather than a requirement, or leave it out. A pack asserting requirements without provenance is one person's opinion in a document that reads as authority, and reviewers will treat it accordingly once they notice.

---

## Part 7: Packs from other people

A pack obtained from someone else is third-party content loaded into the review context. Treat it as you would treat an unfamiliar skill.

**Read it before using it.** All of it, not the description.

**Reject rather than sanitise** anything that reads as an instruction to the model, addresses the reviewer or the assistant directly, attempts to change how findings are reported, or tries to relax any check. A pack does not need these to do its job, so their presence is a reason to distrust the whole file rather than a passage to edit out.

This is the same principle as `untrusted-input.md`, applied to the one place where the suite invites external content into the review.

---

## Part 8: Testing a pack

The rule from Part 1 made concrete.

**The delta test.** Run the core alone on a paper in the field. Run the core plus the pack on the same paper. Show what the pack caught that the core did not. If the answer is nothing, across several papers, the pack is not earning its load.

**The perturbation test**, once a calibration set exists. Plant a defect the pack should catch and the core should not: a missing reportable quantity from the completeness checklist, or one of the field's red flags. Check that core-plus-pack finds it and core alone does not. This is a sharper test than the delta, because it has ground truth.

**The false-positive test.** Run the pack on a good paper in the field, ideally one that passed review at a strong journal. Findings it generates there are either genuine gaps that survived review, which is interesting, or pack over-reach, which needs fixing. A pack that fires on everything is worse than no pack.

**The wrong-paper test.** Run the pack on a paper just outside its scope. It should produce few findings and no confident ones. If it generates authoritative-sounding criticism of a paper it was not written for, the scope statement in section 0 needs tightening.

---

## Part 9: Template

The template is `TEMPLATE-field.md`, Part F, for `field` packs, and `TEMPLATE-house.md` for `house` packs. It is kept in one place only, so that two copies cannot drift apart.

---

## Part 10: Files in this directory

- `PACK-INTERFACE.md`: this document.
- `TEMPLATE-field.md`: starting point for a `field` pack, with the structure by kind of pack, writing rules, guidance and examples from several materials fields for each section, submission requirements and a blank template.
- `TEMPLATE-house.md`: starting point for a `house` pack, with guidance on what local convention is worth encoding.
