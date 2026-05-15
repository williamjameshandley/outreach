# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is Will Handley's **outreach talks** repository, containing LaTeX beamer presentations for public-facing astrophysics talks (schools, colleges, public lectures, cafe scientifique). The repository uses a **branch-per-talk organization**: each historical talk lives on its own branch (e.g. `intro_to_astro_2013`, `cups_2023`, `sherrington_2022`), while `master` contains only the shared preamble template.

For academic/research talks, see the sibling repository `talks` (`~/github/williamjameshandley/talks`).

## Repository Layout

### `master` branch (template only)

- `will_handley.tex` — placeholder top-level document with `<+Title+>`, `<+Subtitle+>`, `<+Date+>` markers
- `whaddress.tex` — author / institute block (shared)
- `whpackages.tex` — LaTeX package imports
- `whcolours.tex` — beamer colour theme tweaks
- `whenvironments.tex` — custom environments (`frameb`, `framet`)
- `matplotlibcolors.sty` — matplotlib colour palette
- `.gitignore`, `README.md`, `CLAUDE.md`

There are **no fragments, no images, no movies** on master. Every fragment / asset lives only on the branch(es) that use it.

### Per-talk branch (`<venue>_<year>`)

Each branch derives from master and adds:

- `will_handley.tex` — the talk's top-level document (renamed from its original filename, e.g. `cups.tex` -> `will_handley.tex`)
- Any fragment subdirectories required by that talk's `\input` closure (e.g. `cmb/`, `dark_matter/`, `inflation/`)
- Any image subdirectories required by that talk's `\includegraphics` closure (typically `Images/`)
- `Movies/` if the talk uses `\movie{}`
- `will_handley_<branch>.pdf` — committed final PDF (the build artefact `will_handley.pdf` is gitignored; the renamed copy is committed)
- `README.md` — abstract + PDF / source links + date / venue

## Build

```bash
latexmk -pdf will_handley.tex
cp will_handley.pdf will_handley_<branch>.pdf  # commit the renamed copy
```

## Branch Workflow

1. `git checkout master && git checkout -b <venue>_<year>`
2. Replace `will_handley.tex` with the talk content; copy in only the fragments / images that talk needs.
3. Build with `latexmk -pdf`, then copy `will_handley.pdf` -> `will_handley_<branch>.pdf` and commit.
4. Write a per-branch `README.md` (title, abstract, PDF link, source link, date / venue).
