---
type: concept
title: "Categorical Encoding"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - feature-engineering
complexity: beginner
domain: machine-learning
status: developing
address: c-000375
related:
  - "[[Multicollinearity]]"
  - "[[Feature Scaling]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Categorical Encoding.md]]"
---

# Categorical Encoding

Models need numbers, so categorical columns must be encoded. From [[ai-notes|AI-Notes]].

## Feature types and encoders

| Type | Example | Encoder |
|------|---------|---------|
| **Ordinal** (ordered) | Bachelors < Masters < PhD | `OrdinalEncoder` with an explicit category order |
| **Nominal** (unordered) | Red, Green, Blue | **One-hot**; target encoding if high cardinality |
| **Target labels** | "spam", "ham" | `LabelEncoder` (for `y` only) |

## One-hot encoding

Create one 0/1 column per category (`pd.get_dummies`, `OneHotEncoder`). Drawbacks:

1. **High cardinality** means many columns (curse of dimensionality).
2. **Dummy-variable trap**: the columns sum to 1, which is **perfect [[Multicollinearity]]** and breaks OLS. Fix with `drop='first'` (k-1 columns).

## Target (mean) encoding

For high-cardinality nominal features: replace each category with the **mean target** for that category. For a multi-class target, label-encode it first (as the source does: Low=1, Medium=2, High=3, so A becomes (1+2+3)/3 = 2); or, more properly, use one encoded column per class probability.

**Risks**: rare categories overfit, and the target leaks.

- **Smoothing**: `enc = (n * cat_mean + m * global_mean) / (n + m)` pulls rare categories toward the global mean.
- **K-fold target encoding**: compute encodings out of fold so a row never sees its own target.

Other options: frequency or count encoding, binary or hash encoding, embeddings (neural nets; see [[Word Embeddings]]).
