---
type: source
title: "Progressive Neural Networks"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1606.04671"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - transfer-learning
  - continual-learning
  - reinforcement-learning
status: ingested
address: c-000279
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Transfer Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/progressive-nn.md]]"
---

# Progressive Neural Networks

[Paper](http://arxiv.org/abs/1606.04671) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Rusu et al. (DeepMind) do transfer **without forgetting**. Train column 1 on task 1 and freeze it. For task 2 add a new column with learned **lateral connections** (with adapters) from the frozen columns' layer `k-1` to the new column's layer `k`. Repeat per task. Beats fine-tuning on Pong variants, Atari games and 3D Labyrinth.

## Key points

- Fine-tuning is destructive (catastrophic forgetting).
- Parameters grow **quadratically** with the number of tasks.
- Metric: AUC (mean score during training) and a transfer score relative to a single-network baseline. Average Perturbation and Fisher Sensitivity reveal which old features get reused.
- Positive transfer in 8 of 12 Atari pairs, negative in 2. Fine-tuning only the last layer **fails** in most experiments.

## Critique (Denny Britz)

Why assume layer `k` should read from layer `k-1` of every column (different tasks may need different depths)? All-to-all connections don't scale. Old tasks can't benefit from new ones. Gating or residual laterals might help. Why AUC rather than final score? It's alarming that last-layer fine-tuning fails, given how common it is outside RL. Try non-RL tasks; training cost grows with columns.
