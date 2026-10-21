# Intake and reading

How to get the manuscript into a state where the checks can actually be performed.

## PDF only

**This skill reviews PDFs. Nothing else.**

If the user supplies a Word document, LaTeX source, plain text, or anything other than a PDF, ask for a PDF before proceeding. Exporting one takes a moment from any authoring tool, and the review is materially better for it. Do not attempt a partial review of an unsupported format: the failure modes are silent rather than obvious, which means a review built on a bad conversion looks exactly like a good one.

Say it plainly and briefly, and offer the reason rather than just the rule:

> I work from PDFs. Could you export the manuscript and its supplementary information as PDF and attach them? A PDF gives me the figures and equations as a referee would see them, which a Word file often does not.

The supplementary information follows the same rule.

Reference material that is **not** the manuscript, such as attached data or a response file, may come in other forms, since it is not the object of review.

## Why PDF, and what is lost

The reasoning belongs here because it governs how firmly to hold the line.

**A PDF is what a referee sees.** It is the rendered artefact: figures placed, equations typeset, tables laid out, pagination fixed. Every other format is a recipe for that artefact, and reading the recipe is not the same as seeing the result.

**Figures survive.** Both raster and vector figures render when pages are rasterised. Word documents may carry figures in formats with no available decoder, and converting such a document can produce a plausible file with every figure silently missing.

**Equations survive.** Conversion routes routinely drop or mangle mathematics, leaving text where a symbol should be. A correctness pass that cannot see the equations is not a correctness pass.

**The text layer and the page can be compared.** This is what makes the concealed-instruction scan in `untrusted-input.md` work, and it needs both forms of the same file.

**It is portable.** PDF reading is available wherever this skill runs. Other formats need tooling that varies by environment, so the same skill on the same manuscript behaves differently from one place to the next.

**What is given up:** tracked changes, comments, and revision history, which live only in the authoring format. That is a deliberate trade. This skill reviews a manuscript, not its editing history, and a review that reads a colleague's unresolved comments is answering a different question.

## Read the manuscript twice, from the one file

**The extracted text layer** is the search index. Use it to find passages, count occurrences and check whether something is absent.

**The rendered page is the authority for what a quotation says.** Where the two disagree, the page wins, because the page is what a referee reads and what the author will check the quotation against. On a word-processed single-column manuscript the two rarely disagree and quoting from the text layer is safe. On a typeset document they disagree constantly, and the next section says how to tell which you have.

**The rasterised pages**, at roughly 100 to 150 dpi, carry the figures, the typeset equations, the true table layout, and anything visual that text cannot represent. Read them as images.

Both come from the same PDF, so there is no version-mismatch risk between them.

**Budget the rendering.** Rasterising pages and enlarging panels costs tool calls, and the supply within a single turn is finite. Spend it deliberately, because running out of it costs the user the artefacts, not the analysis.

One sweep of the pages carrying figures, tables or dense equations, at a single resolution in the 100 to 150 dpi range, is the baseline. Do not sweep the same pages twice at different resolutions, and do not render the whole document at high resolution on the chance that something is there.

Enlarge an individual panel only where a finding depends on a value you cannot otherwise read: an axis label, an inset statistic, a fitted parameter printed on the plot. **Roughly six enlargements is the working ceiling.** Where more panels would have to be read to settle a question, say so in the scope block and leave the question open rather than rendering your way through the paper.

Reading every page visually is better where the budget allows, and never at the cost of delivering the artefacts.

## Establish the layout before quoting anything

Extraction damage is systematic, not random, and it depends on how the document was produced. Establish which kind you have at intake and say so in the scope block.

**Word-processed, single column.** Producer metadata names a word processor. Text extracts close to reading order. Quoting from the text layer is safe.

**Typeset, single column.** Producer names a typesetting or distilling tool. Line-end hyphenation appears. Running heads and page numbers may land in the text stream.

**Typeset, two column.** The common form for a published paper and for a manuscript drafted in a two-column template. All of the above, plus the reading order problem below.

**The rendered page decides the column count.** Look at a page of body text and count the columns. The producer string, soft hyphens in the extraction and a header line repeating on every page say how the document was produced; they corroborate the page and never settle the column count on their own. A typesetting producer does not imply two columns: several journals typeset in a single column. Declaring a two-column document single column is the expensive error, because it licenses quoting from an extraction that interleaves columns.

**What goes wrong in the extraction, and what to do about it.**

*Reading order across columns.* Extraction that preserves physical layout puts both columns on the same output line, so a sentence running down the left column is chopped and interleaved with fragments of the right one. Two passages that appear adjacent in the extraction may be from different columns. **Never assemble a quotation from text that looks contiguous in the extraction without confirming on the rendered page that it is one continuous passage.** This is the one failure here that could produce a quotation that is wrong rather than merely unmatchable.

*Line-end hyphenation.* A word broken across a line carries a hyphen that belongs to the typesetting, not to the word. Quote the word whole. Where hyphenation is itself the finding, say so explicitly.

*Running heads, footers and page numbers.* These land inside sentences. Leave them out of the quotation.

*Superscript markers.* Citation numbers and footnote marks extract inline, in the middle of a phrase. Leave them out.

In every one of these cases the quotation you write will not be findable by a naive search of the extracted text. That is expected and is not a reason to change the quotation. It is a reason to have read the page.

## Verify what you actually got

Do not trust a success code. Check.

**For the text layer:** confirm extraction returned the body text rather than a handful of characters. A scanned or image-only PDF yields almost nothing; if that happens, say so and ask whether an OCR'd or original-export version exists.

**For the figures:** rasterise a page the text says carries a figure and confirm a figure is there. A page count and a clean exit tell you nothing about whether any figure rendered.

**Never describe a figure you have not verifiably seen.** Do not infer axis ranges, plotted values, trends or panel contents from the surrounding text and report them as read from the figure. If a finding needs a value from a plot you could not read, either drop the finding or phrase it as a question about what the figure shows. A fabricated reading of a figure is as serious as a fabricated quotation and much harder for the author to detect, because they know what the figure shows and will assume you saw it.

**Declare the outcome** in the report and the findings list: figures inspected and by what means, or figures not inspected and why, or partially inspected and which.

## Supplementary information

Ask for it, as a PDF, if the manuscript references it and it has not been supplied. A great deal of the methodological detail a review depends on now lives there, and a reproducibility finding written without it may simply be wrong.

State in the report which of three applies: supplementary material was reviewed; it was referenced but not supplied, so certain checks could not be completed; or the manuscript references none.

## Attached data and code

When the user supplies data files, analysis scripts or notebooks alongside the manuscript, they become part of the review. These are not manuscripts, so the PDF rule does not apply to them: take spreadsheets, notebooks or scripts as they come.

Say what you will do with them, then do it. Check that values quoted in the manuscript appear in the data as quoted. Check that sample sizes stated in the text match the rows present. Where a script computes a headline result, run it if the environment permits and confirm it reproduces the stated number. Record any discrepancy as a finding at critical severity, since a mismatch between a paper and its own data is as serious as findings get.

Where code cannot be run, say so rather than implying the check was performed.

If no data is supplied, nothing here applies and nothing need be said.

## Computational verification

Where code execution is available, **use it for every check involving a calculation**. Do not perform arithmetic mentally and report the result as verified.

This covers percentage changes and improvements claimed in the text, values derived from other values given in the paper, unit conversions, means and spreads recomputed from tabulated values, order-of-magnitude plausibility against known constants for the system, and any statistical claim recomputable from reported summary statistics.

Record in the findings list which findings rest on a recomputation, under `verified_by`. A discrepancy you have recomputed is a far stronger finding than one you suspect, and should be reported with corresponding firmness.

Where code execution is unavailable, perform the check by careful reasoning, mark the finding as unverified arithmetic, and phrase it as a query to the authors rather than an established error.

## Date the manuscript before judging its currency

Establish when the draft was written before making any finding about whether its literature coverage is current. The PDF's creation date, the dates in its own reference list, and anything the user has said all bear on this. Ask if none of them settle it.

This matters because the same reference list is a finding or no finding depending on the answer. A list ending three years ago is a real gap in a manuscript written this month and no gap at all in an archival draft or a resubmission of older work. Where the date cannot be established, phrase the finding conditionally, naming the most recent work cited and asking whether more recent literature should be added, rather than asserting a gap.

The same check often surfaces something more consequential. A draft whose metadata predates it by years may already have been published, which is the first thing the user needs to hear.

## Word counts

The output contract sets a length target and the integrity gate checks it. A language model cannot count words reliably by inspection.

Where code execution is available, count the report programmatically. Where it is not, estimate deliberately, by counting one representative paragraph and multiplying, and treat the target as approximate. Do not claim a precise count you have not performed.

## Before leaving intake

You should have: the manuscript as a PDF, read in both forms, with the figure render verified and within the rendering budget above; the layout established and its consequences for quoting understood; the date of the draft, or a recorded reason why it could not be established; the supplementary information as a PDF, or a recorded reason why not; any supplied data or code, with a stated plan for it; and the outcome of the concealed-instruction scan from `untrusted-input.md`.
