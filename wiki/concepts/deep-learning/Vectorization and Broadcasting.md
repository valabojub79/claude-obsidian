---
type: concept
title: "Vectorization and Broadcasting"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - numpy
complexity: beginner
domain: deep-learning
status: developing
address: c-000202
related:
  - "[[Logistic Regression]]"
  - "[[Deep L-Layer Neural Network]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
---

# Vectorization and Broadcasting

## Vectorization

Replace explicit Python `for` loops with whole-array operations (`np.dot`, `np.exp`, `np.sum`). NumPy dispatches these to SIMD instructions on CPU or GPU, often 100x+ faster. Rule: avoid explicit loops over examples whenever possible. The loop over *layers* in a deep network is acceptable.

Stack examples as columns (`X` is `(n_x, m)`) so one matrix product handles the whole batch.

## Broadcasting

When shapes do not match, NumPy stretches the smaller array:

- `(m, n) op (1, n)`: the row is copied `m` times.
- `(m, n) op (m, 1)`: the column is copied `n` times.

That is how `np.dot(W.T, X) + b` adds a scalar bias to every column.

## Shape-bug hygiene

- Avoid rank-1 arrays of shape `(m,)`: transposing them does nothing. Use `(m, 1)` or `(1, m)`.
- `assert a.shape == (5, 1)` liberally; `reshape` is cheap.
- `sum(axis=0)` sums down columns, `axis=1` across rows. Use `keepdims=True` in backprop.
- Flatten an image `(h, w, c)` to a column with `img.reshape(-1, 1)`.

## Related

Python background: [[Python Iterators and Generators]] and [[Object-Oriented Programming in Python]] (AI-Notes' Python data-structure pages are empty stubs).
