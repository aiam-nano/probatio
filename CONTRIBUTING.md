# Contributing

Thank you for testing Probatio. The most useful contributions, in order:

1. **Reports of what it gets wrong**: false findings, missed problems, and harness or model problems. Use the [issue forms](https://github.com/aiam-nano/probatio/issues/new/choose). Never paste text from an unpublished manuscript into an issue: describe the problem, the section and the kind of error in your own words, or show it on a published paper.
2. **Experience with particular models and harnesses**, in [Discussions](https://github.com/aiam-nano/probatio/discussions). Say which model, which harness and version, and whether the skill was named in the prompt.
3. **Field packs.** See below.
4. **Pull requests** that fix a documented problem.

## Changing the skill

The skill's files live in `manuscript-review/`. Please keep to these rules, which the skill itself was built on:

- **One change, one reason.** Say which observed behaviour the change fixes, on which model and how many runs. A single run on one model is a data point, not a pattern.
- **No new options where a fixed behaviour will do.** Where behaviour varies, fix it in the skill rather than adding a switch.
- **Keep the version in step.** The version is stated in three places that must agree: the `SKILL.md` frontmatter, the sentence opening its body, and `CITATION.cff`.
- **Keep `SKILL.md` within its limits:** the description under 1,024 characters, and the body under about 19,500 characters, so that the instructions a model must follow without opening a reference file stay within reach. Detail goes in `references/`.
- **No performance claim without its measurement,** stated with its method and date.

## Field packs

A pack is a discipline's checklist: methods-completeness requirements with the standards behind them, claim-strength conventions, red flags, and an evidence glossary. Start from `manuscript-review/packs/PACK-INTERFACE.md` and `TEMPLATE-field.md`. A pack needs:
- **named sources** for every requirement;
- **a date**, because field norms move;
- **evidence that it adds findings the core does not**, from runs with and without it on real papers.

A pack adds and never subtracts. It cannot disable a core check, relax the integrity gate or change the output contract. Packs state domain facts, not instructions to the model.

## Writing

This repository is written in British English. The rules in `manuscript-review/references/forbidden-patterns.md`, which the skill applies to its own reports, apply here too: no em-dashes as connectors, none of the banned vocabulary, no manufactured balance.

By contributing, you agree that your contribution is licensed under the repository's MIT licence, and to the [code of conduct](CODE_OF_CONDUCT.md).
