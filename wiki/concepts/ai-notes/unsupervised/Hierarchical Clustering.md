---
type: concept
title: "Hierarchical Clustering"
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
address: c-000403
related:
  - "[[K-Means Clustering]]"
  - "[[Clustering Algorithms]]"
sources:
  - "[[.raw/repos/AI-Notes/Unsupervised Learning/Clustering Algorithms/Hierarchy based clustering.md]]"
---

# Hierarchical Clustering

Builds a **hierarchy** of clusters, drawn as a **dendrogram** (a tree whose merge heights are distances). From [[ai-notes|AI-Notes]].

**Why not just K-Means?** K-Means needs `k` up front and assumes spherical, similar-sized clusters. Hierarchical clustering makes no shape assumption, and you choose the number of clusters afterwards by cutting the dendrogram.

## Approaches

- **Agglomerative (AGNES, bottom-up)**:
  1. Every point starts as its own cluster.
  2. Build an `n x n` distance matrix.
  3. Merge the closest pair.
  4. Update distances using a **linkage** rule.
  5. Repeat until one cluster remains or a stopping criterion is met.
- **Divisive (DIANA, top-down)**: start with one cluster and recursively split. (The source section is empty.)

## Linkage

| Linkage | Cluster distance | Tendency |
|---------|------------------|----------|
| Single | **Minimum** pairwise distance | Chaining, long thin clusters |
| Complete | **Maximum** pairwise distance | Compact clusters, sensitive to outliers |
| Average | Mean pairwise distance | In between |
| Centroid | Distance between centroids | |
| (Ward) | Merge that minimizes the increase in WCSS | Like K-Means; the scikit-learn default |

## Stopping

A target number of clusters, or a **distance threshold** above which clusters aren't merged (or, for DIANA, not split further).

## Scaling to big data

Naive agglomerative clustering is about `O(n^2)` memory and `O(n^2 log n)` or worse in time.

- **CURE** (Clustering Using REpresentatives): each cluster keeps **several well-scattered representative points**, shrunk toward the centroid by a factor. That handles non-spherical, unevenly sized clusters and dampens outliers. Starts from single-link initial clusters, then shrinks and merges.
- **Chameleon**: merges by dynamic modeling of inter- and intra-cluster connectivity and closeness (the source section is empty).
