---
type: concept
title: "Train Dev Test Split"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: beginner
domain: deep-learning
status: developing
address: c-000198
related:
  - "[[Bias and Variance]]"
  - "[[Evaluation Metrics and Dev Sets]]"
  - "[[Data Mismatch]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Train / Dev / Test Split

- **Train set**: fit parameters. Always the largest.
- **Dev set** (hold-out cross-validation set): compare models and tune hyperparameters.
- **Test set**: one unbiased estimate of final performance. Optional; without one, call the held-out set "dev", not "test".

## How big?

| Dataset size | Typical split |
|--------------|---------------|
| 100 to ~1M | 60 / 20 / 20 (or 70 / 30) |
| 1M+ | 98 / 1 / 1, even 99.5 / 0.25 / 0.25 |

Dev and test only need to be big enough to tell models apart and give confidence in the final number. 10,000 examples is often plenty.

## Same distribution

Dev and test must come from the **same distribution**, and that distribution should reflect the data you expect in production. Example: training on web cat photos while users upload phone photos. Put phone photos in dev and test. Training data may differ; see [[Data Mismatch]] for diagnosing that gap.

Course 3 extends this: [[Evaluation Metrics and Dev Sets]].

## Cross-validation

Classic k-fold cross-validation is covered in [[ai-notes|AI-Notes]]: see [[Cross Validation]].
