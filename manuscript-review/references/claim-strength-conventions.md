# Claim-strength conventions

Most overclaiming is not dishonesty. It is a verb chosen for emphasis and never revisited. Checking claim strength is cheap, it catches real problems, and the fix is usually a single word. That combination makes it some of the highest-value feedback a review can give.

The question in every case: **what would this verb have to be true for, and is that what was shown?**

## The ladder

From weakest to strongest, for a claim about a relationship between two things:

| Verb | What it requires |
|---|---|
| is consistent with | The observation does not contradict the claim. Very weak; honest for single observations. |
| suggests / indicates | A pattern is present, alternatives not excluded. |
| shows / provides evidence that | A designed comparison, with controls, supports the claim. |
| demonstrates / establishes | Alternatives have been excluded by design or explicit test. |
| proves | Reserve for mathematics. In experimental work this is almost never earned. |

A correlation supports "is associated with". It supports "causes" only where the design licenses a causal reading, and the review should ask explicitly what licenses it.

## Specific words that warrant a check

**"First", "novel", "unprecedented".** A priority claim is checkable and gets checked, by reviewers if not by us. Where retrieval is available, check it. Where it is not, flag it as a claim requiring the authors' own verification. "Among the first" is usually both true and safe.

**"Significantly".** Must mean statistically significant, with a stated test, or be replaced with "substantially", "markedly", or a number. This ambiguity is common and genuinely misleads readers.

**"Optimal", "optimised".** Optimal against what objective, over what search space? Usually the honest word is "improved" or "tuned".

**"Scalable", "general", "universal".** Demonstrated over what range, and what licenses extrapolation beyond it? A method shown at two conditions is not thereby general.

**"Robust".** Against which perturbations, tested how? Untested robustness claims are a routine major finding.

**"Confirms", "validates".** These presuppose the prior claim was correct. Where the work tests rather than confirms, say tests.

**"Clearly", "obviously", "evidently".** These do no evidential work and often mark exactly the places where evidence is thin. Their presence is a signal worth following.

## Abstract versus body

Overclaiming concentrates in abstracts, where compression pushes hedges out. Check every claim in the abstract against what the results section actually reports, and treat a mismatch as a real finding rather than a stylistic quibble. The abstract is what most readers take away, and it is what reviewers read first and most sceptically.

## Scope creep in the discussion

The other concentration point is the final paragraphs, where a bounded result is generalised into an application, a field, or a societal implication. Check that each step outward is licensed by something. The test: if a reader acted on the final sentence, would the results in the paper have supported them?

## Writing the finding

Name the verb, quote the sentence, say what would be needed to earn it, and give the replacement.

> The abstract states that the approach "demonstrates superior performance across material systems", where results are reported for two systems under a single processing condition. Demonstrating generality across systems would require either a wider sample or an argument for why these two are representative; without that, "improves performance in both systems examined" states what was shown and costs nothing.

This is the shape to aim for: specific, quoted, with the fix already written.
