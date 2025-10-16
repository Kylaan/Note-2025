# Copilot instructions for this LaTeX notes repo

## What this repo is
- A LaTeX workspace for course notes. Each subject lives in its own folder; the main example is `泛函分析/FA.tex` (Chinese functional analysis notes). Another subject `random-process/main.tex` currently has no content.
- Chinese typesetting via `ctexbook` with `fontset=windows`; compile with XeLaTeX.

## Key structure and conventions
- Class/layout: `\documentclass[12pt,a4paper,oneside,fontset=windows]{ctexbook}`, `\geometry{a4paper, margin=1in}`, `\linespread{1.3}`.
- Paragraph style: `\parindent=0` (no first-line indent), `\parskip=1em` (space between paragraphs).
- Theorem stack (section-scoped counters): `theorem`, `definition`, `lemma`, `corollary`, `example`, `proposition`.
- Math operators/macros: `\\DeclareMathOperator*{\\esssup}{ess\\,sup}`, `\\DeclareMathOperator{\\st}{\\mathrm{s.t.}}`, `\\DeclareMathOperator{\\diff}{\\mathrm{i.f.f.}}`, `\\DeclareMathOperator{\\ie}{\\mathrm{i.e.}}`. Add new operators using `\\DeclareMathOperator` for correct spacing.
- Visuals: `tcolorbox` for callouts; TikZ (`tikzmark, arrows.meta, shapes`) sometimes with `overlay, remember picture` for annotations; `hyperref` enabled.
- Front matter flow: roman pages for preface, TOC with `\tableofcontents`, then arabic numbering for main chapters.

## Build and preview (Windows PowerShell)
Recommended latexmk commands for XeLaTeX; quote non-ASCII paths:

```powershell
# One-shot build to PDF
latexmk -xelatex "泛函分析/FA.tex"

# Continuous preview (auto recompile on change)
latexmk -xelatex -pvc -interaction=nonstopmode -synctex=1 "泛函分析/FA.tex"

# Clean auxiliary files (keeps PDF)
latexmk -c "泛函分析/FA.tex"

# Full clean (including PDF)
latexmk -C "泛函分析/FA.tex"
```

Notes:
- Shell-escape is not required (no minted/Pygments). TikZ used here works without `--shell-escape`.
- Outputs are placed next to sources by default (e.g., `FA.aux`, `FA.fls`, `FA.xdv`, `FA.pdf`). If you introduce an output directory later, document the flag (e.g., `-outdir=build`).

## Patterns to follow when editing
- Use the predefined theorem-like environments; numbering resets per section.
- Prefer `tcolorbox` for highlighted principles/lemmas/notes (see Minkowski/Bessel examples).
- When annotating equations with TikZ overlays, include `overlay, remember picture` and mark nodes; rely on latexmk multi-pass to resolve positions.
- Reuse math operator macros (`\\esssup`, `\\st`, etc.) to keep typography consistent.
- Tables: follow the existing `table` + `tabular` style (see the `l^p` vs `L^p` comparison table).

## Adding a new subject/file
- Create a folder per subject with a `main.tex`. Start from the `泛函分析/FA.tex` preamble (ctexbook + packages). Update `\\title{}`, `\\author{}`, and reuse the theorem stack.
- Keep layout consistent (A4, 12pt, oneside, `\parskip`/`\parindent`) unless a subject requires a different style.

## External dependencies
- TeX distribution with Chinese support (TeX Live or MiKTeX).
- Packages used: `ctex`, `amsmath`, `amsthm`, `amssymb`, `bm`, `graphicx`, `hyperref`, `mathrsfs`, `tcolorbox`, `tikz` (with `arrows.meta`, `shapes`, `tikzmark`), `geometry`.
- Engine: XeLaTeX (due to `ctexbook` and Windows fontset). LuaLaTeX may work but is not the current convention here.

## Troubleshooting
- Missing Chinese fonts/`ctex`: install a full TeX scheme or allow MiKTeX auto-install; compile with XeLaTeX.
- TikZ `tikzmark`/overlay errors: ensure `\\usetikzlibrary{tikzmark,arrows.meta,shapes}` is present; build with latexmk (multi-pass) so references resolve.
- Overfull boxes in Chinese paragraphs: prefer minor rephrasing; adjust `geometry`/`\\linespread` only if necessary to keep style consistent.

## Examples already in this repo
- Orthogonal decomposition annotated with TikZ in the Hilbert space chapter.
- Bessel and Minkowski inequalities formatted via `tcolorbox`.
- Use of `\\esssup` in the `L^\\infty` definition and `l^p/L^p` comparison table.

> Agents: make small, consistent edits and mirror the existing patterns. If you add new packages or change the engine/flags, update this file to keep conventions aligned.
