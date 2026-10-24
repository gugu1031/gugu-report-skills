# Default Academic Report Style

Use these defaults only when the course requirements or user instructions do not specify a format.

## Document

- Engine/class: `ctexart` with `UTF8,a4paper,12pt`.
- Paper: A4.
- Margins: `left=2.6cm,right=2.6cm,top=2.6cm,bottom=2.6cm`.
- Paragraphs: first-line indent `2em`; paragraph skip about `0.25em`.
- Table row spacing: `\renewcommand{\arraystretch}{1.2}`.
- Caption spacing: `\captionsetup{skip=0.35em}`.
- Hyperlinks: black internal/citation links, blue URLs.
- Title page: title, author/group, no date unless required (`\date{}`).
- Front matter: choose by report type; do not always include abstract, keywords, or table of contents.
- Table of contents: when included, it starts on a new page and the body starts after it.
- Opening content: do not start a report with an internal checklist table unless the course template requires a cover sheet, group division, experiment metadata, or similar front-matter table.
- Template priority: when a course gives an explicit template, keep its required margins, fonts, headings, numbering, spacing, caption style, title page, and bibliography style. Use this default style only for unspecified gaps.
- Visual fill: avoid gray/color filled blocks in normal report content. Code listings should be white background with a thin frame by default; do not use shaded code boxes unless the course template explicitly requires them.

## Fonts

The default report style is based on `ctexart` under XeLaTeX/Tectonic on macOS. `ctexart` may map Chinese font names through the current system fontset, so verify the rendered PDF when exact font identity is required.

- Main Chinese body font: macOS CTeX Song-style font, commonly `STSong` when available.
- Chinese bold/headings/title font: macOS CTeX Hei-style font, commonly `STHeiti` when available.
- Chinese kai/emphasis font when used by CTeX: macOS CTeX Kai-style font, commonly `STKaiti` when available.
- Main English body font: Latin Modern Roman (`LMRoman12-Regular`).
- English bold font: Latin Modern Roman Bold (`LMRoman12-Bold`).
- English italic/slanted font: Latin Modern Roman Italic/Slanted.
- Math fonts: Computer Modern / Latin Modern math (`CMR`, `CMMI`, `CMSY`, `CMEX`).

Imported figures may embed their own fonts. Do not treat figure-embedded fonts as the report body style.

## Front Matter Defaults

- Course papers and paper reviews usually include title, abstract, keywords, and a table of contents when the report is long enough to benefit from navigation.
- Short lab reports usually do not need an abstract or keywords unless required. Start with course/experiment metadata, student information, date, environment, deliverables, or group division when those are more useful.
- Group project/practice reports should include a group member and contribution table near the front when the course asks for collaboration details.
- Use a table of contents only when required or when the report has enough sections/pages to justify it. Avoid a standalone contents page for very short reports.
- If using a table of contents, write `\clearpage\tableofcontents\clearpage`; never place it below the title-page prose or on the same page as the first body section.
- Requirements checklists are planning artifacts, not report front matter. Convert them into natural prose in the introduction or task-background section.
- If the course supplies a cover sheet, reproduce or embed it first, then continue the LaTeX report.

## Default LaTeX Preamble Pattern

```tex
\documentclass[UTF8,a4paper,12pt]{ctexart}
\usepackage{amsmath}
\usepackage{array}
\usepackage{booktabs}
\usepackage{caption}
\usepackage{enumitem}
\usepackage{float}
\usepackage{geometry}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{listings}
\usepackage{needspace}
\usepackage{tabularx}
\usepackage{xcolor}

\geometry{left=2.6cm,right=2.6cm,top=2.6cm,bottom=2.6cm}
\hypersetup{colorlinks=true,linkcolor=black,citecolor=black,urlcolor=blue}

\makeatletter
\renewcommand{\@cite}[2]{\textsuperscript{[#1\if@tempswa , #2\fi]}}
\makeatother

\setlength{\parindent}{2em}
\setlength{\parskip}{0.25em}
\renewcommand{\arraystretch}{1.2}
\captionsetup{skip=0.35em}
\newcolumntype{Y}{>{\raggedright\arraybackslash}X}

\definecolor{codekeyword}{RGB}{0,0,170}
\definecolor{codegray}{RGB}{96,96,96}
\definecolor{codestring}{RGB}{0,110,80}
\lstdefinestyle{reportcode}{
  basicstyle=\footnotesize\ttfamily,
  frame=single,
  breaklines=true,
  captionpos=t,
  columns=fullflexible,
  commentstyle=\color{codegray},
  keepspaces=true,
  keywordstyle=\color{codekeyword}\bfseries,
  numbers=left,
  numberstyle=\tiny\color{codegray},
  showstringspaces=false,
  stringstyle=\color{codestring},
  tabsize=2,
  xleftmargin=2em,
  framexleftmargin=1.5em
}
```

Use the `reportcode` style only when the report contains code. Set the language explicitly on each listing so keyword highlighting works, for example `\begin{lstlisting}[style=reportcode,language=C++,caption={...}]` or `\begin{lstlisting}[style=reportcode,language=Python,caption={...}]`. If the language is pseudocode or unsupported, choose the nearest supported language only when it improves readability and note that highlighting is approximate.

For short body listings, reserve enough space before the block so the caption and first lines are not orphaned at the bottom of a page. Use `\Needspace{<n>\baselineskip}` before the listing, with `<n>` roughly equal to the number of code lines plus caption and spacing, for example `\Needspace{14\baselineskip}` before a 10-line snippet. After adding `\Needspace` or a deliberate page break, inspect the previous page; if it now has excessive bottom whitespace, move the setup or explanatory paragraph before the listing. If the listing is too long to keep together, split it into meaningful chunks or move it to an appendix instead of allowing an ugly break.

Add `\usepackage{longtable}` only when a multi-page table is genuinely required; do not include it by habit.

## Bibliography Defaults

- Follow the course template or required citation style first.
- If no citation style is specified, `thebibliography` is acceptable for small course reports. Keep the bibliography in the normal document font by default.
- Do not add `\footnotesize`, `\scriptsize`, aggressive item spacing, or other font/spacing hacks to the bibliography just to reduce page count or fill/avoid whitespace.
- Make references look like references, not a raw link dump: include author/organization, title, venue or source, year when available, and URL only when it is needed for web/course materials.
- Long URLs may wrap, but should not overflow the margin. If URL appearance dominates the reference page, consider citing a stable title/source in text and keeping the URL in a normal `\url{...}` field.

## Page Density Defaults

- A rendered page should not look unintentionally empty except for cover, contents, appendix separator, or a naturally short final references page.
- Before final delivery, create or inspect a full-document page overview from rendered page images. For short course reports, review every page thumbnail and open suspicious pages at full size; do not inspect only the pages touched by the last edit.
- Keep a page review ledger during QA. Mark each rendered page as `OK`, `fix`, or `acceptable exception`, and record a short reason for exceptions such as required cover layout, table of contents, appendix separator, or naturally short final references page. If a PDF is produced, `review/page_review_ledger.md` or an equivalent ledger must exist before final delivery.
- Treat `[H]` as a high-risk exception. Every remaining `[H]` figure/table must be recorded in the ledger with its page number, why fixed placement was necessary, and previous/current/next page status after rendering.
- After any layout-affecting edit, recompile, rerender, and re-check the changed page plus the previous and next page. For edits involving `\Needspace`, `\clearpage`, `\FloatBarrier`, a large float/table, or a long code listing, explicitly re-check the preceding page for new whitespace.
- Scan body pages from top to bottom after rendering, not only at the bottom edge. Avoid unexplained mid-page holes larger than about three body text lines between adjacent content blocks, especially around headings, figures, tables, code blocks, display equations, and forced float barriers. Common causes are `[H]`, `\clearpage`, `\FloatBarrier`, manual `\vspace`, overlarge floats, and code/table blocks that should be split or resized.
- On body pages, excluding cover/title pages, table of contents, references, appendix separator pages, and template-required blank pages, check bottom whitespace after rendering. The distance from the last visible body line or content element to the bottom of the text block should usually be no more than about three body text lines. If a thesis-style chapter must end before a forced new-page next chapter, allow up to about five lines on that chapter-ending page; ordinary course reports should not introduce chapter-style forced page breaks by default. Treat this as a rendered-PDF check, not a source-code blank-line count.
- Follow conservative academic layout conventions unless the course template says otherwise: figures centered with captions below; tables centered with captions above; explanatory text stays near the result.
- Body tables should be short, scan-friendly, and necessary for comparison. Use them for numeric results, compact comparisons, parameter grids, small timelines, experiment metadata, or group division when required.
- Avoid multi-page tables in the main body. Use `longtable` only when the assignment explicitly requires a full catalog/timeline/coding sheet or when the table itself is central evidence. Otherwise summarize in prose, use a compact overview table, or move the full inventory to an appendix/supplement.
- Do not put planning columns such as "可配视觉材料", "待补素材", "备注", source-hunting notes, file lists, or checklist status into the final report body.
- For sparse figure/table pages or body pages with excessive middle/bottom whitespace, first fix content and layout: move the explanatory paragraph closer, adjust float placement, slightly resize the image, split code/tables, or revise the surrounding analysis.
- Use side-by-side layouts only when the items are visually and semantically comparable: paired subfigures, before/after images, ablation tables with similar height, or direct A/B comparisons. Do not place a short plot next to a tall table, mix unrelated results into one visual block, or create diagonal/stair-step compositions.
- Do not make the body, captions, references, margins, or line spacing uglier to solve whitespace. Typography is part of report quality.
- If adding text is the right fix, add substantive analysis: what the figure/table shows, why the result occurs, what limitation it reveals, or how it answers the assignment.
- If the remaining whitespace is caused by a necessary section break, a large required figure, or a short bibliography, leave it rather than damaging the layout.
- If a long table, full code listing, questionnaire, timeline, or inventory is moved to an appendix or supplementary file, keep a compact summary and explicit appendix/source reference in the main text so the argument remains readable.
- Final delivery should include an acceptance summary with PDF page count, render/review directory, checked page numbers or ranges, `OK`/`fix`/`acceptable exception` counts, exception reasons, `[H]` entries if any, and unresolved placeholder count. Do not call the PDF final while the ledger is missing, any page is marked `fix`, or unresolved placeholders remain without explicit user acceptance.

## Report Type Structures

Use these only when no course outline is provided.

### Course Paper

1. 引言
2. 背景与问题
3. 主体分析
4. 讨论
5. 结论
6. 参考文献

### Paper Review / Method Comparison

1. 引言
2. 背景方法
3. 代表性方法
4. 实验结果与局限
5. 横向对比
6. 总结
7. 参考文献

### Lab Report

1. 实验目的
2. 实验原理
3. 实验环境与数据
4. 方法步骤
5. 关键代码
6. 结果图表
7. 结果分析
8. 问题与总结

### Project / Practice Report

1. 任务背景与目标
2. 需求或方案设计
3. 实现方法
4. 测试与结果展示
5. 问题分析
6. 总结与改进方向

## Material, Figure, and Table Defaults

- User-provided templates, rubrics, real experiment outputs, screenshots, generated plots, and instructor materials have priority over generic styling.
- For lab/project reports, if code and data are available, try to generate real plots/tables before falling back to placeholders.
- For paper/method reports, prefer original authoritative assets when they are needed: arXiv source figures, official repository images, or course PPT figures. Keep vector files such as PDF/SVG when possible.
- If a needed image is unavailable, use a labeled placeholder such as `\fbox{\parbox[c][4cm][c]{0.85\linewidth}{\centering 待插入：实验结果截图}}`. Report remaining placeholders before final delivery.
- Every figure/table should support an explanation in the surrounding text. Avoid decorative figures.
- Captions should state what the reader should notice; include source notes when using paper/PPT/repository figures.
- Never fabricate results, screenshots, datasets, citations, or source attributions.

## Code Defaults

- Put only important snippets in the body. Move long code to an appendix or reference a separate source file.
- Prefer small monospace code with line numbers, a thin frame, white background, automatic wrapping, and stable indentation.
- Set `language=...` explicitly for each listing when the language is known; otherwise blue keyword highlighting will not reliably appear. Use modest syntax highlighting: blue bold keywords, gray comments, readable strings, black identifiers, and no colored background.
- Do not add gray/color background fill to code blocks. Avoid `backgroundcolor`, shaded boxes, `tcolorbox`, and `mdframed` for code unless the course template explicitly requires them.
- Keep short code listings together when possible. Avoid page breaks that leave only a caption or one to three code lines at the bottom or top of a page; use `\Needspace{...}`, a deliberate page break before the listing, splitting, or appendix placement as appropriate.
- After using `\Needspace` or a deliberate page break for code, re-check the previous page for excessive bottom whitespace. If needed, move nearby explanation text rather than adding arbitrary blank lines.
- After rendering, inspect code pages for overflow, cramped line numbers, broken Chinese comments, clipped frames, and awkward page breaks.
- If Chinese comments do not render cleanly, explain them in the surrounding text and keep the code block itself simple.
- If `minted` is unavailable or shell escape is disabled, use `listings`; do not choose a code highlighter that breaks compilation.
