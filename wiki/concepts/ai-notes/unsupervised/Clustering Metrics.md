---
type: concept
title: "Clustering Metrics"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - unsupervised
  - evaluation
complexity: intermediate
domain: machine-learning
status: developing
address: c-000402
related:
  - "[[K-Means Clustering]]"
  - "[[Classification Metrics]]"
sources:
  - "[[.raw/repos/AI-Notes/Unsupervised Learning/Clustering Algorithms/Clustering Metrics.md]]"
---

# Clustering Metrics

From [[ai-notes|AI-Notes]].

## Internal (no ground truth)

| Metric | Measures | Better |
|--------|----------|--------|
| **Silhouette** | Cohesion vs separation per point, `(b - a)/max(a, b)` | Higher (range -1 to 1) |
| **Davies-Bouldin** | Average similarity of each cluster to its most similar cluster | **Lower** |
| **Dunn index** | Minimum inter-cluster distance / maximum intra-cluster diameter | Higher |
| **WCSS / inertia / SSE** | Within-cluster variance | Lower (always falls as K grows, hence the elbow method) |
| **Calinski-Harabasz** (variance ratio) | Between-cluster / within-cluster dispersion | Higher |

## External (with ground-truth labels)

| Metric | Notes | Range |
|--------|-------|-------|
| **Adjusted Rand Index** | Pair agreement, chance-corrected | -1 to 1 (0 is random) |
| **Normalized Mutual Information** | Shared information | 0 to 1 |
| **Fowlkes-Mallows** | Geometric mean of pairwise precision and recall | 0 to 1 |
| **Homogeneity / Completeness / V-measure** | Each cluster is one class / each class is one cluster / their harmonic mean | 0 to 1 |
| Pairwise precision, recall, F1 | Over point pairs | 0 to 1 |

Used for choosing K in [[K-Means Clustering]]; compare [[Classification Metrics]].
