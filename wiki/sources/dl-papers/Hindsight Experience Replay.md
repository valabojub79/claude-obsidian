---
type: source
title: "Hindsight Experience Replay"
source_type: paper
year: 2017
url: "https://arxiv.org/abs/1707.01495"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
status: ingested
address: c-000251
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Deep Q-learning from Demonstrations]]"
  - "[[Exploration - A Study of Count-Based Exploration for Deep Reinforcement Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/hindsight-ep.md]]"
---

# Hindsight Experience Replay

[Paper](https://arxiv.org/abs/1707.01495) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Andrychowicz et al. (OpenAI) tackle **sparse binary rewards**. If an episode misses goal G, it still reached *some* state; replay the transitions as if that state had been the goal. Requires a **goal-conditioned, off-policy** learner (DQN, DDPG).

## Key points

- Multi-goal RL: a goal is sampled per episode; policy and reward depend on it.
- Extra goals per episode (for example the final state reached) are a hyperparameter; relabeled transitions go into the replay buffer.
- Claimed **implicit curriculum**: as the agent improves, relabeled goals get harder.
- Robot-arm tasks (push, slide, pick and place): HER clearly beats DDPG and DDPG with count-based exploration, for single or multiple goals.
- **Shaped rewards can hurt exploration.**

## Critique (Denny Britz)

Loved the shaped-reward insight; there's a link to model-based learning (generalizing across goals). Not convinced by the implicit-curriculum claim in general.
