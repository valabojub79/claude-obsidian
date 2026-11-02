---
type: concept
title: "Confidence Interval"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - inference
complexity: intermediate
domain: mathematics
status: developing
address: c-000344
related:
  - "[[Central Limit Theorem]]"
  - "[[Hypothesis Testing]]"
  - "[[T Test]]"
  - "[[Regression Analysis]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Confidence Interval.md]]"
---

# Confidence Interval

From [[ai-notes|AI-Notes]] (CampusX, *Mastering Statistics* vol. 3).

## Vocabulary

- **Population**: all the data of interest. **Sample**: the subset you observe.
- **Parameter**: a population quantity (`mu`). **Estimate**: computed from a sample (`x_bar`).
- **Descriptive statistics** summarize a sample; **inferential statistics** generalize to the population (confidence intervals, [[Hypothesis Testing]], [[Regression Analysis]]).

## From point estimate to interval

A **point estimate** (say a sample mean height of 168 cm) changes from sample to sample. An interval conveys that uncertainty:

```
CI = point_estimate +/- margin_of_error
MOE = critical_value * standard_error
```

| Procedure | When | SE | Critical value |
|-----------|------|----|----------------|
| **Z** | Population sigma known | `sigma / sqrt(n)` | `z*` (1.96 for 95%) |
| **T** | sigma unknown (use sample `s`) | `s / sqrt(n)` | `t*` with `df = n - 1` |

## What widens or narrows a CI

- Larger sigma (or SE): **wider**.
- Larger `n`: **narrower** (SE shrinks with `sqrt(n)`).
- Higher confidence level (99% vs 95%): **wider**.

(The source labels wider intervals "less reliable". More precisely, a wider interval is less *precise*; at a higher confidence level it is *more* likely to contain the parameter.)

## Interpretation

"95% CI = (45, 70)" means: if we repeated the sampling many times, about **95% of the intervals built this way would contain the true parameter**. It does **not** mean there is a 95% probability that this particular interval contains it.

Uses in ML: error bars on metrics ([[Central Limit Theorem]]), coefficient intervals ([[Regression Analysis]]).
