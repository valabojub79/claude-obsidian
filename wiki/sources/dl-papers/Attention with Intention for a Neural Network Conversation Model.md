---
type: source
title: "Attention with Intention for a Neural Network Conversation Model"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1510.08565"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
  - attention
status: ingested
address: c-000221
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[A Neural Conversational Model]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/attention-with-intention.md]]"
---

# Attention with Intention for a Neural Network Conversation Model

[Paper](http://arxiv.org/abs/1510.08565) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Three RNNs for dialogue. An **encoder** of the user turn (conditioned on the previous decoder state); an **intention** RNN tracking the conversation's goal over turns (state the problem, resolve the issue, acknowledge); an attentive **decoder** conditioned on the intention.

Evaluated on internal helpdesk chats (10k dialogs, 100k turns, 2M tokens): perplexity and a sample conversation.

## Critique (Denny Britz)

A short paper. Perplexity isn't compared to alternatives, and there's no human evaluation (unlike the Neural Conversational Model), so the results are hard to judge.
