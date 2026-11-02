---
type: concept
title: "LISA Tutorial - Hybrid Monte Carlo Sampling"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - sampling
complexity: advanced
domain: deep-learning
status: developing
address: c-000169
related:
  - "[[Energy-Based Models]]"
  - "[[LISA Tutorial - Restricted Boltzmann Machines]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/hmc.txt]]"
---

# LISA Tutorial: Hybrid (Hamiltonian) Monte Carlo

Duane et al. 1987; Neal 1993. A sampler for [[Energy-Based Models]] over **continuous** variables. It avoids Gibbs sampling's random-walk behavior and the need for tractable conditionals (for example the mean-covariance RBM, whose conditionals need matrix inversions).

## Idea

Treat the state `s` as a particle's position and add a velocity `phi`:

```
H(s, phi) = E(s) + K(phi) = E(s) + 1/2 * sum_i phi_i^2
p(s, phi) = exp(-H) / Z = p(s) p(phi)          # phi is independent Gaussian
```

Simulate **Hamiltonian dynamics** (`ds/dt = phi`, `dphi/dt = -dE/ds`): volume-preserving, reversible, keeps `H` constant. Alternate it with resampling `phi ~ N(0, I)` so the chain is ergodic. Marginalizing out `phi` gives samples of `p(s)`.

## Leapfrog integrator

```
phi(t + eps/2) = phi(t) - eps/2 * dE/ds(s(t))
s(t + eps)     = s(t) + eps * phi(t + eps/2)
phi(t + eps)   = phi(t + eps/2) - eps/2 * dE/ds(s(t + eps))
```

Implemented as half-step, then `n-1` full steps, then half-step, with Theano `scan`.

## Metropolis correction

Discretization and float rounding break exact conservation, so accept `chi'` with probability `min(1, exp(-H(chi')) / exp(-H(chi)))`. This cancels the bias **exactly**.

## One HMC step

1. Sample a velocity.
2. Run `n` leapfrog steps.
3. Accept or reject.

## Adaptive step size

Track a moving-average acceptance rate. If it is above target, multiply `eps` by `stepsize_inc` (mix faster); if below, multiply by `stepsize_dec`. Clip to `[eps_min, eps_max]`.

## Theano structure

`simulate_dynamics`, then `hmc_move` (returns accept and final position), then `hmc_updates` (shared-variable updates for position, step size, acceptance rate), wrapped by an `HMC_sampler` class. Tested by sampling a multivariate Gaussian after burn-in.

## Today

HMC and its adaptive variant NUTS power Stan and PyMC for Bayesian inference.
