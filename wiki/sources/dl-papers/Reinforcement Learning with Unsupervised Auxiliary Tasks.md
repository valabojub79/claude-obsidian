---
type: source
title: "Reinforcement Learning with Unsupervised Auxiliary Tasks"
source_type: paper
year: 2016
url: "http://openreview.net/forum?id=SJ6yPD5xg"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
  - auxiliary-tasks
status: ingested
address: c-000285
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Multi-Task Learning]]"
  - "[[Hindsight Experience Replay]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/rl-auxiliary-tasks.md]]"
---

# Reinforcement Learning with Unsupervised Auxiliary Tasks

[Paper](http://openreview.net/forum?id=SJ6yPD5xg) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Jaderberg et al. (DeepMind) propose **UNREAL**: A3C plus auxiliary tasks sharing the CNN and LSTM trunk. Auxiliary value functions are learned **off-policy** (n-step Q-learning) from a small replay buffer. They only shape the representation, never the policy directly.

## Auxiliary tasks

- **Pixel control**: maximize pixel changes in grid cells.
- **Feature control**: maximize activation of hidden units.
- **Reward prediction**: predict the next reward from a short history, sampled so `P(r != 0) = 0.5`, which counters sparsity.
- **Value-function replay**: extra value regression with varied n-step windows.

## Results

- Labyrinth: human-normalized score 38% to **83%**, and **11x faster** learning across levels. Each task helps independently. Input reconstruction instead **hurts**, since it over-focuses on irrelevant pixels.
- Atari: beats the state of the art and is **more robust to hyperparameters** than A3C.

20-step returns; auxiliary updates every 20 steps; replay of the last 2k transitions.

## Critique (Denny Britz)

"I want an algorithm box please."
