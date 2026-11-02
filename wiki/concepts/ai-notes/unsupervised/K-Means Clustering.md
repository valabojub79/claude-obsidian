---
type: concept
title: "K-Means Clustering"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - unsupervised
  - clustering
complexity: intermediate
domain: machine-learning
status: developing
address: c-000404
related:
  - "[[Clustering Algorithms]]"
  - "[[Clustering Metrics]]"
  - "[[Hierarchical Clustering]]"
sources:
  - "[[.raw/repos/AI-Notes/Unsupervised Learning/Clustering Algorithms/Partition based clustering.md]]"
---

# K-Means Clustering

Partition (centroid-based) clustering. From [[ai-notes|AI-Notes]].

## Algorithm (Lloyd's)

1. Initialize `k` centroids.
2. **Assign** each point to its nearest centroid (Euclidean distance).
3. **Update** each centroid to the mean of its assigned points.
4. Repeat 2 and 3 until centroids stop moving (or a maximum number of iterations).

It minimizes **WCSS (inertia)**: `sum_k sum_{x in C_k} ||x - mu_k||^2`.

## Choosing K

- **Elbow method**: plot inertia against `k` and pick the "elbow" where the decrease flattens. Imprecise and subjective.
- **Silhouette method**: pick the `k` with the highest mean silhouette `s = (b - a) / max(a, b)`, where `a` is the mean intra-cluster distance (cohesion) and `b` the mean distance to the nearest other cluster (separation). Range -1 to 1: near +1 means well clustered; near 0 means on a boundary; negative means probably misassigned. See [[Clustering Metrics]].

## Drawbacks

1. **Sensitive to initialization**: bad starts give poor optima and slow convergence. Run several inits (`n_init`).
2. **K must be chosen** in advance.
3. Assumes **spherical, similar-sized** clusters (and is sensitive to scale and outliers). For other shapes see [[Hierarchical Clustering]] or DBSCAN ([[Clustering Algorithms]]).

## K-Means++ initialization

1. Pick the first centroid uniformly at random.
2. For each point, compute `D(x)`, the distance to the nearest chosen centroid.
3. Choose the next centroid with probability proportional to `D(x)^2`.
4. Repeat until there are `k` centroids.

**Why not just take the farthest point?** It would often pick **outliers**. Sampling proportional to `D^2` favors spread-out choices but still lets typical points win: a balance of exploration and robustness. (Default in scikit-learn.)

Fuzzy C-Means: soft memberships instead of hard assignments.
