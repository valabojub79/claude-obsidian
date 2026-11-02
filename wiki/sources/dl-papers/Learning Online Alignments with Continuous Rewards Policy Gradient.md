---
type: source
title: "Learning Online Alignments with Continuous Rewards Policy Gradient"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1608.01281"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - speech
  - reinforcement-learning
  - attention
status: ingested
address: c-000257
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Speech Recognition and CTC]]"
  - "[[Recurrent Models of Visual Attention]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/online-alignments-pg.md]]"
---

# Learning Online Alignments with Continuous Rewards Policy Gradient

[Paper](https://arxiv.org/abs/1608.01281) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Luo et al. train an RNN with a **hard, online attention** decision (emit an output at this step or not) using policy gradients, so it doesn't need the whole input first, unlike soft attention. Comparable to standard sequence models on small and medium speech recognition tasks.

## Notes

- **Entropy regularization and baselines** were critical.
- Trick: **increase dropout** as training progresses.
- Grid LSTMs beat standard LSTMs.
