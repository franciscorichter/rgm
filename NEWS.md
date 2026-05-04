# rgm 1.2.1

CRAN-pretest follow-up to 1.2.0:

* `DESCRIPTION` now references the published JABES 2026 article via its
  journal DOI (`<doi:10.1007/s13253-024-00638-6>`) instead of the
  superseded arXiv preprint (CRAN policy on e-print references).
* Removed "state-of-the-art" promotional language.

# rgm 1.2.0

First release after the 2026-02-01 CRAN archival.

## Major changes

* **Dropped `huge` dependency** — the reason `rgm` was archived (because
  `huge` itself was archived). The graphical-lasso warm start for the initial
  graph has been replaced with an empty initial graph; pass
  `initial.graphs = ` to `rgm()` to keep a warm start of your own choice.
* New exported function `post_processing_rgm()` returning ggplot diagnostics
  (recovery, alpha estimation, posterior density, beta convergence, ROC, edge
  probability heatmap).
* Updated CI to a working multi-platform `R-CMD-check` matrix
  (Ubuntu release / oldrel-1, macOS, Windows) with `--as-cran`.

## Minor changes

* Added `mvtnorm` to `Imports`. Removed an in-file `rmvnorm()` definition in
  `R/sim.rgm.R` that was unintentionally shadowing the imported one.
* Anchored the `R/imports.R` `@importFrom` tags with a `"_PACKAGE"` block so
  roxygen now actually emits the corresponding `importFrom()` lines into
  `NAMESPACE` (previously they were silently ignored).
* Removed an unused C++ template file (`src/test.cpp`).
* README rewritten: now references the JABES 2026 publication directly,
  explains the latent-space framing, and includes a runnable quick-start.

## Internal

* Removed compiled artifacts (`*.o`, `*.so`) from version control; they are
  build outputs.
* Added `.github/` and `.DS_Store` to `.Rbuildignore`.

# rgm 1.0.x

Versions prior to 1.2.0 required the now-archived `huge` package and are
available from the CRAN archive only.
