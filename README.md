# CITC LaTeX style

`citc.sty` formats a LaTeX document to the USTP College of Information Technology
and Computing manuscript guidelines (*Formatting and Submission Guidelines for
Undergraduate and Graduate Theses and Capstone Projects*, 2nd Edition). Drop it
beside your `.tex` file, load it, and write normally.

## Use it

```sh
latexmk -pdf thesis.tex      # biber runs automatically
```

`thesis.tex` is a working skeleton that shows every construct the guidelines
have an opinion about, and `frontmatter.tex` holds the preliminary pages — chapters, the three subsection levels, a paragraph
heading, a table, a figure, a numbered equation with its term list, and APA
citations. Start from it, or copy the two lines you need into a document you
already have:

```latex
\documentclass[12pt,a4paper]{article}
\usepackage[colorlinks=true,allcolors=black]{hyperref}
\usepackage{citc}        % after hyperref
\usepackage{cleveref}    % optional, after citc
```

Put your references in `references.bib`. If you use Zotero, export with Better
BibTeX and keep exporting to that filename.

## What you get

Write a `\section` and you get a chapter. The rest follows from ordinary LaTeX.

| You write | You get |
|---|---|
| `\section{Introduction}` | new page, `Chapter I` over `INTRODUCTION`, centered bold uppercase, page number suppressed on that page |
| `\subsection{...}` | `1.1.` bold at the left margin, title case |
| `\subsubsection{...}` | `1.1.1.` bold at the left margin |
| `\phead{A heading}` | indented, **bold italic**, period, paragraph runs on |
| `\begin{table}` + `\caption` | `Table 2.1.` above, sentence case, left aligned |
| `\begin{figure}` + `\caption` | `Figure 3.4.` below, sentence case, left aligned |
| `\begin{equation}` | `(Equation 3-1)` italic, flush right |
| `\begin{whereterms}` | `where:` list, flush left, single-spaced, wraps |
| `\eqentry{A short name}` | adds that equation to the list of equations |
| `P{3cm}` and `L` in a table | ragged-right columns, fixed width and flexible |
| `\parencite` / `\textcite` | APA 7 author–date |
| `\Cref{sec:...}` | "Chapter 2" for a chapter, "Section 2.1" below that |

Tables, figures and equations are numbered per chapter and restart in each one,
independently of each other, as Articles 5 to 7 require.

Set automatically, with no markup: A4; margins 2.5 cm top, bottom and right and
3.8 cm left; Book Antiqua 12 pt in black; justified, single-spaced, 1.25 cm
first-line indent on every paragraph; arabic page numbers in the upper right,
2.5 cm from the right edge and 1.25 cm from the top.

## The preliminary pages

`\input{frontmatter}` in place of `\maketitle` produces all nine pages Section
3.1.1 lists, in its order: title page, acknowledgment, dedication, table of
contents, lists of tables, figures and equations, acronyms, abstract. Lowercase
roman numerals sit centered at the bottom, and the title and approval pages are
counted without being printed, as 3.2.12 and 3.3.16 require. Arabic numerals
resume in the upper right at Chapter I.

Fill the fields at the top of `frontmatter.tex` -- title, authors, department,
degree, date, and the five signatories. The title appears twice, once broken
into inverse-pyramid lines for the title page and once as a single run of text
for the approval paragraph. Delete the dedication page if you are not using one.

Three things the file cannot do for you. The approval page reproduces the layout
of 3.3.4 to 3.3.15, but 3.3.2 requires the current ISO form FM-USTP-ACAD-11,
which 3.3.17 wants printed, signed in wet ink and scanned into the electronic
copy -- so replace that page with the scan before submission. The acknowledgment
and abstract are placeholders. And an equation appears in the list of equations
only if you tag it with `\eqentry`.

## Two things to know

**The font.** Book Antiqua is Monotype's Palatino. `citc.sty` loads URW Palladio
through `mathpazo`, which is metric-compatible, so line breaks and page counts
match what Book Antiqua produces. Mathematics falls back to Computer Modern for
symbols Palatino has no glyph for — parentheses, summation signs, large
delimiters. That is normal LaTeX and no one reads it as the wrong font.

**Tables that overflow.** Size wide columns with `tabularx` at `\linewidth`, as
`thesis.tex` does, rather than in centimetres. The CITC text block is 14.7 cm
wide, narrower than the LaTeX default, and fixed column widths copied from
another document will run past the right margin.

## What it does not do

The package formats the manuscript. It does not produce the hardbound cover and
spine (Article 2), the signed ISO approval form (3.3.2), or the plagiarism and
AI-disclosure certificates (Article 11). Those are documents in their own right,
and each of them needs a signature.

It also cannot check what it cannot see. Read Articles 4 to 7 for the rules about
content rather than layout: third-person point of view, sentence-case captions
that name a table or figure instead of describing it, every equation term defined
after the equation, and no underlining for emphasis.

## Requirements

A TeX Live installation with `titlesec`, `tabularx`, `array`, `chngcntr`,
`caption`, `tocloft`, `fancyhdr`, `mathpazo`, `biblatex`, `biblatex-apa` and
`biber`. On TeX Live
these come with `texlive-latex-extra`, `texlive-fonts-recommended`,
`texlive-bibtex-extra` and `biber`.

## License

MIT, see `LICENSE`. The guidelines themselves belong to CITC and are not
included here; get the current edition from the college.
