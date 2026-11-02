---
type: concept
title: "Activation Functions"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
complexity: beginner
domain: deep-learning
status: developing
address: c-000129
related:
  - "[[Vanishing and Exploding Gradients]]"
  - "[[Weight Initialization]]"
  - "[[Backpropagation]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Techniques/Activation Functions.md]]"
---

# Activation Functions

The non-linearity `g` applied after each layer's linear step `z = Wa + b`.

## Why non-linear?

Without one, any stack of layers collapses to a single linear map, no better than [[Logistic Regression]]. Linear (identity) activation is only sensible in the **output** layer of a regression model, and ReLU often works there too if outputs are non-negative.

## Common choices

| Function | Formula | Derivative | Range | Notes |
|----------|---------|-----------|-------|-------|
| Sigmoid | `1 / (1 + e^-z)` | `g(1 - g)` | (0, 1) | Use for a binary output layer only |
| Tanh | `(e^z - e^-z)/(e^z + e^-z)` | `1 - g^2` | (-1, 1) | Zero-centered, usually beats sigmoid in hidden layers |
| ReLU | `max(0, z)` | 0 if z<0, else 1 | [0, inf) | Default for hidden layers; trains fast |
| Leaky ReLU | `max(0.01 z, z)` | 0.01 if z<0, else 1 | (-inf, inf) | Avoids "dead" units; slope can be learned |
| Softmax | `e^z_i / sum_j e^z_j` | (see source) | simplex | Multiclass output, see [[Softmax Regression]] |

Sigmoid and tanh saturate: for large `|z|` the slope is near zero and learning crawls. That saturation is a main cause of [[Vanishing and Exploding Gradients]], and why weights start small (see [[Weight Initialization]]).

## Rule of thumb (Ng)

Hidden layers: ReLU. Output: sigmoid for binary, softmax for multiclass, linear for regression. Otherwise, try several and compare on a dev set.

## Deeper dive

AI-Notes adds an ideal-properties checklist; see the section below.

## AI-Notes perspective: what makes a good activation?

[[ai-notes|AI-Notes]] scores activations against five ideal properties: **non-linear**, **non-saturating** (saturation causes vanishing gradients), **differentiable** (needed for backprop), **cheap to compute**, **zero-centered** (faster convergence).

| Function | Non-linear | Non-saturating | Differentiable | Cheap | Zero-centered |
|----------|-----------|----------------|----------------|-------|---------------|
| Step | yes (discontinuous) | no | no | yes | no |
| Sigmoid | yes | no | yes | no (exp) | no |
| Tanh | yes | no | yes | no (exp) | yes |
| ReLU | yes | positive side only | almost everywhere | yes | no |

(The source table has a few inconsistent ticks, for example marking sigmoid both "computationally expensive" and ideal; this table records the intended meaning.)

**Dead neurons (dying ReLU):** a unit whose input stays negative outputs 0 with 0 gradient, so it never recovers. Many dead units cause underfitting. Variants:

- **Leaky ReLU**: `alpha * x` for `x < 0`, with fixed `alpha` (say 0.01).
- **Parametric ReLU (PReLU)**: `alpha` is learned.
- **ELU**: `alpha * (e^x - 1)` for `x < 0`. Smooth and near zero-mean, so faster convergence.

**Output-layer cheat sheet:** binary classification uses ReLU hidden and sigmoid out; multiclass uses ReLU hidden and softmax out; regression uses ReLU hidden and linear out.

**Regression losses:** MSE, MAE, and **Huber** (MSE near 0, MAE in the tails, robust to outliers). The source's loss-function page ([[ai-notes|AI-Notes]] `Loss Functions.md`) is otherwise a stub.
