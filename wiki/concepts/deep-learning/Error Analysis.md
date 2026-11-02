---
type: concept
title: "Error Analysis"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: beginner
domain: deep-learning
status: developing
address: c-000152
related:
  - "[[Human-Level Performance]]"
  - "[[Data Mismatch]]"
  - "[[DLAI Course 3 - Structuring Machine Learning Projects]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Error Analysis

Manually inspect the examples your model gets wrong, so you know where effort will pay off before spending weeks on it.

## Ceiling analysis

Dev error is 10%. Should you fix dogs being misread as cats?

1. Sample about 100 misclassified dev examples.
2. Count dogs. If 5 of 100, a perfect fix only gets you to 9.5% error; probably not worth it. If 50, you could get to 5%.

## Evaluate several ideas in parallel

A spreadsheet with one row per error and one column per hypothesis:

| Image | Dog | Great cat | Blurry | Instagram filter | Mislabeled | Comment |
|-------|-----|-----------|--------|------------------|-----------|---------|
| 1 | x | | | x | | Pitbull |
| 2 | x | | x | x | | |
| ... | | | | | | |
| **%** | 8% | 43% | 61% | 12% | 6% | |

This takes a few hours and turns gut feeling into priorities (here: great cats and blur).

## Mislabeled data

- Deep learning is robust to **random** label noise in the training set, less so to **systematic** noise.
- In dev and test, add a "mislabeled" column. With 10% dev error and 6% of errors mislabeled, labels cost 0.6% while 9.4% comes from elsewhere: fix that first. If dev error is 2% and 0.6% is labels, cleaning labels becomes worthwhile.
- When fixing, apply the **same process to dev and test** so they stay one distribution; consider checking examples the model got right too; the train set can stay a slightly different distribution.

## Build fast, then iterate

Set dev/test and metric, build a quick first system, then let bias/variance and error analysis decide the next step. Don't over-engineer v1 (unless the problem is well studied in the literature).
