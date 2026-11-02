---
type: concept
title: "Chi Square Test"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - hypothesis-testing
complexity: intermediate
domain: mathematics
status: developing
address: c-000343
related:
  - "[[Hypothesis Testing]]"
  - "[[Feature Selection]]"
  - "[[Bernoulli Distribution]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Chi Square Test.md]]"
---

# Chi-Square Test

From [[ai-notes|AI-Notes]] (CampusX).

## Chi-square distribution

The sum of `k` squared independent standard normals. Mean `k` (degrees of freedom), variance `2k`; right-skewed, approaching normal as `k` grows.

Chi-square **tests** are **non-parametric** (no assumption about the population distribution's parameters, unlike z and t tests).

**Assumptions for both tests**: categorical variables; expected count of at least 5 per cell.

```
chi^2 = sum (Observed - Expected)^2 / Expected
```

## 1. Goodness of fit

Does one categorical variable follow a hypothesized distribution? `df = categories - 1`.

**Example: is the die fair?** 60 rolls gave counts 8, 12, 9, 11, 10, 10; expected 10 each.

```
chi^2 = (4 + 4 + 1 + 1 + 0 + 0) / 10 = 1.0,   df = 5
critical value at alpha = 0.05: 11.07   (p is about 0.96)
```

Since 1.0 < 11.07, **don't reject H0**: no evidence the die is unfair.

> [!contradiction] Critical value vs p-value
> The source calls 11.07 "the p value" and compares it to the statistic. 11.07 is the **critical value**; the p-value for chi-square = 1 with df = 5 is about 0.96. The conclusion (don't reject) is the same.

**ML uses**: check whether predicted class proportions match actual ones; check a feature's distribution before modeling.

## 2. Test of independence

Are two categorical variables associated? Build a **contingency table**; expected count `E_ij = row_i total * col_j total / N`.

```
df = (rows - 1) * (cols - 1)
```

(The source writes `(rows - 1) + (cols - 1)`, which is incorrect.)

**ML use**: filter-based [[Feature Selection]] for categorical features vs a categorical target (`sklearn.feature_selection.chi2`).

Framework: [[Hypothesis Testing]].
