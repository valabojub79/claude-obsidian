---
type: concept
title: "LISA Tutorial - Multilayer Perceptron"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
complexity: beginner
domain: deep-learning
status: developing
address: c-000172
related:
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
  - "[[Multilayer Perceptron]]"
  - "[[Weight Initialization]]"
  - "[[Hyperparameter Tuning]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/mlp.txt]]"
---

# LISA Tutorial: Multilayer Perceptron

One-hidden-layer [[Multilayer Perceptron]] on MNIST in Theano. A `HiddenLayer` class is stacked under the `LogisticRegression` class from [[LISA Tutorial - Logistic Regression]].

## Implementation notes

- Hidden activation **tanh**: "typically trains faster and sometimes finds better local minima" than sigmoid.
- **Glorot/Xavier uniform init** for tanh: `W ~ U[-sqrt(6/(fan_in+fan_out)), +sqrt(6/(fan_in+fan_out))]`; **4x that range** for sigmoid. This keeps units in their linear regime early, so activations flow forward and gradients flow backward. See [[Weight Initialization]].
- Cost: `NLL + L1_reg * ||W||_1 + L2_reg * ||W||_2^2`.
- Gradients are computed generically over `classifier.params`, so the training code works for any depth.

## Result

**1.65% test error** after 828 epochs (about 10 epochs/minute on an i7-2600K).

## Tips and tricks (after LeCun et al., *Efficient BackProp*, 1998)

| Hyperparameter | Advice |
|---------------|--------|
| Non-linearity | Prefer functions symmetric about 0 (tanh), which give zero-mean inputs to the next layer |
| Weight init | Small, so activations sit in the linear (high-gradient) regime; preserve the variance of activations and gradients across layers (Glorot 2010) |
| Learning rate | Log-spaced grid (`1e-1, 1e-2, ...`), then narrow down. Decay: `mu_0 / (1 + d*t)` with `d <= 1e-3` |
| Hidden units | Dataset-dependent; without regularization, the generalization-vs-size curve is U-shaped |
| L1/L2 `lambda` | Try `1e-2, 1e-3, ...`; rarely a big win here, but worth a look |

Hyperparameter search is non-convex, mixes discrete and continuous values, and parameters interact, so it's not solvable exactly. Rely on rules of thumb (see [[Hyperparameter Tuning]]).
