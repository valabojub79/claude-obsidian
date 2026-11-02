---
type: source
title: "A Neural Conversational Model"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.05869"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
  - sequence-models
status: ingested
address: c-000209
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Sequence to Sequence Models]]"
  - "[[A Diversity-Promoting Objective Function for Neural Conversation Models]]"
  - "[[Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/neural-conversational-model.md]]"
---

# A Neural Conversational Model

[Paper](http://arxiv.org/abs/1506.05869) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Vinyals and Le train a plain **seq2seq chatbot**:

- **IT helpdesk** (33M tokens): 1-layer LSTM with 1024 units, 20k vocabulary, perplexity 8. It can walk users through simple fixes; the whole conversation is fed as context.
- **OpenSubtitles** (1.3B tokens, 62M sentences): 2-layer LSTM with 4096 units, 100k vocabulary. Consecutive lines are treated as different speakers (noisy). **Attention didn't help.**

It beats n-gram models in perplexity and shows some world knowledge and generalization, but has **no consistent personality** ("What do you do?" and "What's your job?" get different answers).

## Critique (Denny Britz)

Attention may not help because contexts are only two sentences. Encode conversation context separately (like paragraph vectors)? We need principled long-context handling (subtitle timestamps, multimodal signals). How do you learn a "personality vector"?
