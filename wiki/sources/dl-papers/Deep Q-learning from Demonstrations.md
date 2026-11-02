---
type: source
title: "Deep Q-learning from Demonstrations"
source_type: paper
year: 2017
url: "https://arxiv.org/abs/1704.03732"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
  - imitation-learning
status: ingested
address: c-000232
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Third-Person Imitation Learning]]"
  - "[[Hindsight Experience Replay]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/dqn-demonstrations.md]]"
---

# Deep Q-learning from Demonstrations

[Paper](https://arxiv.org/abs/1704.03732) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** **DQfD** pretrains a DQN agent on human demonstrations with four losses, then keeps learning online with demonstrations and agent transitions in one prioritized replay buffer.

## Key points

- Most real problems lack simulators but have some human play data (5k to 75k transitions per game here).
- **Losses:** 1-step Q-learning, **n-step** Q-learning, a **large-margin supervised loss** (demonstrations only), L2. All four matter; removing n-step or supervised loss hurts badly.
- Unlike pure imitation learning (capped at demonstrator level), DQfD can **surpass the human**.
- Demonstration data is never evicted, and gets a sampling bonus.
- Strongest on long-horizon games where demonstrations guide exploration.

## Critique (Denny Britz)

A simple, effective bootstrap. But are comparisons fair given the extra data and tuning? No comparison to Rainbow, A3C or Reactor.
