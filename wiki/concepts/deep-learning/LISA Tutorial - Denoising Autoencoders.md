---
type: concept
title: "LISA Tutorial - Denoising Autoencoders"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - unsupervised
complexity: intermediate
domain: deep-learning
status: developing
address: c-000167
related:
  - "[[Autoencoders]]"
  - "[[LISA Tutorial - Stacked Denoising Autoencoders]]"
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/dA.txt]]"
---

# LISA Tutorial: Denoising Autoencoders (dA)

Vincent et al., 2008. Train an [[Autoencoders|autoencoder]] to reconstruct the **clean** input from a **corrupted** copy.

## Corruption

Randomly zero a fraction of input entries (up to half). The dA must predict the missing values from the present ones, which forces it to capture **statistical dependencies between inputs**, not copy them. Being able to predict any subset of variables from the rest is enough to capture the full joint distribution (the same principle as Gibbs sampling).

Vincent 2008 interprets dAs from several angles: manifold learning, stochastic operator, information-theoretic, generative model.

## Implementation (Theano)

- `get_corrupted_input(x, level)`: `x * binomial(p = 1 - level)` drawn from a `RandomStreams`.
- Tied weights: decoder uses `W.T`. Sigmoid units; cross-entropy reconstruction loss.
- The constructor accepts **shared** `W` and `bhid`, so a dA can share parameters with an MLP's sigmoid layer (needed for stacking).
- `tile_raster_images` (from `utils.py`) plots the filters.

## Result on MNIST

Without noise, filters look patchy and uninformative; with **30% corruption**, filters become clear stroke detectors. Noise is what makes the representation useful.

Next: [[LISA Tutorial - Stacked Denoising Autoencoders]].
