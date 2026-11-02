---
type: concept
title: "Clustering Algorithms"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - unsupervised
  - clustering
complexity: beginner
domain: machine-learning
status: developing
address: c-000401
related:
  - "[[K-Means Clustering]]"
  - "[[Hierarchical Clustering]]"
  - "[[Clustering Metrics]]"
sources:
  - "[[.raw/repos/AI-Notes/Unsupervised Learning/Clustering Algorithms/Partition based clustering.md]]"
---

# Clustering Algorithms

Group unlabeled points so that points within a cluster are similar and points in different clusters are dissimilar. Hub page for [[ai-notes|AI-Notes]]' unsupervised section.

| Family | Algorithms | Cluster shape | Need K? | Page |
|--------|-----------|---------------|---------|------|
| Partition / centroid | K-Means, K-Means++, Fuzzy C-Means | Spherical, similar size | Yes | [[K-Means Clustering]] |
| Hierarchical | AGNES (agglomerative), DIANA (divisive), CURE, Chameleon | Flexible (depends on linkage) | No (cut the dendrogram) | [[Hierarchical Clustering]] |
| Density-based | DBSCAN, OPTICS, HDBSCAN | Arbitrary; finds noise points | No | (source stub) |

Evaluate with [[Clustering Metrics]]. Related unsupervised tools: [[Principal Component Analysis]] (dimensionality reduction), [[Autoencoders]].

> [!gap] Missing source content
> `Density Based Clustering.md` and the autoencoder page in AI-Notes' dimensionality-reduction folder are empty. DBSCAN groups points with at least `minPts` neighbors within radius `eps`, and labels the rest noise; that makes it useful for [[Outliers]].
