# Workshop: Package Dependency Management (renv + conda)

Rationale: Bioinformatics tools are diverse and could require different programming languages which may lead to confusion when switching between tools and testing their functionalities

Workshop repo demonstrating how to use renv (R) and conda/python together inside the same Quarto/R Markdown workflow.

Duration: 1 hour including concepts, additional resources, demo

## 📊 View Rendered Slides

**The slides are automatically rendered and deployed via GitHub Actions**

Access the rendered slide deck here: **https://jeffstang.github.io/workshop-dependency-management/**

The slides are automatically updated whenever changes are pushed to the `main` branch.

Prerequisites
- R (>= 4.0) and RStudio installed
- Quarto CLI (for rendering slides or the demo locally) — optional for attendees following Rmarkdown in RStudio
- Local installation of Miniforge3 for macOS and Windows users

What you'll find in this repo
- slides/index.qmd — Quarto revealjs slide deck for the workshop
- demo/demo.qmd — Single Quarto/R Markdown document demonstrating renv and conda/python + reticulate examples
- environment.yml — example conda environment used by the demo (development-friendly)
- .github/workflows/render-slides.yml — GitHub Actions workflow that automatically renders the slides and deploys them to GitHub Pages on every push to main

Usage notes
1. **Viewing the slides**: 
   - **Online**: Visit https://jeffstang.github.io/workshop-dependency-management/ (automatically updated)
   - **Locally** (if you have Quarto installed):
     ```bash
     quarto render slides/index.qmd --to revealjs --output-dir ../docs
     ```
     Or from the repository root:
     ```bash
     mkdir -p docs
     quarto render slides/index.qmd --to revealjs --output-dir ../docs
     ```
     Then open `docs/index.html` in a browser

2. To follow the demo locally (RStudio):
   - Open demo/demo.qmd in RStudio
   - For the R-only portion, you can use renv::init() and renv::snapshot() as shown in the demo
   - To run the Python/reticulate parts, install Miniconda (see slides for mac/windows steps) and create the conda env with:
       conda env create -f environment.yml
     or use mamba for faster resolution:
       mamba env create -f environment.yml
   - In R, use reticulate::use_condaenv("workshop-dependency", required = TRUE) to point to the conda environment

3. Lockfiles
   - This repo includes an environment.yml for development. For reproducible deployment you can generate conda-lock files locally or in CI. See slides (conda-lock FYI) for details.

Contact
- Jeffrey Tang — jeffrey.tang@hli.ubc.ca

License
- MIT (see LICENSE file)

