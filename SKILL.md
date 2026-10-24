---
name: gugu-report-skills
description: Create, revise, typeset, and verify LaTeX/PDF undergraduate/graduate course reports, lab reports, paper reviews, method comparisons, and project/practice reports from course requirements, rubrics, templates, slides, papers, code, images, notes, and existing drafts. Use when the user asks to complete an academic report, convert requirements into a LaTeX report, enforce report formatting/font/layout requirements in LaTeX, compare papers within a report, include code/results/figures/tables in a report, manage report citations, or visually inspect the final report PDF.
---

# gugu-report-skills

## Core Workflow

1. Establish the priority order.
   - For report decisions, treat explicit course requirements/rubrics/templates as the highest priority: topic, section structure, page count, fonts, margins, line spacing, citation style, required figures/tables, naming, and submission format.
   - If course requirements conflict with prior defaults, obey the course requirements.
   - If the course provides an explicit template or layout, preserve it as the source of truth. Use default styling only to fill unspecified gaps; do not replace a clear course template because the default style looks cleaner.
   - If a requirement is missing or ambiguous, use the defaults in `references/default-style.md`.
   - If a user gives a direct override after the requirements are known, follow the newest user instruction unless it would violate a hard course requirement; surface the conflict clearly.

2. Establish local rules and available tools.
   - Read project `AGENTS.md` and `~/.codex/AGENTS.md` when present.
   - For PDFs, inspect cheaply with Poppler before deeper parsing:
     `pdftotext -layout -enc UTF-8 file.pdf -`, `pdfimages -list file.pdf`, and `pdftoppm -png -r 180 file.pdf pages/page`.
   - Use OCR/MinerU only for scanned PDFs, dense multi-column papers, tables, formulas, or failed text extraction.

3. Convert requirements into a checklist and identify the report type.
   - Extract required topic, comparison targets, format, page limits, grading points, optional tasks, and submission artifacts.
   - Separately list formatting requirements: document class/template, paper size, margins, font family/size, line spacing, heading style, title page, table of contents, abstract/keywords, citation style, figure/table caption style, bibliography style.
   - Identify what the report must answer, not just what it must summarize.
   - Classify the task as one or more of: course paper, paper review/method comparison, lab report, or project/practice report. Use the matching structure guidance from `references/default-style.md`.
   - Decide front matter by report type and requirements. Do not mechanically add abstract, keywords, or table of contents to every report; short lab reports often start with course metadata, experiment metadata, or group division instead.
   - Do not expose the internal requirements checklist as the report's opening content. Checklists guide the work, but the delivered report should begin like a real academic report: cover/title information, abstract when appropriate, a short task/background note when useful, then navigation/body.
   - If a table of contents is included, it must start on its own page and the body must start after it. Never squeeze a table of contents under the title page content just to reduce whitespace.
   - Keep a visible checklist during work: requirements, outline, draft, LaTeX, compile, rendered PDF check, final artifact. The checklist is for the working response only; never copy requirement checklists, planning notes, material status, TODOs, or production reminders into the final `.tex` report unless the course explicitly requires such a table.

4. Build source understanding before writing.
   - Read the course PPT/rubric, template, existing report/slides, target papers, code, data descriptions, result screenshots, and figures the user provides.
   - For paper/method reports, capture each paper's problem, route, core mechanism, key formula meaning, experiments, limitations, and relation to other methods.
   - For lab reports, capture experiment purpose, theory, environment/data, method/steps, key code, result figures/tables, analysis, problems encountered, and summary.
   - Prefer comparison axes that match the task, such as paradigm, assumptions, implementation cost, efficiency source, quality tradeoff, result reliability, and applicable scenarios.

5. Plan evidence and visual material before drafting.
   - User-provided course templates, requirements, real experiment results, screenshots, generated plots, code outputs, and instructor materials have highest priority.
   - For lab/project reports, if runnable code or data are available, try to produce real result plots/tables before using placeholders.
   - For paper/method reports, when architecture diagrams, examples, or result tables are needed, prefer authoritative original assets: paper arXiv source, official repositories, and course PPT figures. Preserve vector PDF/SVG when possible and label figure sources.
   - If no real image/result exists but the report needs a visual slot, use a clearly labeled placeholder or self-made schematic. Never fabricate experiment results, data, citations, or screenshots.
   - For code, include only key snippets in the main text; put long code in an appendix or separate file reference.

6. Draft the report around an argument.
   - Use an academic but readable Chinese style.
   - Do not merely retell materials; explain why each method, experiment, figure, table, or code snippet matters.
   - Explain formulas intuitively: state what each term controls and why it matters.
   - For lab/project reports, connect implementation choices to observed results; include failures or limitations when they affect interpretation.

7. Typeset every report in LaTeX.
   - Always produce auditable `.tex` source and a compiled PDF as the primary artifacts.
   - Use course-provided `.tex`, `.cls`, or `.sty` files directly when available.
   - Treat course-provided `.docx` or PDF templates as layout sources to reproduce or embed in LaTeX, not as an alternative authoring format.
   - If no template exists, use the default LaTeX style from `references/default-style.md`.
   - When a template is explicit, keep its required title page, margins, fonts, headings, numbering, spacing, caption style, and bibliography style. Add helper packages or local fixes only when they do not change the required appearance.
   - Keep style choices stable and explicit in the source so they can be audited later.
   - Do not invent fonts, margins, date formats, or citation styles when the course specifies them.
   - Prefer the LaTeX route that compiles reliably in the current environment. A polished preamble is not acceptable unless it actually compiles.
   - Use explicit page breaks for front matter: title/cover page as appropriate, `\clearpage\tableofcontents\clearpage` when a TOC is present, then the first body section. A TOC may span pages, but it should not share a page with title prose, metadata tables, or the start of the body.

8. Polish code, figures, and tables by rendered pages, not by source guesswork.
   - Avoid `[H]` unless the figure/table must stay exactly there; it often creates blank space. Every remaining `[H]` figure/table must be recorded in the page review ledger with its page number, why `[H]` was necessary, and the previous/current/next page status after rendering.
   - Follow conservative academic layout conventions: figures centered with captions below; tables centered with captions above; surrounding text explains the result before or after the float.
   - Use tables only when tabular structure adds real value: numeric results, parameter grids, direct comparisons, ablations, member contributions, experiment metadata, or a compact chronology. Do not use a table as a container for paragraph-length prose, reading notes, planning reminders, or "could add image/source" columns.
   - Treat `longtable` as an exception, not a default. A multi-page table belongs in the main text only when the course explicitly asks for a full table/timeline or the table is itself a central result. Otherwise summarize the main pattern in prose, keep a small representative table, or move the full table to an appendix/supplement.
   - Do not turn a course report's source/material inventory into a multi-page body table. Summarize material classes and selection criteria in prose or a compact overview table; cite analyzed sources in context; move exhaustive inventories to references, an appendix, or submission notes.
   - Body tables should support reading, not archiving. Appendices can carry complete parameter lists, coding sheets, material indexes, long questionnaires, or full timelines when they are useful for audit; the main body should remain readable without depending on those inventories.
   - Before using any table likely to cross a page, ask whether the reader benefits from scanning rows. If most cells contain complete sentences or the table reads like a materials checklist, convert it to paragraphs, a staged bullet timeline, or a short overview table.
   - Do not include internal workflow columns such as "可配视觉材料", "待补素材", "备注", or source-hunting notes in the final report unless the assignment explicitly asks for them.
   - For a sparse page with only one figure/table cluster, first adjust content and layout: move nearby analysis text, tune figure width, or revise the surrounding explanation so the page carries useful content.
   - Use side-by-side `minipage` layouts only for comparable material in the same visual unit: two subfigures of similar size, two related sub-tables of similar height, or direct A/B comparisons. Do not pair a plot with a tall table, mix unrelated results, or create diagonal/stair-step pages just to fill whitespace.
   - For two related sub-tables, usually place the sub-tables side by side inside one `table` with `minipage`; do not force unrelated tables into one row.
   - Use `booktabs`, consistent captions, and stable widths. Check that no table overflows and no image caption crosses awkwardly.
   - For code blocks, default to a clean white background with a thin frame, line numbers, wrapping, and readable monospace text. Do not add gray/color fill, shaded boxes, `tcolorbox`, `mdframed`, or other filled code containers unless the course template explicitly requires them.
   - When the code language is known, set the listing language explicitly, such as `language=C++`, `language=Python`, or `language=bash`; otherwise keyword highlighting may not appear. Use modest syntax highlighting: blue bold keywords, gray comments, readable strings, black identifiers, and no colored background. Do not use a colorful IDE theme in a course report.
   - Prevent awkward code-listing page breaks. A short listing should either fit as one visual unit or be pushed to the next page with `\Needspace{...}` or a deliberate page break before the listing. Never leave only the caption or the first one to three code lines at the bottom of a page with the rest on the next page. After using `\Needspace` or a manual page break, re-check the previous page for excessive bottom whitespace and move nearby explanation text if needed. For long listings, split the snippet into meaningful pieces, move it to an appendix, or cite the source file instead; keep a short explanation and appendix/source reference in the main text.
   - For code blocks, check line wrapping, line-number spacing, Chinese/comment rendering, monospace font behavior, and page breaks.
   - For figures/tables, check clarity, source/caption, relevance to the argument, and whether any placeholder remains.
   - Do not solve page density by arbitrarily shrinking the bibliography, body font, margins, or line spacing. Preserve the bibliography font and spacing unless the course template or citation style explicitly says otherwise.

9. Verify the PDF visually before delivery.
   - Compile until cross-references settle.
   - Run Poppler extraction and rendering:
     ```sh
     pdftotext -layout -enc UTF-8 report.pdf review/text.txt
     pdfimages -list report.pdf > review/images.txt
     pdftoppm -png -r 180 report.pdf review/page
     ```
   - Create or inspect a full-document page overview after rendering. For short course reports, inspect every rendered page thumbnail plus any suspicious full-size page before final delivery; do not rely only on the pages that contain the most recent edit.
   - Use an explicit page review ledger during QA: mark each rendered page as `OK`, `fix`, or `acceptable exception`, with a short reason for any exception. Required checks include front matter semantics, page density, bottom whitespace, mid-page holes, orphan headings, code-listing breaks, float/table placement, references, placeholders, and user-flagged pages. If the task produced a PDF, a `review/page_review_ledger.md` or equivalent ledger must exist before final delivery.
   - If any layout-affecting edit is made after review, recompile, rerender, and re-check the changed page plus its previous and next page. If the edit uses `\Needspace`, `\clearpage`, `\FloatBarrier`, a large float/table, or a long code listing, explicitly re-check the preceding page for new whitespace.
   - Inspect the rendered title/front-matter page, table of contents when present, pages with large figures/tables, references, and any page the user called out.
   - Check front-matter semantics, not only visual density: the first page should look like a report opening, not a process checklist; a TOC should be isolated on its own page; tables at the front should appear only when the course template asks for a cover sheet, group division, experiment metadata, or other genuinely tabular information.
   - On body pages, scan the whole rendered page from top to bottom, not only the page bottom. Avoid unexplained mid-page holes larger than about three body-line heights between adjacent content blocks, such as a heading stranded above a figure, text separated too far from its figure/table, or gaps caused by `[H]`, `\clearpage`, `\FloatBarrier`, manual `\vspace`, overlarge floats, or oversized code blocks. Fix these by moving analysis text, relaxing float placement, resizing visual material, splitting code/tables, or revising content; do not hide the problem with negative spacing hacks.
   - For body pages, excluding cover/title pages, table of contents, references, appendix separator pages, and template-required blank pages, check bottom whitespace after rendering: the distance from the last visible body line or content element to the bottom of the text block should usually be no more than about three body-line heights. If a thesis-style chapter must end before a forced new-page next chapter, allow up to about five line heights on that chapter-ending page; ordinary course reports should not introduce chapter-style forced page breaks by default. If a rendered body page violates this, revise content or layout before delivery.
   - Iterate until there are no blank-looking pages, clipped text, unreadable tables, broken citations, or unwanted dates.
   - When a page looks empty, prefer honest content/layout fixes over typographic hacks: add or move substantive analysis, rebalance figures/tables, or slightly resize visual material. Do not make references ugly just to remove whitespace.
   - Reject visually awkward collages during PDF review: no diagonal float arrangement, no unrelated plots/tables stacked only to occupy space, and no page where the reading order is unclear.
   - Before final delivery, state the concrete page numbers or page ranges checked, not only broad page types. Include a fixed acceptance summary: PDF page count, render/review directory, checked page range, count of `OK`/`fix`/`acceptable exception` pages, exception reasons, `[H]` entries if any, and unresolved placeholder count. Do not present the report as final if the ledger is missing, any page remains marked `fix`, or unresolved placeholders remain without explicit user acceptance.

## Reusable Prompt

When the user wants a copyable prompt for another conversation, load `references/prompt-template.md` and adapt the bracketed fields.
When the user asks for default formatting, load `references/default-style.md`.
