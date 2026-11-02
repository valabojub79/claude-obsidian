---
type: concept
title: "LISA Tutorial - Logistic Regression"
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
address: c-000171
related:
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
  - "[[Logistic Regression]]"
  - "[[Softmax Regression]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/logreg.txt]]"
---

# LISA Tutorial: Logistic Regression on MNIST

The first algorithm tutorial in [[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]: multiclass (softmax) logistic regression in Theano. It's the [[Softmax Regression]] of DLAI Course 2.

## Model

```
P(Y = i | x, W, b) = softmax_i(W x + b) = exp(W_i x + b_i) / sum_j exp(W_j x + b_j)
y_pred = argmax_i P(Y = i | x)
```

Geometrically: one hyperplane per class; distance to it reflects class probability.

## Loss

Mean negative log-likelihood over the minibatch. In Theano, `-T.mean(T.log(p_y_given_x)[T.arange(y.shape[0]), y])` (index the log-probability of each correct label). Using the mean rather than the sum makes the learning rate less sensitive to batch size.

## Theano patterns introduced

- Parameters `W` and `b` as **shared variables** (persistent state).
- A `LogisticRegression` class whose `__init__` takes the symbolic **input**, so layers can be chained into deeper networks (reused by the MLP and LeNet tutorials).
- `T.grad(cost, W)` does **automatic differentiation**; no hand-derived gradients.
- `theano.function(inputs=[index], outputs=cost, updates=[(W, W - lr*g_W), ...], givens={x: train_x[index*B:(index+1)*B], ...})`: one compiled step of MSGD with the data sliced from shared memory.
- `errors(y)` counts misclassifications for `validate_model` and `test_model`.

## Results

Batch size 600, 75 epochs to **7.49% test error**; about 1.9 epochs/s on a Core 2 Duo, about 10 epochs/s on GPU. The model is pickled at each new best validation score and reloaded by `predict()`.

`logistic_cg.py` shows SciPy conjugate gradient instead of SGD, which is better for small data and models.

## Takeaway

Even the simplest model shows the "symbolic graph, then compile, then run" workflow that later frameworks (TensorFlow 1.x) copied. See [[Deep Learning Frameworks]].
