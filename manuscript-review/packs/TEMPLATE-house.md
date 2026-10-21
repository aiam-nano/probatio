---
name: TEMPLATE-house
type: house
scope: Template and guidance for writing a house pack. Not a pack; do not load it for a review.
sources: n/a
maintainer: n/a
last-reviewed: 2026-09-18
---

# House pack: template and guidance

A house pack encodes the conventions of one group, department, company or collaboration. Copy the template at the end, fill it in, and name the file after the group.

Read `PACK-INTERFACE.md` first. Everything there applies. This document covers only what is different about a house pack.

---

## What makes a house pack different

**Its authority is local.** A field pack says what the discipline expects and cites a standard. A house pack says what this group has decided, and the only thing behind it is the decision.

That difference has to survive into the report. A finding from a field pack reads "the manuscript does not report the excitation wavelength, which ISO/TS 21356-1 requires". A finding from a house pack reads "the group's convention is to report n and the error definition in every table caption, and Table 2 does not". The second names whose convention it is. The first does not need to.

**Why this matters more than it sounds.** The people most likely to have a house pack applied to their work are students and new members, and they are the people least able to tell a local preference from a disciplinary requirement. A student who learns "we always show the raw curves" as though it were a field norm will argue for it in a review one day, against a referee who has never heard of it. Encode the convention; label it as the group's.

**A house pack may be more prescriptive than a field pack**, because a group is entitled to its own standards, and less well sourced, because the source is a decision rather than a standard. Both are fine, provided the labelling is honest.

---

## What is worth encoding

The test: **would a new member of the group get this wrong, and would you correct it every time?**

Both halves. If nobody gets it wrong, it does not need writing down. If you would not correct it, it is a preference rather than a convention and should not generate findings.

Things that usually pass:

- **Reporting conventions.** "n ≥ 3 for every reported mean." "Standard deviation, not standard error, and say which." "Raw curves in the supplementary information for every fitted result."
- **Method defaults.** "Sonication parameters in full, always." "Two independent batches before any composition-property claim."
- **Data and code practice.** "Deposited before submission, with the accession number in the manuscript." "Analysis scripts in the group repository, referenced by commit."
- **Local safety or ethics steps** that go beyond the institutional minimum and that the group requires to be stated.
- **Terminology the group has settled on**, particularly where the field is loose and the group has chosen to be precise.
- **Recurring corrections.** The things you find yourself writing on every draft. These are the highest-value entries and the easiest to collect: keep a note for a month.

Things that usually fail:

- Personal writing preferences. Sentence length, word choice, whether to use the first person. These belong in a style note, not a pack that generates findings.
- Anything already in the core check set or in a field pack.
- Anything you would not defend to a referee who disagreed.
- Formatting for a particular journal, which is outside this skill's scope.

---

## Scope for a house pack

A group is a natural scope boundary, so the sizing problem from `PACK-INTERFACE.md` Part 3 mostly does not arise. Two cautions instead.

**Do not let it become a field pack.** If most of what you are writing is discipline norm rather than group decision, write a field pack, or write both and keep them separate. A house pack that silently contains field requirements loses the labelling distinction that justifies its existence.

**Do not let it become a project pack.** Conventions that apply to one project or one material system are too narrow, and they will fire wrongly on the group's other work. Either keep the pack to what applies across the group, or write separate packs per sub-area and name them clearly.

---

## Length

Shorter than a field pack. **Target 100 to 150 lines; ceiling 300.**

A group's genuine conventions are not numerous. A long house pack usually means field norms have crept in, or preferences have.

---

## Using it alongside a field pack

Both can be named: "review this with the graphene pack and the group pack". They are additive, and the core resolves overlap by preferring the more specific requirement.

Where the two conflict, which happens when a group has chosen to exceed a field norm, the house pack's requirement stands and the finding says so: "the field requires X; the group's convention is the stricter Y, which this does not meet". Never report a field norm as violated when the group's stricter rule is what was missed.

---

## Template

```markdown
---
name: <group-slug>
type: house
scope: <whose conventions these are, and over what work>
sources: group decision; <any internal document, with its date>
maintainer: <who to ask>
last-reviewed: <YYYY-MM-DD>
---

# <Group> pack

## 0. Scope and authority

Covers: <whose work, and what kinds of paper>.
Does not cover: <explicitly: other groups, other project areas, field norms>.

**Authority.** These are the conventions of <group>, decided by <how and when>. They are
not field requirements and are not standards. Findings generated from this pack must say
whose convention is at issue. Where a convention here is stricter than the field's, that
is deliberate.

## 1. Reporting conventions

### <Convention>
**Requirement:** <what must be reported or done>
**Why:** <one line: the reason the group decided this>
**Severity:** <critical if it makes results uninterpretable within the group's standards;
major if it leaves them incompletely specified; minor otherwise>

### <Convention>
...

## 2. Method defaults

<Standing decisions about how work is done and reported. Same three fields.>

## 3. Recurring corrections

<The things you correct on every draft. The highest-value section; keep it concrete and
keep examples short.>

## 4. Data, code and deposition

<What must exist, where, and what must appear in the manuscript.>

## 5. Terminology

<Where the group has chosen precision the field does not enforce.>

## 6. Not our business

<Things explicitly left to the author's judgement, so the pack does not generate findings
about them. An underused section: saying what you do not care about is as useful as
saying what you do.>

## 7. Changelog

- YYYY-MM-DD: <what changed, why, who decided>
```

---

## Testing a house pack

The tests in `PACK-INTERFACE.md` Part 8 apply, with one addition and one substitution.

**Substitution.** The false-positive test uses a paper the group published and was happy with, rather than a paper that passed review elsewhere. Findings the pack generates on the group's own accepted work are either conventions the group does not actually hold, or conventions it holds and has been breaching, and both are worth knowing.

**Addition: the new-member test.** Give the pack to someone who joined recently and ask which entries they did not know. Entries everyone knew do not need to be there. Entries nobody knew are worth checking are actually conventions rather than one person's habit.

---

## A caution on scope creep

A house pack is the easiest of the three types to write and the easiest to fill with things that should not generate findings. The discipline is the test at the top: would a new member get this wrong, and would you correct it every time.

Anything failing that test makes the pack longer, makes reviews noisier, and makes the entries that matter harder to see.
