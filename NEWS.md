# rgm 1.1.0

## Major changes

* **Dropped `huge` dependency** to address the CRAN archival on 2026-02-01.
  The graphical-lasso warm start for the initial graph has been replaced with
  an empty initial graph; pass `initial.graphs = ` to `rgm()` to keep a warm
  start of your own choice.
* New exported function `post_processing_rgm()` returning ggplot diagnostics
  (recovery, alpha estimation, posterior density, beta convergence, ROC, edge
  probability heatmap).

## Minor changes

* Added `mvtnorm` to `Imports`. Removed an in-file `rmvnorm()` definition in
  `R/sim.rgm.R` that was unintentionally shadowing the imported one.
* Anchored the `R/imports.R` `@importFrom` tags with a `"_PACKAGE"` block so
  roxygen now actually emits the corresponding `importFrom()` lines into
  `NAMESPACE` (previously they were silently ignored).
* Removed an unused C++ template file (`src/test.cpp`).

## Internal

* Removed compiled artifacts (`*.o`, `*.so`) from version control; they are
  build outputs.
* Added `.github/` and `.DS_Store` to `.Rbuildignore`.

# rgm 1.0.x

Versions prior to 1.1.0 required the now-archived `huge` package and are
available from the CRAN archive only.
