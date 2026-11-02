---
type: source
title: "Batch Normalization - Accelerating Deep Network Training"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1502.03167"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - optimization
  - normalization
status: ingested
address: c-000223
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Batch Normalization]]"
  - "[[Layer Normalization]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/batch-normalization.md]]"
---

# Batch Normalization - Accelerating Deep Network Training

[Paper](http://arxiv.org/abs/1502.03167) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Ioffe and Szegedy's *Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift*. Normalize each unit's input to zero mean and unit variance using minibatch statistics, then apply a learned scale and shift. This gives faster training, higher accuracy, and a regularizing effect. A BN ensemble set the ImageNet state of the art at the time.

## Key points

- Motivation: **internal covariate shift**. Higher layers' input distributions change as lower layers learn.
- Only 2 extra parameters per normalized unit.
- Works for fully connected and convolutional layers; RNNs weren't tried.
- **When you add BN:** raise the learning rate, reduce or remove dropout and L2, decay the learning rate faster, shuffle more thoroughly.

## Connections

Concept page: [[Batch Normalization]]. For RNNs, use [[Layer Normalization]] instead. (Later work argues BN helps mainly by smoothing the loss landscape rather than by reducing covariate shift.)
