---
type: concept
title: "Measures of Central Tendency"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - descriptive
complexity: beginner
domain: mathematics
status: developing
address: c-000349
related:
  - "[[Measures of Dispersion]]"
  - "[[Outliers]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Measure of CT.md]]"
---

# Measures of Central Tendency

From [[ai-notes|AI-Notes]].

**Statistics** = collecting, summarizing and analyzing data. **Descriptive** statistics summarize; **inferential** statistics generalize from samples ([[Confidence Interval]], [[Hypothesis Testing]]).

## The measures

| Measure | Definition | Robust to outliers? | Use |
|---------|-----------|---------------------|-----|
| **Mean** (arithmetic) | `sum x / n` | No | Symmetric data |
| Weighted mean | `sum w x / sum w` | No | Unequal importance |
| Trimmed mean | Mean after dropping the top and bottom k% | Partly | Some outliers |
| Harmonic mean | `n / sum(1/x)` | | Rates; the [[Classification Metrics\|F1 score]] |
| **Median** | Middle value | **Yes** | Skewed data (income) |
| **Mode** | Most frequent value | Yes | Categorical data; imputation of categoricals ([[Missing Values]]) |

## Limitation

A center says nothing about **spread**: two datasets with the same mean can look completely different. That's why you pair it with [[Measures of Dispersion]].

Relationship under skew: right-skewed means mean > median > mode; left-skewed reverses it.
