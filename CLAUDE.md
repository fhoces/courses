# Courses collection — authoring conventions

Five sibling course repos share a deliberate, common style. This file
documents what's not derivable from the code itself.

```
courses/
  discrimination-econ-refresher/
  experimentation-refresher/
  ml-discrimination-refresher/
  python-for-r-users/
  sql-industry-prep/
```

Each course is self-contained — no shared tooling, build script, or CSS.
Consistency is maintained by convention.

**Domain across all courses:** ride-sharing (Uber / Lyft). Use ride-sharing
examples and synthetic data with that schema unless there's a specific
reason not to.

**Secondary domain (experimentation-refresher + causal-inference-beyond-ab
only, added 2026-07-03):** every module also carries one online-retail
parallel example under a "The Same Problem at an Online Retailer" slide and
a matching concepts.md section — a paid membership program (selection /
IV / HTE / policy modules) and a staggered next-day-delivery rollout
(interference / geo / panel-methods modules). Prose-only, no company ever
named (public repos). Keep new modules in those two courses consistent with
this thread.

**Tone:** the audience is the user, refreshing material they already know.
Never write as if to a beginner.

## Course directory structure

A course directory must have:

- `README.md` — "why this exists", "how to use this repo", a modules table,
  and a key-references list. 1–4 KB. Conversational, not academic.
- `learning-plan.md` — module-by-module breakdown: titles, time budgets,
  topics, objectives, dependencies, prerequisites. The authoritative spec
  for what's in / out of scope.
- `index.html` — hand-written nav hub. Bootstrap-free, inline CSS, ~760 px
  max-width, system fonts. Modules link to `module-XX/slides.html` with a
  status cell (`✓ done`, `upcoming`). GitHub link at the bottom. Match the
  existing per-course CSS — don't redesign.
- `module-XX/` directories, kebab-case, zero-padded.
- Optional `data/` — committed CSVs or `.sqlite` files **plus** the build
  script (`build_csvs.R` / `setup.R`). Only when drills need external data.

## Module structure

Every module has the **concept → show → drill** trio:

- `concepts.md` — written reference, the "what". Markdown prose, ~80–300
  lines.
- `slides.Rmd` (xaringan) → `slides.html` + `slides_files/`. The "show".
  Rendered outputs commit alongside the `.Rmd`.
- `exercise.{R,py,sql}` — runnable drills, the "do". Section headers in
  comments (`# ===== Q1. Title =====` or `-- Q1. Title`).

Don't invent new module artifacts (`notes.md`, `solution.R`, `figs/` …)
without first checking how a sibling course solved the problem. The single
existing exception is `ml-discrimination-refresher/module-03/figs/`.

## xaringan slide invariants

Every `slides.Rmd` opens with:

```yaml
---
title: "Module N: ..."
subtitle: "..."
output:
  xaringan::moon_reader:
    css: [default, default-fonts]
    nature:
      highlightStyle: github
      highlightLines: true
      countIncrementalSlides: false
      ratio: "16:9"
---
```

CSS chunk:

```css
.remark-code, .remark-inline-code { font-size: 80%; }
.remark-slide-content { padding: 1em 2em; }
.small .remark-code, .small table { font-size: 70%; }
```

knitr setup:

```r
knitr::opts_chunk$set(
  echo = TRUE, fig.align = "center",
  fig.width = 10, fig.height = 4.5, dpi = 150,
  message = FALSE, warning = FALSE
)
library(tidyverse)
theme_set(theme_minimal(base_size = 14))
```

**Slide 1 is always Course Map** — an HTML table linking every module in the
course with status indicators (`← current`, `✓`, `upcoming`). Update Course
Map in **every** module of a course when a new module is added.

Don't introduce new global CSS classes. Reuse `.small` and built-in
xaringan classes.

## Backup slides

For material that interrupts the main flow — proofs / derivations, DGP
(simulation) code, supplementary detail — use the backup-slide pattern from
`experimentation-refresher/module-03`. Three categories, one button style.

### Categories and anchor names

- **Proofs / derivations** — anchor `<topic>-proof` or `<topic>-derivation`
- **DGP code** — anchor `<topic>-dgp`
- **Additional details** — anchor `<topic>-detail` or descriptive slug

### Structure

All backup slides go at the end of the deck, after a divider:

```markdown
---
class: center, middle, inverse

# Backup Slides

---
name: selection-proof

# Backup: Deriving the Selection-Bias Decomposition

<content>

<a href="#selection-main" class="nav-btn">← back</a>
```

The originating main slide must declare its own `name:` anchor so the
`← back` button returns precisely.

### Button CSS — copy verbatim

```css
.nav-btn {
  position: absolute;
  bottom: 12px;
  left: 40px;
  font-size: 11px;
  background: #e8eaf6;
  padding: 2px 8px;
  border-radius: 3px;
  z-index: 100;
  text-decoration: none;
  color: #1a237e;
}
.nav-btn:hover { background: #c5cae9; }
.nav-btn-br {
  position: absolute;
  bottom: 12px;
  right: 70px;
  font-size: 11px;
  background: #e8eaf6;
  padding: 2px 8px;
  border-radius: 3px;
  z-index: 100;
  text-decoration: none;
  color: #1a237e;
}
.nav-btn-br:hover { background: #c5cae9; }
.inline-btn {
  font-size: 11px;
  background: #e8eaf6;
  padding: 2px 8px;
  border-radius: 3px;
  text-decoration: none;
  color: #1a237e;
  margin-right: 6px;
  vertical-align: middle;
}
.inline-btn:hover { background: #c5cae9; }
```

### Which button to use

- **`.nav-btn`** — bottom-left absolute. Default forward link from a main
  slide to its backup, and default `← back` link from a backup.
- **`.nav-btn-br`** — bottom-right variant. Use when a slide already has a
  `.nav-btn` in the bottom-left and needs a second anchor.
- **`.inline-btn`** — inline inside body text, when the link belongs to a
  specific sentence rather than the slide as a whole.

The blue-block `.btn-link` style in `experimentation-refresher/module-01`
is the older variant; match module-03 going forward.

## Pedagogy

- **Concept → show → drill** — every module hits all three artifacts.
- **Simulation-first** — synthesize data inline rather than shipping a real
  dataset, unless a real public dataset is the point of the module.
- **One published study per module where applicable** — at minimum link the
  canonical paper; ideally replicate or simulate its setup.
- **Stack discipline** — pandas (not polars) for Python; tidyverse +
  base R + ggplot2 for R; SQLite (not Postgres) for SQL.

## When adding or modifying a module

1. Read the course's `learning-plan.md` first — confirm the module is in
   scope and what it should cover.
2. Match the existing module structure exactly: `concepts.md` +
   `slides.Rmd` + `exercise.{R,py,sql}`.
3. Copy the YAML / CSS / setup chunks verbatim from a sibling module in
   the same course. Don't re-derive them.
4. Rebuild Course Map slide 1 in **every** module of that course.
5. Update the course's `index.html` row (link + status).
6. Update the course's `README.md` modules table if title/scope changed.
7. If the module has proofs, simulation code, or formal detail that would
   bloat the main flow, push them into backup slides and link with
   `.nav-btn` or `.inline-btn`.
8. Render `slides.html`, commit it alongside `.Rmd`, spot-check via the
   PDF→PNG pipeline.

## Per-course state

Verify against the filesystem before acting on any of these.

- **discrimination-econ-refresher** — modules 01–05, complete.
- **experimentation-refresher** — modules 01–08 planned; only 01–03 built.
  Modules 04–08 marked `upcoming` in `index.html`.
- **ml-discrimination-refresher** — modules 01–04 and 07 built; 05, 06, 08
  intentionally skipped or pending.
- **python-for-r-users** — modules 01–05, complete. Requires
  `Rscript data/build_csvs.R` before running exercises.
- **sql-industry-prep** — modules 01–05, complete. Requires
  `Rscript data/setup.R` to seed SQLite.

## Style drift to be aware of

Don't propagate, but don't refactor away as a side quest — confirm first.

- Custom CSS classes vary: `.highlight-box` / `.blue-box`
  (experimentation), `.write-ref` (sql), nothing extra elsewhere.
- Only `experimentation-refresher` has its own `.claude/` directory.
- Only `ml-discrimination-refresher` and `python-for-r-users` ship `.Rproj`
  files.
