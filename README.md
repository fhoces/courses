# Course Refreshers

**Live hub:** https://fhoces.github.io/courses/

An index over a set of self-contained refresher courses on the applied-economics
/ data-science stack, each threading the same ride-sharing (Uber/Lyft) running
example through its modules. Built for interview prep; doubles as a working
portfolio.

## How this repo is organized

Each course is its own independent GitHub repository — its own commit
history, its own remote, its own GitHub Pages deployment. This repo doesn't
contain their code; it's a thin hub that links out to each one (see
`index.html`), so the six courses stay separately versioned and buildable.
The course repos are checked out as sibling directories on disk but are
`.gitignore`d here to avoid nesting one git repository inside another.

## Courses

| Course | Repo | Summary |
|---|---|---|
| Experimentation Refresher | [experimentation-refresher](https://github.com/fhoces/experimentation-refresher) | Experimental design and causal inference for tech interviews — potential outcomes, SUTVA, power/CUPED, external validity, plus a tour of modern DiD, synthetic control, and causal forests |
| Causal Inference Beyond A/B Tests | [causal-inference-beyond-ab](https://github.com/fhoces/causal-inference-beyond-ab) | A deep-dive companion to Experimentation Refresher's Module 8 — modern difference-in-differences, synthetic control, and causal forests for heterogeneous effects |
| Discrimination in Labor Economics | [discrimination-econ-refresher](https://github.com/fhoces/discrimination-econ-refresher) | Audit studies, pay-gap decompositions, and algorithmic-bias audits, brought current past the Becker/Phelps-era canon |
| ML Refresher: Discrimination and Fairness | [ml-discrimination-refresher](https://github.com/fhoces/ml-discrimination-refresher) | Classical ML (linear models → trees → neural nets) paired with algorithmic-discrimination scenarios; every exercise in R |
| Python for an R User | [python-for-r-users](https://github.com/fhoces/python-for-r-users) | Translates existing R fluency into Python interview fluency — pandas + statsmodels, no syntax tutorials |
| Intro to SQL | [sql-industry-prep](https://github.com/fhoces/sql-industry-prep) | Interview-style analytical queries against a ride-sharing schema, concept → code → drills |

Plus one reference course kept for background, not part of the refresher
collection above:

| Course | Repo | Summary |
|---|---|---|
| EC140: Econometrics | [EC140S2022](https://github.com/fhoces/EC140S2022) | UC Berkeley, Spring 2022 — a full-semester undergraduate causal-inference course (syllabus, slides, problem sets) |

## Authoring conventions

`CLAUDE.md` in this repo documents the shared structure and style all six
refresher courses follow (module layout, slide-deck conventions, backup-slide
pattern, etc.) — useful context if you're looking at more than one of them.
