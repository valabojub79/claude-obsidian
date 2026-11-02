---
type: concept
title: "Logistic Regression"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - machine-learning
complexity: beginner
domain: deep-learning
status: developing
address: c-000179
related:
  - "[[Gradient Descent]]"
  - "[[Backpropagation]]"
  - "[[Activation Functions]]"
  - "[[DLAI Course 1 - Neural Networks and Deep Learning]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Machine Learning/Linear Models/Logistic Regression.md]]"
---

# Logistic Regression

A binary classifier, and the smallest possible neural network: one neuron with a sigmoid activation. DLAI uses it as the on-ramp to neural networks (example: "is this image a cat?").

## Model

- Input `x` has `n_x` features; `m` training examples stacked as columns: `X` has shape `(n_x, m)`.
- `y_hat = sigmoid(w^T x + b)`, with `w` of shape `(n_x, 1)` and scalar `b`.
- Ng prefers keeping `b` separate over folding it into `w` as `w0` with `x0 = 1`.

A perceptron applies a hard threshold to `w^T x + b`, so tiny weight changes can flip its output. Swapping the threshold for a sigmoid makes the output change smoothly, which is what makes gradient-based learning work.

## Loss and cost

Squared error makes the optimization non-convex, so instead use cross-entropy (log loss):

```
L(y_hat, y) = -( y log(y_hat) + (1 - y) log(1 - y_hat) )
J(w, b)     = (1/m) * sum_i L(y_hat_i, y_i)
```

- If `y = 1`, loss is `-log(y_hat)`: pushes `y_hat` toward 1.
- If `y = 0`, loss is `-log(1 - y_hat)`: pushes `y_hat` toward 0.
- **Loss** is per example; **cost** is the average over the training set.

## Gradients

With `a = sigmoid(z)`:

```
dz = a - y
dw = x * dz      (averaged over m)
db = dz          (averaged over m)
```

Vectorized over all examples:

```python
Z  = np.dot(w.T, X) + b
A  = 1 / (1 + np.exp(-Z))
dZ = A - Y
dw = np.dot(X, dZ.T) / m
db = np.sum(dZ) / m
```

Because `J` is convex for logistic regression, zero initialization is fine. That is not true for networks with hidden layers (see [[Weight Initialization]]).

## In other sources

- [[LISA Tutorial - Logistic Regression]] builds the multiclass (softmax) version on MNIST.
- [[Softmax Regression]] generalizes it to C classes.

## AI-Notes perspective: the classical-ML view

[[ai-notes|AI-Notes]] (CampusX, *Hands-On ML*):

- **Why "regression"?** It belongs to the linear-model family and fits a **linear decision boundary**; on non-linearly separable data it struggles unless you engineer features.
- **History, the perceptron trick**: early logistic regression updated the boundary with a step function, which gives no notion of *how good* a boundary is. Replacing the step with a **sigmoid** gives probabilities (confidence), and the objective becomes **maximizing likelihood**.
- **Deriving binary cross-entropy from MLE**: likelihood = product of the probabilities of each point's true class. Take logs (to avoid underflow), giving a sum of `y log y_hat + (1-y) log(1 - y_hat)`. Negate so it becomes a loss to **minimize**. Then [[Gradient Descent]].
- **Multiclass**:
  - **One-vs-Rest (OvR)**: K binary classifiers; pick the highest positive probability. Useful when labels **aren't mutually exclusive** or classes are imbalanced, but expensive with many classes.
  - **Multinomial / softmax regression** with categorical cross-entropy (see [[Softmax Regression]]).
