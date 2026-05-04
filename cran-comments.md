# Resubmission of rgm 1.2.0

## Reason for resubmission

`rgm` was archived on CRAN on 2026-02-01 because it required the archived
package `huge`. This release removes the dependency on `huge`:

* The single use of `huge::huge.select()` (a graphical-lasso warm start for the
  initial graph in `rgm()`) has been removed. The default initial graph is now
  empty, and the BD-MCMC step refines it from there. Users who need a warm
  start can still pass any starting graph via the `initial.graphs` argument.

`huge` is no longer in `Imports`, and there are no remaining uses of `huge`
or any other archived package anywhere in the source.

## Other changes in 1.2.0

* Added `mvtnorm` to `Imports` and removed an orphan in-file `rmvnorm()`
  definition that was shadowing the imported one.
* New exported function `post_processing_rgm()` with diagnostic plots.
* Removed an unused C++ template file (`src/test.cpp`); regenerated
  `RcppExports.{R,cpp}` via `Rcpp::compileAttributes()`.
* Repository hygiene: untracked compiled artifacts and `.DS_Store` files;
  added `.github/`, `.DS_Store` to `.Rbuildignore`.
* CI updated to multi-platform `R-CMD-check` (Ubuntu release / oldrel-1,
  macOS, Windows), all green with `--as-cran`.

## Test environments

* macOS 14, R 4.4.0 (local): `R CMD check --as-cran` passes with 0 errors,
  0 warnings, 3 NOTEs:
    1. "Package was archived on CRAN" (expected for this resubmission).
    2. "unable to verify current time" (local clock/network — not a package
       issue).
    3. HTML manual `<main>` tag warnings (local `tidy` version artifact;
       does not appear on the CRAN check farm).
* GitHub Actions matrix (current `main`): Ubuntu (release + oldrel-1),
  macOS (release), Windows (release) — all green with `--as-cran`.

## Reverse dependencies

None.
