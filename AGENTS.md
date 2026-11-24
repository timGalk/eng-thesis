# Editing the RenalSafe thesis

These conventions apply to the English-language thesis in `Diploma-tex/main.tex`. The PWr template sets the page layout in `Diploma-tex/pre.sty`. The instructions below preserve the formatting guidance from its example chapter and “Typical mistakes” table.

## Work in the source

- Edit the requested chapter in `main.tex`. Use `pre.sty` for shared typography, `refs.bib` for bibliographic records, and `figs/` for figure assets. Make local edits for local problems. Preserve the two-sided layout, margins, running headers, and front and back matter when editing chapter content.
- Use the existing chapter, section, and subsection hierarchy. Let LaTeX number headings. Keep labels stable when titles change so that existing references continue to work.
- For descriptions of RenalSafe, check the relevant implementation in the sibling `../RenalSafe` repository. Use tests to verify edge cases and recorded outputs to support reported results. Identify synthetic examples explicitly. A proposed feature, a unit test, and a clinical finding support different claims.

## Prose and cross-references

- Write one sentence per source line when practical. A single newline continues the paragraph. A blank line starts a new paragraph. Use the template's paragraph indentation and reserve `\noindent` for intentional exceptions. Let TeX wrap and hyphenate prose, especially when pasting text from a PDF.
- In English prose, write `e.g.\ when` or `i.e.\ the` when an abbreviation ends in a period mid-sentence. The backslash-space produces normal word spacing. Use a nonbreaking space for a reference such as `Fig.~\ref{fig:workflow}`, so the prefix stays with the number.
- Place descriptive labels next to their targets. Use `ch:` for chapters, `sec:` for sections, `ssec:` for subsections, `eq:` for equations, `fig:` for figures and panels, and `tab:` for tables. Each label must be unique. Refer to an item through its label, even if its current number is known.
- Use forms such as `Chapter~\ref{ch:intro}`, `Section~\ref{sec:decision-models}`, and `Equation~\eqref{eq:clearance}`. The last example assumes the equation has that label. `\eqref` already supplies the parentheses. When referring to a numbered section of an external SmPC, give its actual section number and cite the document.

## Equations, quantities, and symbols

Set variables and expressions in math mode. Use a numbered `equation` environment for a display cited later. Punctuate a displayed equation as part of the sentence. When the next line begins with “where”, place it directly after `\end{equation}` with no blank line. Define the symbols and units at first use.

| Meaning | LaTeX source | Typesetting detail |
| --- | --- | --- |
| Quantity in prose | `30~mL/min` | Keep the number and unit on the same line. |
| Quantity in an expression | `\(30\,\mathrm{mL/min}\)` | Use a thin space and upright unit symbols. Retain the case, denominator, and any normalization of the reported metric. |
| Products | `\(2x\)` and `\(2\cdot 3\)` | Use juxtaposition for a coefficient and a centred dot between numeric factors. Reserve the programming asterisk for literal code or an explicitly defined operator such as convolution. |
| Dimensions | `\(M\times N\)` | Use the multiplication sign between dimensions. |
| Negative values | `\(-1\)` | Math mode produces a minus sign. In prose use a hyphen for compounds, `--` for a range, and `---` for an em dash. |
| Named functions | `\(\sin(x)\)` and `\(\max(x,y)\)` | Use operator commands for upright names and correct spacing. |
| Subscripts and transpose | `\(s_{\mathrm{out}}\)`, `\(u_{ij}\)`, `\(\mathbf{U}^{\mathrm{T}}\)` | Set descriptive labels and the transpose marker upright. Keep variable indices italic. |

## Figures, flowcharts, tables, and code

- Export plots and flowcharts as vector PDF or EPS. Crop the export to the artwork. Use raster files for photographs and native screenshots. Inspect plots at their final printed size. Label each axis with the quantity and unit, and keep ticks, legends, and diagram labels legible.
- Put artwork inside a centred `figure` float. Set the width relative to `\linewidth` inside the enclosing figure or panel. Put `\caption` below the artwork and `\label` immediately after the caption. For a multipanel figure, caption and label each panel that the text discusses individually, then caption and label the complete figure.
- Explain the content in the caption. For a flowchart, identify the input, the decision or transformation, and the output. For a plot, identify the quantity or comparison shown. Use `\caption[Short list entry]{Full caption}` when the explanation is too long for the list of figures or tables.
- Use a `table` float with the caption and label **above** the tabular material. Give units in column headings when all entries share them. Use the existing `booktabs` or `tabularx` support where helpful. Check the result within the text margins at normal scale.
- Introduce each numbered figure or table in the text and explain what the reader should take from it. Let floats move to the top, bottom, or a dedicated page. Refer to the number through `\ref` so the prose still makes sense when the float moves.
- Set inline identifiers in `\texttt{}` and escape underscores there, as in `\texttt{renal\_rules}`. Use `verbatim` for short, relevant code excerpts. Preserve indentation and literal operators. Introduce the purpose of the excerpt and explain any non-obvious operation. Check line lengths because verbatim text does not wrap automatically.

## Attribution and final checks

1. Cite the source beside the claim with `~\cite{key}`. Credit reproduced or adapted figures, tables, and data in their captions. Verify that every key exists in `refs.bib` and that the source supports the statement. Keep the existing BibTeX `plain` style and let citations determine which entries appear in the bibliography.
2. Build from `Diploma-tex/` with `latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex` or the project's configured LaTeX editor. Allow BibTeX and the subsequent LaTeX passes to finish. An isolated build directory is useful for checking that old auxiliary files are not masking missing references.
3. Inspect the final log for unresolved references, missing citations, duplicate labels, missing graphics, and overfull boxes on edited pages. Check the rendered pages for split units, clipped tables, unreadable diagram text, and captions separated from their objects.
4. After moving or deleting a section, check surviving references against the removed labels and inspect the rebuilt contents and lists of figures and tables. Keep previously drafted sections, bibliography commands, and source assets outside the requested edit intact.
