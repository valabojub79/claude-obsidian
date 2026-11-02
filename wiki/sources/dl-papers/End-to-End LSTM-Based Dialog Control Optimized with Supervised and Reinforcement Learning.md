---
type: source
title: "End-to-End LSTM-Based Dialog Control Optimized with Supervised and Reinforcement Learning"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1606.01269"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
  - reinforcement-learning
status: ingested
address: c-000243
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/e2e-dialog-control-sl-rl.md]]"
---

# End-to-End LSTM-Based Dialog Control Optimized with Supervised and Reinforcement Learning

[Paper](https://arxiv.org/abs/1606.01269) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Williams and Zweig (Hybrid Code Networks precursor). An LSTM picks **action templates**; an entity extractor plus a few hundred lines of Python **business rules** mask invalid actions. Pretrained with supervised learning on just **21 dialogs**, then improved with policy-gradient RL to **70% task completion** on "call a person from the address book".

## Key points

- Hand-crafted input features and templates; the system *selects* responses and doesn't generate text.

## Critique (Denny Britz)

21 dialogs already cover much of this small task space; larger action spaces would be much harder. "I wouldn't call this end-to-end."
