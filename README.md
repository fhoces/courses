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

| Course | Repo |
|---|---|
| Experimentation Refresher | [experimentation-refresher](https://github.com/fhoces/experimentation-refresher) |
| Causal Inference Beyond A/B Tests | [causal-inference-beyond-ab](https://github.com/fhoces/causal-inference-beyond-ab) |
| Discrimination in Labor Economics | [discrimination-econ-refresher](https://github.com/fhoces/discrimination-econ-refresher) |
| ML Refresher: Discrimination and Fairness | [ml-discrimination-refresher](https://github.com/fhoces/ml-discrimination-refresher) |
| Python for an R User | [python-for-r-users](https://github.com/fhoces/python-for-r-users) |
| Intro to SQL | [sql-industry-prep](https://github.com/fhoces/sql-industry-prep) |

Plus one reference course kept for background, not part of the refresher
collection: [EC140S2022](https://github.com/fhoces/EC140S2022) (UC Berkeley
Econ 140, Spring 2022).

## Authoring conventions

`CLAUDE.md` in this repo documents the shared structure and style all six
refresher courses follow (module layout, slide-deck conventions, backup-slide
pattern, etc.) — useful context if you're looking at more than one of them.
