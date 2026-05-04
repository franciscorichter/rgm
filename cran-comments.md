# Resubmission of rgm 1.2.1

## Reason for resubmission (vs. 1.2.0)

Addresses the issue raised in the CRAN auto-pretest of 1.2.0:

* `DESCRIPTION` no longer references the arXiv preprint as `<arXiv:...>`;
  it now points at the **published** JABES 2026 article via its journal DOI
  `<doi:10.1007/s13253-024-00638-6>`. The paper has been peer-reviewed and
  published since the arXiv-era citation was written.
* Removed "state-of-the-art" promotional language from the Description.

## Reason for resubmission (vs. archived 1.0.4)

`rgm` was archived on CRAN on 2026-02-01 because it required the archived
package `huge`. The `huge` dependency has been removed: the single use of
`huge::huge.select()` (a graphical-lasso warm start for the initial graph in
`rgm()`) is gone. The default initial graph is now empty, and the BD-MCMC
step refines it from there. Users who want a warm start can pass any
starting graph via the `initial.graphs` argument.

## Other changes since 1.0.4

* Added `mvtnorm` to `Imports` and removed an orphan in-file `rmvnorm()`
  definition that was shadowing the imported one.
* New exported function `post_processing_rgm()` returning ggplot diagnostics.
* Removed an unused C++ template file (`src/test.cpp`); regenerated
  `RcppExports.{R,cpp}` via `Rcpp::compileAttributes()`.
* Repository hygiene: untracked compiled artifacts and `.DS_Store` files;
  added `.github/`, `.DS_Store` to `.Rbuildignore`.
* CI updated to multi-platform `R-CMD-check` (Ubuntu release / oldrel-1,
  macOS, Windows), all green with `--as-cran`.

## Notes from the auto-pretest

The 1.2.0 pretest also flagged "Possibly misspelled words: RGMs, Vinciotti,
Microbiome, microbiome". These are correct domain-specific words and proper
names (RGM = Random Graphical Model; Vinciotti is a co-author). They are
intentional.

## Test environments

* macOS 14, R 4.4.0 (local): `R CMD check --as-cran` passes with 0 errors,
  0 warnings, 3 NOTEs:
    1. "Package was archived on CRAN" (expected for this resubmission).
    2. "unable to verify current time" (local clock/network — not a package
       issue).
    3. HTML manual `<main>` tag warnings (local `tidy` version artifact;
       does not appear on the CRAN check farm).
* GitHub Actions matrix on `main`: Ubuntu (release + oldrel-1), macOS
  (release), Windows (release) — all green with `--as-cran`.
* CRAN auto-pretest of 1.2.0 (Windows + Debian, r-devel): only the
  arXiv-format issue addressed in this resubmission, plus the spell-check
  false positives noted above.

## Reverse dependencies

None.
