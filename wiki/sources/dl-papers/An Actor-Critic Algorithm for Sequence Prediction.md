---
type: source
title: "An Actor-Critic Algorithm for Sequence Prediction"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1607.07086"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - sequence-models
  - reinforcement-learning
status: ingested
address: c-000219
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Sequence to Sequence Models]]"
  - "[[BLEU Score]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/actor-critic-sequence.md]]"
---

# An Actor-Critic Algorithm for Sequence Prediction

[Paper](http://arxiv.org/abs/1607.07086) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Train seq2seq models with actor-critic RL. An **actor** (policy) generates the sequence; a **critic** estimates Q-values per token. Only the critic sees the ground truth, and the reward is a task score such as BLEU, given partially at each step.

## Key points

- Log-likelihood training conditions on ground truth but decodes on its own guesses, so errors compound (**exposure bias**). AC trains under the model's own outputs.
- Both are bidirectional RNNs; the actor uses soft attention.
- TD-learning analogue, with DQN tricks: a target network for `q_t`, a delayed actor, and a constraint on the critic for large action spaces. Pretrain both to explore the right region.
- Results: spelling correction (gains grow with sequence length) and German-English MT (beats LL and REINFORCE).
- Training BLEU stays below the LL model's, which suggests strong regularization.

## Critique (Denny Britz)

Spelling sequences only go up to length 30, which an LSTM should handle easily. Longer sequences would be more convincing.

## Connections

Related approaches to exposure bias: [[Professor Forcing - A New Algorithm for Training Recurrent Networks]], [[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient]].
