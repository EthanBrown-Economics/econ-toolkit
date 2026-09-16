# Technical Skills for Economics

[![Deploy documentation](https://github.com/EthanBrown-Economics/econ-toolkit/actions/workflows/deploy.yml/badge.svg)](https://github.com/EthanBrown-Economics/econ-toolkit/actions/workflows/deploy.yml)
[![Read the docs](https://img.shields.io/badge/read-the%20docs-0f766e?logo=github)](https://ethanbrown-economics.github.io/econ-toolkit/)

An open-source, practical field guide to the technical skills used in economics research and analysis. Learn the tools behind modern econometrics, data work, and reproducible research in one place.

The guide covers Git and GitHub, Markdown, command line basics, LaTeX, R for econometrics, Stata, Python, SQL, data visualization, machine learning, and reproducible research. It is designed for students, research assistants, economists, and applied researchers building a reliable workflow.

**[Read the documentation](https://ethanbrown-economics.github.io/econ-toolkit/)** | **[Browse the guides](docs/index.md)** | **[Suggest a topic](https://github.com/EthanBrown-Economics/econ-toolkit/issues/new)**

## Why this exists

Economics research often depends on a stack of tools rather than one programming language. This project connects those tools to the work economists actually do: cleaning data, estimating models, producing tables and figures, collaborating with Git, and making results reproducible.

The first pass is anchored in Stata, R, Python, SQL, and Power BI, with later guides filling in adjacent skills such as web scraping and deep learning.

## Contents

- [Git & GitHub](docs/git-github/README.md): version control, branches, pull requests, and GitHub Actions
- [Markdown](docs/markdown/README.md): the writing format used by every guide
- [Command line basics](docs/command-line/README.md): files, environments, and package managers
- [LaTeX](docs/latex/README.md): papers, CVs, bibliographies, and Beamer slides
- [R for econometrics](docs/r/README.md): data wrangling, visualization, panel models, and IV
- [Stata](docs/stata/README.md): do-files, estimation, tables, merging, and reshaping
- [Python for data work](docs/python/README.md): pandas, NumPy, and web scraping
- [SQL](docs/sql/README.md): joins, aggregation, and data warehouse queries
- [Data visualization](docs/data-viz/README.md): Power BI, ggplot2, matplotlib, and seaborn
- [Machine learning](docs/machine-learning/README.md): scikit-learn and deep learning primers
- [Reproducible research](docs/reproducible-research/README.md): project structure and environments

## Local development

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
mkdocs serve
```

Then open the local URL shown by MkDocs.

The published site is available at <https://ethanbrown-economics.github.io/econ-toolkit/>.

## Contributing

Corrections, examples, and proposed topics are welcome. Open an issue for a question or suggestion, or submit a pull request with a focused improvement. Keep examples reproducible and explain which economics workflow they support.

## Build order

1. Git & GitHub
2. Markdown
3. Command line basics
4. LaTeX
5. R for econometrics
6. Stata
7. Python for data work
8. SQL
9. Data visualization
10. Intro ML / deep learning
11. Reproducible research practices
