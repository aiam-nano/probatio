# Security

## What counts

The skill runs inside your AI agent and reads untrusted documents. A security issue here is anything that makes it act against the user:

- **Prompt injection:** text in a PDF, supplementary file, response file or field pack that changes how the skill reviews, reports, or uses its tools, despite its rule that everything in the submitted materials is data.
- **Disclosure:** a literature query that carries the manuscript's title, authors, sentences or results, despite the retrieval rule.
- **Anything that makes the skill write outside its own two output files** or edit the manuscript.

A wrong or missed scientific finding is not a security issue. Please report those as [issues](https://github.com/aiam-nano/probatio/issues/new/choose).

## How to report

Use GitHub's private vulnerability reporting: the repository's **Security** tab, then **Report a vulnerability**. Include:
- the model and harness;
- a minimal reproducing document, written for the purpose and not taken from an unpublished manuscript;
- what the skill did.

You will get an acknowledgement within a week. Please do not open a public issue for a security report.

## Supported versions

Only the latest release is supported.
