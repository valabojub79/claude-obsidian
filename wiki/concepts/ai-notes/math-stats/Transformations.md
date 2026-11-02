---
type: concept
title: "Transformations"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - feature-engineering
  - statistics
complexity: beginner
domain: mathematics
status: seed
address: c-000355
related:
  - "[[Log Normal Distribution]]"
  - "[[Outliers]]"
  - "[[Naive Bayes]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Linear Algebra/Transformations.md]]"
---

# Mathematical Transformations

Referenced throughout [[ai-notes|AI-Notes]] (for Gaussian [[Naive Bayes]], [[Outliers]], linear models), but the source page is a stub. Standard options:

| Transform | Good for | Caveat |
|-----------|----------|--------|
| `log(x)` / `log1p(x)` | Right skew ([[Log Normal Distribution]]) | Needs x > 0 (or x >= 0 with log1p). Applying it carelessly creates `NaN`s and outliers, a cause the AI-Notes [[Missing Values]] page mentions |
| `sqrt(x)` | Counts, moderate skew | x >= 0 |
| Reciprocal `1/x` | Strong skew | x != 0 |
| **Box-Cox** | Learns the power lambda | x > 0 |
| **Yeo-Johnson** | Like Box-Cox | Handles 0 and negatives |
| Quantile transform | Maps to uniform or normal by rank | Nonparametric; distorts distances |

Check normality with Q-Q plots. scikit-learn: `PowerTransformer`, `QuantileTransformer`, `FunctionTransformer`.

> [!gap] Source stub
> `Mathematics/Linear Algebra/Transformations.md` is 23 bytes. The linear-algebra sense (matrices as linear transformations) is covered in [[Principal Component Analysis]].
