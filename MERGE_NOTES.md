# Dissertation merge notes (Phase 1)

Generated: August 2026. This project was assembled from four Overleaf
exports: the UM dissertation template, SlabCity (VLDB 2023
camera-ready), GenRewrite (SIGMOD 2026 final), and DAGSmith (VLDB
submission).

## Structure
- `main.tex` — front matter + chapter includes
- `packages.tex` — merged package requirements (see comments there)
- `macros/{slabcity,genrewrite,dagsmith}_macros.tex` — per-paper macros,
  regenerated from the originals with conflicts resolved
- `chapters/01_introduction.tex`, `05_future_work.tex`,
  `06_conclusion.tex` — Phase-1 stubs seeded from the thesis proposal
  (search for `TODO`)
- `chapters/0{2,3,4}_*.tex` — wrappers (chapter title, publication
  footnote, listing style) around the verbatim paper sections in
  `chapters/{slabcity,genrewrite/sections,dagsmith/sections}/`

## Key transformations
- `\tool` renamed per paper: `\slabcity`, `\genrewrite`, `\dagsmith`.
  Author-note macros with conflicting definitions got prefixes
  (`\genbarzan`, `\dagjie`, `\genjie`, ...). Identical duplicate macros
  use `\renewcommand` in later-loaded files.
- All labels/refs prefixed `slab:` / `gen:` / `dag:`.
- Bibliographies merged into `references.bib` (272 entries after
  dedup); duplicate keys remapped in the chapter text.
- GenRewrite's algorithm converted from algorithm2e to algorithmicx
  (algorithm2e globally breaks algorithmicx labels). Rendering differs
  slightly from the paper; content identical.
- Global `\lstset` styles became `\lstdefinestyle{genrewriteCode}` /
  `{dagsmithCode}`, applied in each chapter wrapper.
- `dissertation.cls`: one `\protect` added in the bibliography hook
  (calc package compatibility — see comment at that line).
- SlabCity figures were referenced from sibling version folders in the
  original project; copied into `chapters/slabcity/figs/`.

## Known Phase-2 items (beyond the TODOs in the text)
- De-duplicate SlabCity/GenRewrite problem setting into a shared
  Background section; trim per-chapter intros; unify notation.
- Decide related-work handling (per-chapter vs consolidated).
- 17 overfull hboxes (two-column text reflowed to one column).
- BibTeX warnings for incomplete entries (missing years/journals).
- DAGSmith publication footnote says "under submission" — update.
- SlabCity alg.tex: omitted post-camera-ready footnote about the
  complete rule set (search `barnzarev`); consider restoring content.

## Build
pdflatex → bibtex → pdflatex ×2. Compiles with zero errors, zero
undefined references/citations.
