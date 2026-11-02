---
type: concept
title: "Backpropagation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
complexity: intermediate
domain: deep-learning
status: developing
address: c-000133
related:
  - "[[Gradient Descent]]"
  - "[[Deep L-Layer Neural Network]]"
  - "[[Gradient Checking]]"
  - "[[Vanishing and Exploding Gradients]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
---

# Backpropagation

Computing the gradient of the cost with respect to every parameter by applying the chain rule backward over a **computation graph**.

## Computation graph

Lay the computation out left to right (forward pass). Then walk right to left: if `x -> y -> z`, then `dz/dx = dz/dy * dy/dx`. In DLAI code, `dvar` names the derivative of the final cost with respect to `var`.

## Two-layer network (one hidden layer)

Forward:

```
Z1 = W1 X + b1;   A1 = g1(Z1)
Z2 = W2 A1 + b2;  A2 = sigmoid(Z2)
```

Backward (cross-entropy loss, sigmoid output):

```
dZ2 = A2 - Y
dW2 = dZ2 A1^T / m
db2 = sum(dZ2, axis=1, keepdims=True) / m
dZ1 = (W2^T dZ2) * g1'(Z1)        # * is element-wise
dW1 = dZ1 X^T / m
db1 = sum(dZ1, axis=1, keepdims=True) / m
```

## General layer l

```
dZ[l]   = dA[l] * g[l]'(Z[l])
dW[l]   = dZ[l] A[l-1]^T / m
db[l]   = sum(dZ[l], axis=1, keepdims=True) / m
dA[l-1] = W[l]^T dZ[l]
```

Initialize with `dA[L] = -(y/a) + (1-y)/(1-a)` for the cross-entropy loss. The forward pass caches `Z[l]` (and `A[l-1]`, `W[l]`) for reuse here. See [[Deep L-Layer Neural Network]].

## Related

- Gradients can vanish or explode in deep nets: [[Vanishing and Exploding Gradients]].
- Through time in RNNs: [[Recurrent Neural Networks]].
- Debug with [[Gradient Checking]].
