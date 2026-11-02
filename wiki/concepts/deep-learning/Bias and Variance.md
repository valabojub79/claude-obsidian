---
type: concept
title: "Bias and Variance"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: beginner
domain: deep-learning
status: developing
address: c-000136
related:
  - "[[Train Dev Test Split]]"
  - "[[Regularization]]"
  - "[[Human-Level Performance]]"
  - "[[Error Analysis]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Bias and Variance

"Easy to learn, difficult to master." Diagnose from train and dev error, relative to a baseline (human-level or Bayes error):

| Train err | Dev err | Diagnosis |
|-----------|---------|-----------|
| 1% | 11% | High variance (overfitting) |
| 15% | 16% | High bias (underfitting) |
| 15% | 30% | High bias **and** high variance |
| 0.5% | 1% | Low bias, low variance |

The table assumes humans get roughly 0% error. If the task is hard (say humans get 15%), the second row is actually fine. Course 3 formalizes this as **avoidable bias** vs variance: [[Human-Level Performance]].

## Basic recipe

1. **High bias?** Bigger network (more units or layers), train longer, better optimizer, different architecture.
2. **High variance?** More data, [[Regularization]] ([[Dropout]], L2, [[Data Augmentation]]), different architecture.
3. Repeat until both are low.

Deep learning weakened the classic "tradeoff": you can usually reduce one without hurting the other.

## Related

- Classical-ML view: [[Bias Variance Tradeoff]].
- With mismatched train and dev distributions, add a train-dev set: [[Data Mismatch]].
