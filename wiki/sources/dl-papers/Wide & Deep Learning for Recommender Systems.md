---
type: source
title: "Wide & Deep Learning for Recommender Systems"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1606.07792"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - recommender-systems
  - production
status: ingested
address: c-000304
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Multi-Task Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/wide-and-deep.md]]"
---

# Wide & Deep Learning for Recommender Systems

[Paper](https://arxiv.org/abs/1606.07792) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Cheng et al. (Google) **jointly** train:

- a **wide** linear model over sparse **cross-product** features (for example `AND(installed=netflix, impression=pandora)`), good at **memorization**;
- a **deep** network over embedded sparse features, good at **generalization** to unseen combinations. Deep alone over-generalizes when most crosses have no data.

Trained on **500B examples**; deployed in **Google Play** with a **+3.9% app acquisition** lift in A/B tests. Open-sourced in TensorFlow (`DNNLinearCombinedClassifier`).

## Connections

A template for production recommenders (DeepFM, DCN follow). [[ai-notes|AI-Notes]] covers recommender basics in its ML sections.
