---
type: concept
title: "Measures of Dispersion"
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
address: c-000350
related:
  - "[[Measures of Central Tendency]]"
  - "[[Outliers]]"
  - "[[Principal Component Analysis]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Measure of CT.md]]"
---

# Measures of Dispersion

How spread out the data is. From [[ai-notes|AI-Notes]] (`Measure of CT.md`; the dedicated `Measure of Dispersion.md` is empty).

| Measure | Formula | Notes |
|---------|---------|-------|
| **Range** | `max - min` | Simple; very outlier-sensitive |
| **Variance** | Population `sum (x - mu)^2 / N`; sample `sum (x - x_bar)^2 / (n - 1)` | Squared units; outlier-sensitive; mathematically convenient (ANOVA, MSE, PCA) |
| **Standard deviation** | `sqrt(variance)` | Original units; interpretable (finance volatility, quality control) |
| **IQR** | `Q3 - Q1` | Robust; the basis of box plots and outlier fences `Q1 - 1.5 IQR`, `Q3 + 1.5 IQR` ([[Outliers]]) |
| **Mean absolute deviation** | `sum |x - x_bar| / n` | Robust-ish, but not differentiable at 0, so it's rarely an optimization target (cf. [[Principal Component Analysis]]) |
| **Coefficient of variation** | `sigma / mu * 100%` | **Unit-free**, compares relative spread across datasets; meaningless when the mean is near 0 or negative |

**Why `n - 1`?** Bessel's correction: the sample mean is fitted to the same data, so it uses up one degree of freedom; dividing by `n - 1` makes the sample variance unbiased.

**Variance vs standard deviation**: use variance in theory and computation (it adds up; ANOVA, regression), and standard deviation to communicate. (The source's claim that the standard deviation is "less sensitive to outliers" isn't really right: both are driven by squared deviations. The IQR and MAD are the robust options.)

Related: the [[Empirical Rule]] for normal data.
