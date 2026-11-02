---
type: concept
title: "Human-Level Performance"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: intermediate
domain: deep-learning
status: developing
address: c-000160
related:
  - "[[Bias and Variance]]"
  - "[[Error Analysis]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Human-Level Performance

## Why compare to humans

- Deep learning now reaches human-level on many tasks, so it is a natural reference point.
- While a model is worse than humans you can get labels from humans, learn from why a human got an example right, and analyze bias and variance more precisely.
- Progress typically slows after passing human level, approaching **Bayes optimal error**, the best any function can do.

## Human error as a proxy for Bayes error

```
avoidable bias = train error - human error
variance       = dev error   - train error
```

| | Scenario A | Scenario B |
|-|-----------|-----------|
| Human | 1% | 7.5% |
| Train | 8% | 8% |
| Dev | 10% | 10% |
| Focus on | **bias** (7% avoidable) | **variance** (2% vs 0.5%) |

Choose the human baseline that fits your purpose. For Bayes-error estimation in medical imaging, use the **best** (a team of expert doctors, say 0.5%) rather than a typical person (3%).

## Surpassing humans

Common on **structured-data** tasks (online ads, recommendations, logistics, loan approval) with huge datasets. Harder, but increasingly achieved, on natural perception (vision, speech). Past human level, you lose the clear bias/variance signal and the human-labeling advantages.

## Improving a model

1. Large avoidable bias: bigger model, train longer or use a better optimizer, architecture or hyperparameter search.
2. Large variance: more data, regularization (L2, dropout, augmentation), architecture or hyperparameter search.
