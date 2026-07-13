# Bayesian Statistics and MCMC — Final Assignment

Final assignment for the **Bayesian Statistics and MCMC** course, MSc in Mathematical
Modeling in Modern Technologies and Financial Engineering, National Technical University
of Athens (NTUA).

**Author:** Eftychios Kontadakis
**Professor:** Dimitrios Fouskakis

## Overview

This report covers four exercises spanning the core toolkit of applied Bayesian inference:
analytical derivations, conjugate models, and MCMC diagnostics, cross-checked against
classical (frequentist) results throughout.

- **Exercise 1 — Bayesian Linear Regression.** Simulates a 15-predictor dataset (including
  deliberately correlated predictors) and a response variable. Derives the Normal-Inverse-Gamma
  conjugate posterior analytically, fits the model in **JAGS**, cross-checks against OLS,
  and implements a **custom Gibbs sampler from scratch** to verify the analytical posterior.
  Includes full convergence diagnostics (trace plots, Gelman–Rubin, ESS, autocorrelation).

- **Exercise 2 — Bayesian Hypothesis Testing.** A Poisson rate model for server error counts.
  Computes a Bayes Factor for H₀: λ=2 vs H₁: λ≠2 under a Gamma(2,1) prior, and derives the
  posterior predictive distribution for a new observation (Negative Binomial), compared
  against the classical plug-in predictive.

- **Exercise 3 — Beta-Binomial Model with Mixed Priors.** A 5-group binomial model (stellar
  spectral classes) combining an **informative prior** (built from a historical experiment)
  for one group with **non-informative flat priors** for the rest. Fit via JAGS and compared
  against the closed-form conjugate posteriors and classical MLEs — including the
  degenerate zero-count case where classical inference breaks down but Bayesian inference
  doesn't.

- **Exercise 4 — Metropolis-Hastings with the Jeffreys Prior.** Derives the Jeffreys prior
  for the Poisson rate analytically, then implements a **Metropolis-Hastings sampler from
  scratch**, tuning the proposal variance to hit a ~25% acceptance rate, and validates the
  simulated posterior against the exact analytical Gamma posterior.

Throughout, all custom samplers (Gibbs, Metropolis-Hastings) are implemented by hand in R
and validated against both JAGS output and closed-form analytical results.

## Repository Contents

| File | Description |
|---|---|
| `Kontadakis-Eftychios.qmd` | Quarto source — full report (text, math, R code, figures) |
| `Kontadakis-Eftychios.pdf` | Rendered final report |

## Requirements

Rendering the `.qmd` to PDF requires:

- [Quarto](https://quarto.org/)
- A working [JAGS](https://mcmc-jags.sourceforge.io/) installation (required by `R2jags`)
- **XeLaTeX** with the `polyglossia` package (used for Greek/English font support —
  see `pdf-engine: xelatex` in the YAML header)
- R packages:
  ```r
  install.packages(c("MASS", "R2jags", "coda", "knitr"))
  ```

## Rendering

```bash
quarto render Kontadakis-Eftychios.qmd
```

## Notes

- Every simulation uses a fixed `set.seed()` for full reproducibility.
- MCMC runs (JAGS and custom samplers) include convergence diagnostics — trace plots,
  Gelman–Rubin R̂, effective sample size, and autocorrelation — before any results are
  interpreted.
