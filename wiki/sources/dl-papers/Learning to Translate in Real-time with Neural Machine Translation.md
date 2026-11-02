---
type: source
title: "Learning to Translate in Real-time with Neural Machine Translation"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1610.00388"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - reinforcement-learning
  - simultaneous-translation
status: ingested
address: c-000260
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Dual Learning for Machine Translation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/learning-to-translate-real-time.md]]"
---

# Learning to Translate in Real-time with Neural Machine Translation

[Paper](https://arxiv.org/abs/1610.00388) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Gu et al. do **simultaneous translation**. An RL agent decides at each step to **READ** another source word or **WRITE** a target word, on top of a pretrained NMT model. Reward combines quality (BLEU) and **delay** (several latency metrics and targets). Trained with policy gradient. On WMT'15 EN-DE and EN-RU it improves quality across settings and trades quality against latency effectively.
