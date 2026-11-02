---
type: source
title: "Noisy Networks for Exploration"
source_type: paper
year: 2017
url: "https://arxiv.org/abs/1706.10295"
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
address: c-000272
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Exploration - A Study of Count-Based Exploration for Deep Reinforcement Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/noisy-networks-4-exploration.md]]"
---

# Noisy Networks for Exploration

[Paper](https://arxiv.org/abs/1706.10295) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Fortunato et al. (DeepMind) add **learned parametric noise to network weights** (`w = mu + sigma * eps`, with `mu` and `sigma` trained by gradient descent). The induced policy randomness drives exploration. Plugged into DQN, Dueling and A3C, NoisyNet substantially improves many Atari games, some going from sub-human to super-human.

## Why weight noise

- epsilon-greedy and entropy bonuses add **local, per-step** dithering, which rarely produces the large-scale behavior changes deep exploration needs.
- Intrinsic-motivation bonuses separate exploration from generalization.
- Evolutionary methods explore well but are data-inefficient and need simulators.
- One weight perturbation yields **consistent, state-dependent** policy changes over many steps; the network learns how much noise to keep.
- Works with any gradient-trained deep RL algorithm. Became part of **Rainbow**.
