---
type: source
title: "Deep Reinforcement Learning with a Natural Language Action Space"
source_type: paper
year: 2015
url: "https://arxiv.org/abs/1511.04636"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
  - nlp
status: ingested
address: c-000233
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[WebNav - A New Large-Scale Task for Natural Language Based Sequential Decision Making]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/drl-nlp-action.md]]"
---

# Deep Reinforcement Learning with a Natural Language Action Space

[Paper](https://arxiv.org/abs/1511.04636) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** He et al.'s **DRRN** (Deep Reinforcement Relevance Network) for text games. State text and each candidate action text are embedded by **separate** networks, and the Q-value is their **dot product**. That lets the agent handle action spaces made of free-form sentences. It learns to play the text games *Saving John* and *Machine of Death*. In essence, a different Q-function parameterization.
