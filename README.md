# rgm: Random Graphical Models for data from multiple environments

`rgm` is an R package that performs joint Bayesian inference of multiple
Gaussian (or Gaussian-copula) graphical models that share structure through
a low-dimensional latent space. It is the reference implementation of the
random graphical model of Vinciotti, Wit & Richter (2026, *JABES*).

When you have multivariate measurements collected at several *environments*
(body sites, tissues, ecological habitats, time periods, treatment groups,
…) and you expect the underlying interaction networks to be related but not
identical, `rgm` lets you estimate all of them jointly while quantifying
how similar each pair of environments is.

## Key features

- **Joint inference across environments.** Estimates per-environment graphs
  $G^{(b)}$ and precisions $\Omega_b$ simultaneously, with a structural prior
  that pools strength when environments are similar.
- **Latent space of environments.** Each environment is assigned a 2-D
  latent location whose posterior gives an interpretable similarity
  embedding (close ⇒ shared edges).
- **Edge covariates.** Optional edge-level covariates `X` enter through a
  global probit coefficient $\beta$ (e.g. taxonomic distance, anatomical
  proximity).
- **Counts via copula.** The Gaussian-copula extension (`method = "gcgm"`)
  handles zero-inflated count data such as microbiome OTU tables.
- **Full posterior.** Returns posterior samples for graphs, precisions,
  intercepts, latent locations, and covariate effects, so you can quantify
  uncertainty on any derived quantity.

## Installation

```r
# from CRAN (once 1.1.0 is back online — submitted 2026-05)
install.packages("rgm")

# or development version from GitHub
install.packages("remotes")
remotes::install_github("franciscorichter/rgm", build_vignettes = TRUE)
```

## Quick start

```r
library(rgm)

# Simulate B=8 related environments with p=20 nodes, n=200 obs each.
sim <- sim.rgm(n = 200, p = 20, B = 8)

# Fit RGM. Defaults: empty initial graph, GGM likelihood.
fit <- rgm(data = sim$data, iter = 2000, burnin = 500, method = "ggm")

# Posterior edge probabilities, n.edge x B
edge_prob <- apply(fit$sample.graphs, c(1, 2), mean)

# Posterior-mean latent locations
cloc <- apply(fit$sample.loc, c(1, 2), mean)

# Diagnostic plots (all-in-one)
plots <- post_processing_rgm(simulated_data = sim, results = fit)
plots$rgm_recovery
plots$edge_prob
```

For count data (microbiome, single-cell) use `method = "gcgm"` and supply
the discrete-Weibull marginal parameters via `gcgm.dwpar`. See the vignette
for a full walkthrough:

```r
vignette("rgm")
```

## What's new in 1.1.0

- Drops the `huge` dependency. The default initial graph is now empty;
  pass `initial.graphs = ` to keep a graphical-lasso warm start of your own.
- New exported function `post_processing_rgm()` returning a set of
  `ggplot` diagnostics.
- Cleaner `mvtnorm` import; namespace regenerated; build artifacts removed
  from version control.

See `NEWS.md` for the full changelog.

## Reference

Vinciotti, V., Wit, E. C., & Richter, F. (2026).
*Random Graphical Model of Microbiome Interactions in Related Environments.*
**Journal of Agricultural, Biological and Environmental Statistics**,
31(1), 46–59. <https://doi.org/10.1007/s13253-024-00638-6>

## License

MIT (see `LICENSE`). Bug reports: <https://github.com/franciscorichter/rgm/issues>.
