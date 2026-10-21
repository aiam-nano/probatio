# Changelog

All notable changes to this skill are recorded here. Versions follow [semantic versioning](https://semver.org/): a minor release adds a capability, a patch release fixes behaviour without adding one.

## 1.0.0 (2026-10-17)

First public release, for public testing and feedback.

- **Review pipeline:** intake reading the PDF as text layer and rendered pages; five criterion-targeted passes (story, presentation, evaluations, correctness, significance); an adversarial pass with a steelman filter; claim verification against the whole manuscript, in a separate context where the harness can start one; and a pre-delivery integrity gate.
- **Outputs:** a bounded prose report and a complete findings list. Every finding carries a verbatim quotation, its location, a severity, a concrete fix and the condition under which it would be wrong.
- **Claim verification never removes a claim.** A claim it doubts reaches the author as a question citing the evidence; a claim resting on outside knowledge is labelled. The only removal is a finding whose quotation is not on the page.
- **Review rounds.** Earlier findings are carried forward with a status, claimed changes are checked against the revised text, and declined findings are closed for good.
- **Document states.** Drafts, journal proofs (with proof-fix marks) and published versions are recognised.
- **Field-pack interface and templates.** No pack ships in this release; a graphene materials pack and its modelling companion will follow.
- **Out of scope for 1.0.0:** journal author-guideline compliance, text-overlap checks, research-assessment readiness. Asked for one, the skill says so once and runs the scientific review.

Development versions 0.1 to 0.9.2 (August to October 2026) were not released. Their evaluation is summarised in [VALIDATION.md](VALIDATION.md).
