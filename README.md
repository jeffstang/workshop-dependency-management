# Workshop: Dependency Management (renv + conda)

Short workshop repo demonstrating how to use renv (R) and conda/python together inside the same Quarto/R Markdown workflow.

Duration: 1 hour demo (renv + Python/reticulate examples)

Prerequisites
- R (>= 4.0) and RStudio installed
- Quarto CLI (for rendering slides or the demo locally) — optional for attendees following Rmarkdown in RStudio
- Optional: Miniconda or Anaconda if you want to run the Python/conda portions locally

What you'll find in this repo
- slides/index.qmd — Quarto revealjs slide deck for the workshop
- demo/demo.qmd — Single Quarto/R Markdown document demonstrating renv and conda/python + reticulate examples
- environment.yml — example conda environment used by the demo (development-friendly)
- .github/workflows/render-slides.yml — GitHub Actions workflow that renders the slides to docs/ on push

Usage notes
1. To preview slides locally (if you have Quarto installed):
   - quarto render slides/index.qmd --to revealjs --output-dir docs
   - Open docs/index.html in a browser

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

