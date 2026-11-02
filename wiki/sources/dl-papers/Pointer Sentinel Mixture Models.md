---
type: source
title: "Pointer Sentinel Mixture Models"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1609.07843"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - language-modeling
  - attention
status: ingested
address: c-000277
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Pointer Networks]]"
  - "[[Language Models and Sequence Generation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/pointer-sentinel-mixture.md]]"
---

# Pointer Sentinel Mixture Models

[Paper](https://arxiv.org/abs/1609.07843) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Merity et al.'s **Pointer Sentinel-LSTM** mixes a softmax over the vocabulary with a **pointer** over the last `L` words of context:

```
p(y|x) = g * p_vocab(y|x) + (1 - g) * p_ptr(y|x)
```

The gate `g` comes from a learned **sentinel** inside the pointer's attention softmax, so it sees the pointer state, not just the RNN state. That is crucial. The pointer handles rare and recently seen words; the softmax handles everything else. State of the art on PTB.

## WikiText datasets (introduced here)

| | Train tokens | Vocab | OOV |
|-|-------------|-------|-----|
| WikiText-2 | 2M | 33k | 2.6% |
| WikiText-103 | 103M | 267k | 2.4% |

Gains concentrate on **rare words**. WikiText-103 became a standard LM benchmark.
