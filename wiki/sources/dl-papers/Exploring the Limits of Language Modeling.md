---
type: source
title: "Exploring the Limits of Language Modeling"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1602.02410"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - language-modeling
  - scaling
status: ingested
address: c-000245
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Language Models and Sequence Generation]]"
  - "[[Character-Aware Neural Language Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/exploring-the-limits-of-lm.md]]"
---

# Exploring the Limits of Language Modeling

[Paper](http://arxiv.org/abs/1602.02410) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Jozefowicz et al. (Google Brain) scale LSTM language models on the **One Billion Word** benchmark: single-model perplexity 51.3 to **30.0**, ensemble 41 to **23.7 to 24.2**. They study softmax approximations, character-CNN inputs and outputs, and dropout.

## Key points

- 800k vocabulary. A **char-CNN in place of the input embedding matrix** works as well or better with far fewer parameters. A CNN *softmax* also saves parameters but blurs similar-looking words, which a correction term fixes. A char-LSTM output is clearly worse.
- **Dropout on non-recurrent connections** helps a lot.
- Importance sampling is enough (vs NCE).
- No preprocessing; batches of 128 without resetting LSTM state; Adagrad lr 0.2, clipping 1.0, unrolled 20 steps.
- A small LSTM beats the old state of the art in **2 hours**; the best model trained **3 weeks on 32 K40 GPUs**.

## Connections

An early sign that **scale** wins in language modeling, the thread that leads to GPT. See [[Large Language Models]].
