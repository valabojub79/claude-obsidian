---
type: concept
title: "LISA Tutorial - Restricted Boltzmann Machines"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - unsupervised
  - generative
complexity: advanced
domain: deep-learning
status: developing
address: c-000175
related:
  - "[[LISA Tutorial - Deep Belief Networks]]"
  - "[[Energy-Based Models]]"
  - "[[LISA Tutorial - Hybrid Monte Carlo Sampling]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/rbm.txt]]"
---

# LISA Tutorial: Restricted Boltzmann Machines (RBM)

## Energy-based models

`p(x) = exp(-E(x)) / Z`, with `Z = sum_x exp(-E(x))` (the **partition function**). With hidden units `h`, use the **free energy** `F(x) = -log sum_h exp(-E(x,h))`, so `p(x) = exp(-F(x)) / Z`. See [[Energy-Based Models]].

NLL gradient:

```
-d log p(x)/d theta = dF(x)/d theta  -  E_{x~p}[ dF(x~)/d theta ]
                      positive phase      negative phase
```

The positive phase lowers the energy of data; the negative phase raises the energy of the model's own samples (**negative particles**), estimated by Monte Carlo.

## RBM

A Boltzmann machine with **no visible-visible or hidden-hidden connections** (a bipartite graph):

```
E(v, h) = -b'v - c'h - h'Wv
P(h_i = 1 | v) = sigm(c_i + W_i v)
P(v_j = 1 | h) = sigm(b_j + W'_j h)
F(v) = -b'v - sum_i log(1 + exp(c_i + W_i v))      # binary units
```

Given one layer, units of the other layer are **conditionally independent**, which allows **block Gibbs sampling**: sample all `h` given `v`, then all `v` given `h`.

## Training with approximate sampling

- **CD-k (contrastive divergence)**: start the chain **at a training example** and run only `k` Gibbs steps; `k = 1` works surprisingly well.
- **PCD (persistent CD, Tieleman 2008)**: one persistent chain whose state carries across updates. If updates are small relative to the chain's mixing rate, it keeps up. Gives better generative models.

Theano detail: return **pre-sigmoid** activations from `scan` so Theano can rewrite `log(sigmoid(x))` as softplus (avoiding NaNs), and pass `consider_constant=[chain_end]` to `T.grad` so gradients don't flow through the Gibbs chain.

## Monitoring (likelihood is intractable because of Z)

1. Look at negative samples: they should come to resemble training data.
2. Look at filters: stroke detectors on MNIST; Gabor-like on natural images with sparsity.
3. Proxies: **pseudo-likelihood** `log PL(x) ~ N * log sigm(F(x_flip_i) - F(x))` with a stochastic bit `i` (for PCD). For CD, reconstruction cross-entropy is more reliable.

## Result

PCD-15, lr 0.1, batch 20, 15 epochs (about 2 h on CPU); samples generated with 20 parallel persistent chains, 1,000 Gibbs steps between plots.

Next: [[LISA Tutorial - Deep Belief Networks]].
