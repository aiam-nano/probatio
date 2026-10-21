# Field pack template

The starting point for writing a `field` pack: a pack that states the norms of a discipline, with external authority behind them. For a pack stating one group's local conventions, use `TEMPLATE-house.md` instead.

**Read `PACK-INTERFACE.md` first.** It sets the rules every pack must follow. This template turns those rules into a structure, and shows each section with short examples from several materials fields, so that authors working in different specialisms produce packs that behave the same way.

**The examples are illustrations of form, not vetted requirements.** They were written to show what a good entry looks like. None has been reviewed by a specialist in its field, and none may be copied into a pack without the author checking it and sourcing it.

A worked example, a graphene material pack and its modelling companion, is to be published separately.

---

## Part A: Before you start

**1. Size the domain.** Apply the test in `PACK-INTERFACE.md` Part 3: does a competent generalist routinely get these things wrong, and do the techniques and claim types recur together in the same papers? If two groups of sections would rarely both apply to one paper, you are writing two packs.

**2. Decide what kind of pack it is.** The kind decides which sections are required (Part B).

**3. Collect your sources before you write.** Standards, reporting guidelines, consensus statements, and the reviews that establish field conventions. Record each with its year and, for standards, the clauses you rely on. A requirement you cannot source is either labelled a field convention or left out.

**4. Line up a reviewer and test papers.** At least one specialist who did not write the pack. At least three papers for testing (`PACK-INTERFACE.md` Part 8): one where the pack should add findings, one strong published paper for the false-positive test, and one just outside scope for the wrong-paper test.

**5. Budget the length.** Hard ceiling 500 lines or about 5,000 words; target 200 to 300 lines. Spend the budget on the technique map, the red flags and the glossary. If it will not fit, split the pack.

---

## Part B: Kinds of pack, and which sections they need

| Section | Material pack | Method pack | Application pack |
|---|---|---|---|
| | *a material family, e.g. graphene, MOFs, metallic glasses* | *a family of techniques, e.g. electron microscopy, atomistic modelling* | *a class of use, e.g. EMI shielding, Li-ion cells, heterogeneous catalysis* |
| 0. Scope | required | required | required |
| 0.1 How to read the citations | required, fixed wording | required, fixed wording | required, fixed wording |
| 1. Identification | required | optional: variants of the method | optional: what the device or test object is |
| 2. Production and residues | required | not used | optional |
| 3. Form, specimen and state | required | not used | required: the test configuration |
| 4. Process history | required | not used | optional |
| 5. Which technique answers which question | required | replaced by 5M | required |
| 5M. Principles and method map | not used | required | not used |
| 6. Physical bounds | recommended | optional | recommended |
| 7. What a downstream claim needs | recommended | optional | recommended |
| 8. Claim-strength conventions | required | required | required |
| 9. Red flags | required | required | required |
| 10. Evidence-adequacy glossary | required | required | required |
| 11. Contested norms | required, and not empty | required, and not empty | required, and not empty |
| 12. Changelog | required | required | required |

Section numbers may differ in a finished pack; keep the order and the headings recognisable. Omit a section that does not apply rather than leaving it empty, except section 11.

---

## Part C: Writing rules that apply to every section

**Checkable, not aspirational.** "Report the excitation wavelength, the laser power at the sample and the number of spectra" is a requirement. "Ensure Raman is properly reported" is not.

**Labelled.** Every requirement carries one of the three labels defined in section 0.1. A label is a claim about authority, and a reviewer will check it.

**Scoped where it is used.** If a standard covers only part of your domain, say so at every point you cite it, not only in the preamble. The first test of the graphene pack found a model citing a standard correctly by name and incorrectly by scope, because the scope was stated once at the top and not where the citation sat.

**Conditions attached.** A value, threshold or range is interpretable only with the measurement conditions it depends on. State them beside it.

**Ranges ask; bounds assert.** A value outside what is typical for a material is a question for the authors, because an unusual result is sometimes the point of the paper. Only a physical or arithmetic bound supports reporting an error.

**Severity for your own items only.** Indicate critical, major or minor for the requirements in the pack. Do not change how the core grades anything else.

**Domain facts, not instructions.** State what the field requires and why. Do not tell the model how to behave, what tone to use, how to format the report, or to "always flag" anything. Where a point should be raised as a question rather than a finding, section 11 is the place, and that phrasing is the one exception the interface allows.

**No duplication of the core.** Internal consistency, arithmetic, uncertainty reporting, figure quality and literature currency are already checked on every paper.

**No reproduced standard text.** Name the document and clause, and paraphrase what it covers in a line. Packs are published openly and cannot carry copyrighted text.

---

## Part D: The sections, with guidance and examples

### Frontmatter

```yaml
---
name: <slug, matching the filename>
type: field
scope: <one line: what this covers, and its companions if any>
sources: |
  <each standard, guideline or consensus statement, with year>
  <any in development, stated as cited nowhere as authority>
maintainer: <name>
last-reviewed: <YYYY-MM-DD>
---
```

List documents in development separately and say they are not cited as authority. A committee draft cited as a published standard was the most serious error found in the first version of the graphene pack.

### 0. Scope

**Purpose.** Tells the model, and a human, when this pack applies. The exclusions matter more than the inclusions, because they stop the pack being loaded on the wrong paper.

**Include:** what the pack covers, by name and by form; what it explicitly does not cover, including neighbouring materials, applications and techniques; any companion pack and how the two divide the ground; and one paragraph on **the problem this pack exists for**, meaning the failure a generalist most often misses in this field.

**Examples.**

- *Li-ion battery electrodes (application pack):* covers intercalation electrodes and cells for Li-ion and Na-ion chemistries, from half-cell to pouch cell. Does not cover solid-state electrolytes, lithium–sulfur, or supercapacitors, whose failure modes differ. The problem it exists for: performance reported under conditions, such as very low mass loading and excess electrolyte, that no practical cell would meet.
- *Metal additive manufacturing (material and process pack):* covers laser and electron-beam powder bed fusion and directed energy deposition of metallic alloys. Does not cover polymer or ceramic additive manufacturing, or binder jetting. The problem: properties reported without the build orientation, porosity or heat-treatment state that determine them.
- *Metal–organic frameworks (material pack):* covers crystalline porous coordination frameworks as material. Does not cover their applications in gas separation or catalysis, which have their own packs. The problem: a framework named by its code while its activation state, defect density or post-exposure crystallinity is never shown.

### 0.1 How to read the citations in this pack

**Use this wording unchanged**, so that every pack means the same thing by the same label:

> **`Standard:`** means a published standard or guide covers the subject of the requirement, and the document is named, with the clause where known. It asserts that the document covers the subject, not that it mandates every detail stated here.
>
> **`Field convention:`** means established practice with no published standard behind it. A finding resting on a field convention is raised as a convention, never as a requirement, and the report says which it is.
>
> **`Physical bound:`** means a limit set by physics or arithmetic. A value past it is an error unless the paper explains why the bound does not apply.
>
> **Typical ranges** are not a label. A value outside what is usual for the material and route is a question for the authors, never an error.

Then add any scoping points specific to your field's standards, for example a standard that covers only some members of the family.

### 1. Identification of the object of study

**Purpose.** A result that cannot be attached to a specified material, device or method is not a result. This section states what a paper must report for its object to be identified, and what the name it uses actually asserts.

**Include:** the vocabulary standard, if one exists; the minimum reportable set that identifies the object; where commercial material is common, that a supplier specification is a starting point and not evidence; and naming that makes a checkable claim.

**Examples.**

- *Polymers:* grade and supplier, or synthesis; number- and weight-average molecular weight with dispersity, and the method and calibration used; tacticity or copolymer composition where it matters. A polymer named by trade name only is not identified.
- *Alloys:* measured composition, not nominal, including interstitials where they control properties, as oxygen and nitrogen do in titanium alloys; the analysis method.
- *MOFs:* phase identity by powder diffraction against the simulated pattern; the activation state at measurement; defect or missing-linker content where properties depend on it.

**Severity:** usually critical if absent, because everything downstream depends on it.

### 2. Production route and what it leaves behind

**Purpose.** Each route leaves a signature: residues, dopants, defects, by-products. Papers often attribute to the material what the route put there.

**Include:** for each common route, what it leaves and what measurement detects it; purification steps and what they were meant to remove.

**Examples.**

- *Colloidal nanoparticle synthesis:* capping ligands and surfactants retained on surfaces, which change catalytic and electronic behaviour; the ligand-removal step and evidence it worked.
- *Solvothermal MOF synthesis:* solvent retained in pores and unreacted linker, both of which inflate mass and depress measured porosity.
- *Sol–gel ceramics:* residual carbon and hydroxyl groups from organic precursors, and the calcination that should remove them.

### 3. Form, specimen and state

**Purpose.** The same material in a different form, or the same device in a different test configuration, is a different measurement.

**Include:** the forms or configurations common in the field; for each, the minimum reportable set; which properties are effective properties of the object rather than intrinsic properties of the material; direction for anisotropic properties.

**Examples.**

- *Battery cells:* half-cell against lithium metal, full cell, or pouch; active mass loading per area; electrode porosity and thickness; electrolyte volume relative to capacity; negative-to-positive capacity ratio in full cells.
- *Mechanical testing:* specimen geometry and the test standard it follows (for example ASTM E8/E8M for metals, ISO 527 for plastics); gauge length; strain rate; for additively manufactured parts, orientation relative to the build direction.
- *Thin films:* substrate and any epitaxial strain it imposes; thickness and how it was measured; whether properties were measured in-plane or out-of-plane.

### 4. Process history

**Purpose.** A material characterised as received and then processed on the way to the final object is no longer the material characterised. This is one of the most consequential gaps in materials papers and one of the least often checked.

**Include:** a table of processing steps against what each can change and how the change would show; the minimum reportable set (the full history from characterised material to final object); what counts as evidence of the state after processing; and proportionate severity. Where the processed material cannot be measured directly, say what alternative evidence suffices, such as a process blank.

**Examples.**

- *Metal additive manufacturing:* as-built against stress-relieved, hot-isostatically-pressed or aged states; as-built surface against machined; mechanical properties are meaningless without the state.
- *Polymer processing:* thermo-oxidative degradation and molecular-weight loss during extrusion or moulding; physical ageing before a glass-transition measurement; moisture uptake in hygroscopic polymers before testing.
- *Hydrogels for biological use:* sterilisation by autoclave, gamma irradiation or ethanol can change crosslink density and swelling; properties measured before sterilisation may not describe what the cells meet.
- *Supported catalysts:* reduction pre-treatment, and sintering or leaching during reaction; characterisation after reaction, not only before.

### 5. Which technique answers which question

**Purpose.** A map of applicability, not a protocol. For each question a paper asks of its material or device, which technique can answer it and what makes the answer interpretable.

**Format:** a table.

| Question | Techniques that answer it | What makes the answer interpretable | Basis |
|---|---|---|---|

**Examples of rows.**

- *Perovskite photovoltaics:* "What is the power conversion efficiency" · current–voltage under simulated AM1.5G illumination · scan direction and rate, aperture mask area, light-source calibration against a reference cell, stabilised output at maximum power point, and short-circuit current cross-checked against the value integrated from external quantum efficiency · IEC 60904 series for photovoltaic measurement.
- *Heterogeneous catalysis:* "What is the intrinsic activity" · turnover frequency · how active sites were counted; conversion kept in the differential regime; absence of mass- and heat-transport limitations shown; carbon balance · Field convention.
- *Electrocatalysis:* "What is the overpotential at a given current density" · polarisation curves · whether and how much iR correction was applied; reference electrode calibration against the reversible hydrogen electrode; normalisation to geometric area, mass or electrochemically active area; scan rate; counter-electrode material · Field convention.
- *Microporous solids:* "What is the specific surface area" · nitrogen or argon physisorption with BET analysis · the pressure range chosen and whether it meets the consistency criteria for microporous materials; activation conditions · ISO 9277.

**Severity:** critical where the technique cannot answer the question asked of it; major where it can and the reporting is incomplete.

### 5M. Principles and method map (method packs only)

**Purpose.** For a pack about a family of methods rather than a material, the equivalent of section 5: which method answers which question, and how each is misapplied.

**Include:** a few principles that apply to every method in the pack, each stated as a checkable expectation; the minimum reportable set for any study using the methods, citing a documentation standard where one exists; then a table.

| Method | Questions it can answer | What makes the answer interpretable | How it is misapplied in this field |
|---|---|---|---|

**Examples.**

- *Electron microscopy:* principle, that images are representative only as far as the number of regions examined supports; row, beam-sensitive materials such as MOFs, halide perovskites and polymers, where the electron dose must be reported and damage ruled out before structure is interpreted.
- *Atomistic modelling:* principle, that the modelled material must be the measured material; row, density functional theory, misapplied when a semilocal functional's band gap is taken quantitatively.
- *Mechanical testing at small scale:* principle, that size effects must be addressed before small-specimen values are compared with bulk; row, nanoindentation, misapplied when hardness is converted to yield strength without justifying the conversion factor.

### 6. Physical bounds on reported values

**Purpose.** Values that cannot be right, and values that cannot mean what the paper says without an explanation. These produce the most mechanical, most checkable findings a pack can offer.

**Format:** a table with the quantity, the bound, what counts as an error, and what counts as a strong question. Give textbook values only, with their conditions.

**Examples.**

- *Photovoltaics:* efficiency above the detailed-balance limit for a single-junction absorber of the stated band gap is an error. External quantum efficiency above 100% in a device with no carrier-multiplication mechanism is a strong question.
- *Batteries:* specific capacity above the theoretical capacity of the active material is a strong question, since other contributions such as conductive additives or electrolyte decomposition are usually responsible. Sustained coulombic efficiency above 100% is a strong question.
- *Catalysis and electrochemistry:* Faradaic efficiencies summing above 100% are an error. A carbon balance that does not close within the stated tolerance is a strong question.
- *Ceramics and powder metallurgy:* relative density above 100% of theoretical is an error, usually a wrong theoretical density.

**Severity:** an error is critical where a central claim rests on the value, major otherwise.

### 7. What a downstream claim needs from this domain

**Purpose.** Connects packs. A material pack states what material characterisation each class of application claim rests on. An application pack states what it needs from the material, and names the material packs that supply it.

**Examples.**

- *Battery application pack, cell-level energy density:* the masses of every cell component, including electrolyte, separator, current collectors and casing. Energy density per mass of active material alone is not a cell-level claim.
- *Polymer nanocomposite material pack, flame-retardancy claims:* filler dispersion shown, loading verified, and the matrix-only control processed identically.
- *Biomaterials, any claim of use in contact with cells:* sterilisation method, endotoxin level, and the material's state at the point of contact.

### 8. Claim-strength conventions

**Purpose.** What evidence the field requires before a class of claim is earned, and which terms have a precise meaning that is used loosely. Often short, and often the most valuable section.

**Examples.**

- *"Stable" in perovskite photovoltaics:* earned only against a stated stress protocol, duration, encapsulation state and metric; the ISOS consensus protocols define the common stress conditions.
- *"Single-atom catalyst":* atomic dispersion shown directly, by aberration-corrected microscopy and by absence of metal–metal scattering in X-ray absorption, not inferred from missing diffraction peaks.
- *"Biocompatible":* one short-term cytotoxicity assay on one cell line supports "not cytotoxic under the test conditions"; biocompatibility in the sense of ISO 10993 is a set of endpoints chosen for the intended contact.
- *"Superhydrophobic":* a high static contact angle together with low contact-angle hysteresis or roll-off angle; the static angle alone does not earn it.

### 9. Red flags

**Purpose.** The failures that look fine unless you know the field. The highest-value content in most packs.

**Include:** controls standard in the field and conspicuous by absence; artefacts mistaken for findings; conditions without which a result is meaningless; known confounds. Close with any core check that does not apply to the field, and why; usually none.

**Examples.**

- *Batteries:* high specific capacity reported at very low areal loading and presented as practical; excess lithium in half-cells masking degradation.
- *Electrocatalysis:* a platinum counter electrode in hydrogen evolution studies, where dissolved platinum can deposit on the working electrode; electrochemically active area from double-layer capacitance using an assumed specific capacitance, presented as measured.
- *Additive manufacturing:* density by the Archimedes method alone, which gives one bulk value and cannot show the size, shape or location of pores; tensile specimens not following a standard geometry.
- *Nanomaterials in cell studies:* colorimetric viability assays whose readout the material itself interferes with, for example by adsorbing the dye.

### 10. Evidence-adequacy glossary

**Purpose.** For each common claim, what counts as adequate support and what does not. A table.

| Claim | Minimum adequate evidence | Does not suffice |
|---|---|---|
| *Record efficiency (photovoltaics)* | *Independent certification* | *In-house measurement alone* |
| *Intrinsic catalytic activity* | *Turnover frequency with a site count and transport limitations excluded* | *Mass activity alone* |
| *Fully dense (additive manufacturing)* | *Porosity by X-ray tomography or metallography over a stated volume* | *Archimedes density alone* |
| *Cell-level energy density (batteries)* | *All component masses included* | *Active-material mass only* |

### 11. Contested norms

**Purpose.** Where the field disagrees with itself. Points listed here are raised as questions, not findings. An empty section is a warning sign: most fields have at least one live methodological argument.

**Examples.**

- *Perovskite stability:* which ISOS stress level, and what duration, is enough to call a device stable.
- *Electrocatalysis:* whether activity should be normalised to geometric area, mass, or electrochemically active area, each of which flatters different materials.
- *High-entropy alloys:* how many principal elements, and what composition range, the term requires.
- *Microporous solids:* how far BET areas mean anything for ultramicroporous frameworks, even when the consistency criteria are met.

### 12. Changelog

Two or three lines per revision: what changed, why, and the date.

---

## Part E: Submitting a pack

Send the maintainer:

1. **The pack**, following this template, named `<slug>.md`.
2. **Its sources**, as listed in the frontmatter, with anything you could not verify flagged.
3. **Your test results** from `PACK-INTERFACE.md` Part 8: the delta test, the false-positive test and the wrong-paper test, with the papers identified and what the pack added or wrongly flagged.
4. **Your reviewer's name**, and whether they and you are happy to be acknowledged.

Packs are released under the repository's MIT licence. Do not include unpublished data, and do not include text from standards or papers.

---

## Part F: Blank template to copy

````markdown
---
name: <slug>
type: field
scope: <one line>
sources: |
  <standards and guidelines, with years>
  <documents in development, cited nowhere as authority>
maintainer: <name>
last-reviewed: <YYYY-MM-DD>
---

# <Domain> pack

## 0. Scope

**Covers:** <what, by name and form>.
**Does not cover:** <neighbouring materials, applications, techniques, explicitly>.
**Companion packs:** <if any, and how the ground is divided>.
**The problem this pack exists for:** <the failure a generalist most often misses>.

## 0.1 How to read the citations in this pack

<The fixed wording from the template, unchanged, then any field-specific scoping points.>

## 1. Identification

**Minimum reportable set:** <...>
**Standard:** / **Field convention:** <...>
**Severity:** <...>

## 2. Production route and what it leaves behind

<For each route: what it leaves, what detects it, severity.>

## 3. Form, specimen and state

### 3.1 <Form or configuration>
**Minimum reportable set:** <...>
**Standard:** / **Field convention:** <...>
**Severity:** <...>

## 4. Process history

| Processing step | What it can change | How the change shows |
|---|---|---|

**Minimum reportable set:** <...>
**Evidence of the state after processing:** <...>
**Severity:** <...>

## 5. Which technique answers which question

| Question | Techniques that answer it | What makes the answer interpretable | Basis |
|---|---|---|---|

**Severity:** <...>

## 6. Physical bounds on reported values

| Quantity | Bound | Error | Strong question |
|---|---|---|---|

## 7. What a downstream claim needs

| Class of claim | What it rests on |
|---|---|

## 8. Claim-strength conventions

<Terms and what earns them.>

## 9. Red flags

<Each as a bold one-line name, then two or three sentences.>

### Core checks not applicable to this field

<Usually: none. The core check set applies in full.>

## 10. Evidence-adequacy glossary

| Claim | Minimum adequate evidence | Does not suffice |
|---|---|---|

## 11. Contested norms

Raise these as questions, not findings.

<Each dispute, with both positions.>

## 12. Changelog

- <YYYY-MM-DD>, version 1. First version.
````

For a method pack, replace sections 1 to 5 with **5M. Principles and method map**, and keep 6 to 12.
