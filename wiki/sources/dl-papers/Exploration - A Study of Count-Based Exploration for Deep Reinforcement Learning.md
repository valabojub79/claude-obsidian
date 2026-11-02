---
type: source
title: "Exploration - A Study of Count-Based Exploration for Deep Reinforcement Learning"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1611.04717"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
  - exploration
status: ingested
address: c-000244
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Noisy Networks for Exploration]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/count-based-exploration.md]]"
---

# Exploration - A Study of Count-Based Exploration for Deep Reinforcement Learning

[Paper](https://arxiv.org/abs/1611.04717) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** "#Exploration": add an exploration bonus `beta / sqrt(n(phi(s)))` for rarely visited states. Counts come from **locality-sensitive hashing** (SimHash) of raw pixels, or of learned autoencoder codes. This simple method gives solid gains on continuous-control and Atari tasks.

## Critique (Denny Britz)

Simple, but adds hyperparameters: the bonus `beta`, the hash granularity (bits), and the feature representation and its own parameters. Environments need very different settings and results are inconsistent, so it's hard to know what to use in practice.
