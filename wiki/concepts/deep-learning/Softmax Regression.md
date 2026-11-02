---
type: concept
title: "Softmax Regression"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - classification
complexity: beginner
domain: deep-learning
status: developing
address: c-000195
related:
  - "[[Logistic Regression]]"
  - "[[Activation Functions]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Softmax Regression

Generalizes [[Logistic Regression]] to `C` classes. The output layer has `C` units; softmax turns their logits into a probability distribution:

```
t     = exp(Z[L])                 # (C, m)
A[L]  = t / sum(t, axis=0)        # columns sum to 1
```

Labels are one-hot vectors, for example `[0, 1, 0, 0]` for class 1.

"Soft" max contrasts with **hard max** (1 for the argmax, 0 elsewhere). With `C = 2`, softmax reduces to logistic regression.

## Loss

Categorical cross-entropy:

```
L(y, y_hat) = - sum_j y_j log(y_hat_j)
J = (1/m) * sum_i L(y_i, y_hat_i)
```

## Backprop

The softmax Jacobian combined with cross-entropy collapses to:

```
dZ[L] = Y_hat - Y
```

the same form as the sigmoid plus log-loss case.

## Related

- [[LISA Tutorial - Logistic Regression]] implements exactly this on MNIST in Theano.
- Used as the output of nearly every classifier: [[Convolutional Neural Networks]], language models.
