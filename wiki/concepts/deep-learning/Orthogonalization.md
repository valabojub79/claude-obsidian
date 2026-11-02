---
type: concept
title: "Orthogonalization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: beginner
domain: deep-learning
status: developing
address: c-000187
related:
  - "[[DLAI Course 3 - Structuring Machine Learning Projects]]"
  - "[[Regularization]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Orthogonalization

Design your tuning "knobs" so that each one affects exactly one thing, like the separate steering and speed controls of a car.

## The chain of assumptions

| Goal | If it fails, turn this knob |
|------|-----------------------------|
| 1. Fit the training set well (near human level) | Bigger network, better optimizer (Adam) |
| 2. Fit the dev set well | [[Regularization]], bigger training set |
| 3. Fit the test set well | Bigger dev set (you overfit dev) |
| 4. Perform well in the real world | Change the dev set or the cost function |

## Consequences

- Ng avoids **early stopping**: it simultaneously affects goal 1 (stops fitting train) and goal 2 (reduces overfitting), so it is not an orthogonal knob.
- Defining a metric (placing the target) and optimizing it (hitting the target) are separate steps. See [[Evaluation Metrics and Dev Sets]].
