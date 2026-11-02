---
type: concept
title: "Regularization in Machine Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - regularization
  - ml-fundamentals
complexity: intermediate
domain: machine-learning
status: developing
address: c-000384
related:
  - "[[Regularization]]"
  - "[[Ridge Regression]]"
  - "[[Lasso Regression]]"
  - "[[Dropout]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Regularization.md]]"
---

# Regularization in Machine Learning

Techniques that reduce **overfitting** by limiting effective model capacity, trading a little bias for less variance. From [[ai-notes|AI-Notes]], which uses this page as an index. The neural-network view (L2 weight decay, dropout, data augmentation, early stopping) is [[Regularization]].

## Per algorithm

| Model | How it's regularized |
|-------|---------------------|
| Linear and logistic regression, polynomial regression | L1 ([[Lasso Regression]]), L2 ([[Ridge Regression]]), both ([[Elastic Net Regression]]) |
| [[Decision Tree]] | **Pruning** (pre: depth and sample limits; post: cost-complexity) |
| [[Naive Bayes]] | **Smoothing** (alpha) |
| [[Support Vector Machine]] | Soft margin: **slack variables** with penalty `C` |
| Ensembles | Bagging (variance), shrinkage and subsampling in boosting |
| Neural networks | L1/L2 (`tf.keras.regularizers.l2(0.01)` per layer), [[Dropout]], max-norm, [[Batch Normalization]] (side effect), early stopping |

## Dropout notes from *Hands-On ML* (quoted in the source)

- At each step every neuron except the outputs is dropped with probability `p`; there are `2^N` possible thinned networks, so training is like averaging a huge ensemble.
- Neurons can't co-adapt and must be useful on their own, which makes them less sensitive to small input changes.
- **Scaling**: with `p = 75%`, only a quarter of the inputs are active during training. To keep scales consistent, **divide by the keep probability `(1 - p)` during training** (inverted dropout), the Keras behavior. (This agrees with DLAI and corrects the AI-Notes [[Dropout]] page's test-time-scaling claim.)
- Because dropout is active only during training, compare **training loss evaluated without dropout** against validation loss; otherwise overfitting can hide.
- Use `functools.partial` to avoid repeating regularizer and initializer arguments on every layer.
