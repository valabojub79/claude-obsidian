---
type: concept
title: "Data Mismatch"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: intermediate
domain: deep-learning
status: developing
address: c-000145
related:
  - "[[Bias and Variance]]"
  - "[[Train Dev Test Split]]"
  - "[[Error Analysis]]"
  - "[[Data Augmentation]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Data Mismatch

Deep learning is data-hungry, so training data often comes from a different distribution than the dev and test data you care about (web images vs phone photos; generic speech vs in-car commands).

## How to split

- **Don't** shuffle everything together: the dev set would then be mostly the wrong distribution.
- **Do** put only target-distribution data in dev and test; put the rest (plus some target data) in training. The target is right, even though train and dev now differ.

## Train-dev set

Hold out a random slice of the **training** distribution. Then:

| Human | Train | Train-dev | Dev | Diagnosis |
|-------|-------|-----------|-----|-----------|
| 0% | 1% | 9% | 10% | Variance |
| 0% | 1% | 1.5% | 10% | **Data mismatch** |
| 10% | 11% | 12% | 20% | Avoidable bias + data mismatch |

```
avoidable bias = train - human
variance       = train-dev - train
data mismatch  = dev - train-dev
dev overfit    = test - dev
```

## Addressing it (no systematic recipe)

1. Do [[Error Analysis]] on train vs dev to understand how they differ (noise? accents? blur?).
2. Make training data more similar, or collect more dev-like data.
3. **Artificial data synthesis**: add car noise to clean speech; render cars with 3D graphics.

Caution: if you synthesize from a tiny subset (one hour of car noise looped over 10,000 hours of speech; the 20 car models in a video game), the network may overfit that subset even though it sounds fine to a human.
