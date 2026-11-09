# MSc Thesis — LaTeX scaffold

Generic scaffold (standard `report` class) for a UCT MSc(Eng) dissertation.
Swap in the official UCT EBE faculty thesis template as soon as you have it —
only `main.tex` and `preamble.tex` should need to change; the `chapters/*.tex`
files are written to survive that swap.

## Structure

```
main.tex              # document shell: front matter, chapter order, bibliography
preamble.tex          # packages/settings (shared, so a paper shell can reuse it)
chapters/
  abstract.tex
  introduction.tex
  lit_review.tex      # written to be liftable into a standalone paper later
  methodology.tex
  results.tex
  discussion.tex
  conclusion.tex
  appendix.tex
bib/
  references.bib      # auto-exported from Zotero (Better BibTeX), do not hand-edit
  concept_matrix.csv   # one row per paper, per Masters_Prep_Plan.md Section 17
figures/
latexmkrc            # `latexmk` build config (biber-aware)
```

## One-time setup

1. **Zotero → Better BibTeX**
   - Install the [Better BibTeX](https://retorque.re/zotero-better-bibtex/) plugin in Zotero.
   - Create/use a collection for this project's references.
   - Right-click the collection → **Export Collection** → format **Better BibLaTeX**
     → check **Keep updated** → save as `bib/references.bib` in this folder.
   - From then on, every paper you add to that Zotero collection updates the
     `.bib` file automatically (local builds pick it up immediately).

2. **Overleaf**
   - Zip this folder (or push it to a GitHub repo) and create a new Overleaf
     project from it ("Upload Project" or "Import from GitHub").
   - Overleaf's free tier does **not** auto-sync with a local folder or Zotero's
     live export — after adding new refs in Zotero you'll need to re-upload
     `references.bib` (or use Overleaf's paid Git/GitHub sync, which can pull
     from a repo you update locally).
   - Overleaf uses `biber` automatically once it sees `\usepackage{biblatex}` —
     no extra config needed.

3. **Local builds (optional, e.g. in VS Code with LaTeX Workshop)**
   ```sh
   latexmk -pdf main.tex
   ```

## Workflow notes

- **One `\input` per chapter** — keeps diffs small and lets you draft chapters
  out of order.
- **`chapters/lit_review.tex`** is deliberately self-contained (no
  "as discussed in Chapter X" references) so it can become the related-work
  section of a journal/conference paper without rewriting.
- **`bib/concept_matrix.csv`** — fill in one row per paper as you read
  (see `Masters_Prep_Plan.md`, Section 17). Gaps in this table become your
  research-gap paragraph in the lit review.
- **Decide the final deliverable format later** — this shell only matters for
  the dissertation; a future paper would get its own `paper/` shell reusing
  `preamble.tex` and the lit review content, with the journal's own class file.
