# Probatio 1.0.0

The first public release of Probatio, an Agent Skill (id `manuscript-review`) that reviews your own scientific manuscript before the referees do. It is released for public testing: please tell us what it gets wrong.

**Install:** download `manuscript-review-1.0.0.zip` below and upload it to your agent (in the Claude app: Settings → Capabilities → Skills). For other harnesses, see the [README](https://github.com/aiam-nano/probatio#install). Then attach a PDF and ask: `@manuscript-review review this manuscript using the manuscript review skill.`

**What you get:**
- a prose report naming the problems a referee would raise, each with a quotation and a concrete fix, ordered by consequence;
- a complete findings list;
- the next round, run on your revision with your response, checks what you addressed.

**How well it works** (internal, model-graded estimates; human adjudication to be reported shortly in a preprint; details in [VALIDATION.md](https://github.com/aiam-nano/probatio/blob/main/VALIDATION.md)), with Claude Opus 5.5:
- **Planted errors:** 96% found in a single run.
- **Known errors in 30 recent preprints:** 84% found per run.
- **Precision:** about 9% of the claims it states as fact turn out false. Doubtful claims arrive as questions, and no real error is removed.
- **Models:** results differ widely by model; see the comparison in the README.

**Not in this release:** journal author-guideline checks, text-overlap checks, research-assessment readiness, and field packs. A graphene materials pack will follow.

**Feedback:** [issue forms](https://github.com/aiam-nano/probatio/issues/new/choose) for false findings, missed problems and bugs, and [Discussions](https://github.com/aiam-nano/probatio/discussions) for everything else. Never paste text from an unpublished manuscript.
