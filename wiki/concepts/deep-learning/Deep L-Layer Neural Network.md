---
type: concept
title: "Deep L-Layer Neural Network"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
complexity: intermediate
domain: deep-learning
status: developing
address: c-000146
related:
  - "[[Backpropagation]]"
  - "[[Parameters vs Hyperparameters]]"
  - "[[Multilayer Perceptron]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
---

# Deep L-Layer Neural Network

A fully connected network with `L` layers (the input layer is not counted). A network with one hidden layer is "shallow"; DLAI calls three or more layers "deep".

## Notation (DLAI)

- `n[l]`: units in layer `l`; `n[0] = n_x`; `n[L]` = outputs.
- `g[l]`: activation of layer `l`; `a[l] = g[l](z[l])`; `a[0] = x`; `a[L] = y_hat`.

## Forward propagation

```
Z[l] = W[l] A[l-1] + b[l]
A[l] = g[l](Z[l])
```

A loop over layers is unavoidable. Cache `Z[l]` for the backward pass ([[Backpropagation]]).

## Getting dimensions right

| Quantity | Shape |
|----------|-------|
| `W[l]`, `dW[l]` | `(n[l], n[l-1])` |
| `b[l]`, `db[l]` | `(n[l], 1)` |
| `Z[l]`, `A[l]`, `dZ[l]`, `dA[l]` | `(n[l], m)` |

Ng's tip: check these with pencil and paper before debugging anything else.

## Why depth helps

Layers compose features from simple to complex: edges, then face parts, then faces; or audio features, then phonemes, then words, then sentences. Circuit theory argues some functions need exponentially many units in a shallow network but only `O(log n)` layers in a deep one (example: XOR of n bits).

Even so, start with the simplest model that might work and add depth only as needed.

## Building blocks

Each layer is a forward block (input `A[l-1]`, output `A[l]` plus cache) paired with a backward block (input `dA[l]`, outputs `dA[l-1]`, `dW[l]`, `db[l]`). Training is: forward through all blocks, compute cost, backward through all blocks, update.
