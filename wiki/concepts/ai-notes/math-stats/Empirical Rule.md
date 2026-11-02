---
type: concept
title: "Empirical Rule"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - probability
complexity: beginner
domain: mathematics
status: seed
address: c-000345
related:
  - "[[Outliers]]"
  - "[[Measures of Dispersion]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Empirical Rule.md]]"
---

# Empirical Rule (68-95-99.7)

For a **normal** distribution: about **68%** of values lie within 1 sigma of the mean, **95%** within 2 sigma, and **99.7%** within 3 sigma.

Used in [[ai-notes|AI-Notes]] to flag [[Outliers]] in roughly normal features: anything beyond +/-3 sigma. For skewed data use IQR fences instead ([[Measures of Dispersion]]). Chebyshev's inequality gives distribution-free bounds: at least `1 - 1/k^2` of the values lie within k sigma.

> [!gap] The source page is a title-only stub.
