---
type: concept
title: "Energy-Based Models"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - generative
  - probabilistic
complexity: advanced
domain: deep-learning
status: developing
address: c-000151
related:
  - "[[LISA Tutorial - Restricted Boltzmann Machines]]"
  - "[[LISA Tutorial - Hybrid Monte Carlo Sampling]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/rbm.txt]]"
---

# Energy-Based Models (EBMs)

Assign a scalar **energy** to every configuration; plausible configurations get low energy:

```
p(x) = exp(-E(x)) / Z,     Z = sum_x exp(-E(x))      # partition function
```

With hidden variables, use the **free energy** `F(x) = -log sum_h exp(-E(x, h))`.

## Learning

Gradient of the negative log-likelihood = **positive phase** (lower F on data) minus **negative phase** (raise F on model samples):

```
dF(x)/d theta  -  E_{x~ ~ p_model}[ dF(x~)/d theta ]
```

The expectation is intractable, so approximate it with MCMC samples ("negative particles"):

- **Gibbs sampling** when conditionals are easy (RBMs): contrastive divergence (CD-k), persistent CD.
- **Hybrid/Hamiltonian Monte Carlo** for continuous variables or hard conditionals: [[LISA Tutorial - Hybrid Monte Carlo Sampling]].

## Examples

- Boltzmann machines, **Restricted** Boltzmann machines ([[LISA Tutorial - Restricted Boltzmann Machines]]), mean-covariance RBMs.
- Deep belief nets ([[LISA Tutorial - Deep Belief Networks]]), RNN-RBM ([[LISA Tutorial - RNN-RBM Polyphonic Music]]).
- Hopfield networks. LeCun's broader EBM framework covers any model that scores compatibility, including contrastive self-supervised learning. Diffusion and score-based models learn the gradient of the log-density (`-grad E`).

## Practical pain

`Z` makes the likelihood unmeasurable during training, so monitor with samples, filters and pseudo-likelihood instead.
