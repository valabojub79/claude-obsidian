---
type: source
title: "On Using Very Large Target Vocabulary for Neural Machine Translation"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1412.2007"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - softmax-approximation
status: ingested
address: c-000273
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Neural Machine Translation of Rare Words with Subword Units]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/on-using-very-large-target-vocabulary-for-nmt.md]]"
---

# On Using Very Large Target Vocabulary for Neural Machine Translation

[Paper](http://arxiv.org/abs/1412.2007) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Jean et al. use **importance sampling** to train NMT with a very large target vocabulary. Partition the corpus, and per partition use only the target words that occur in it, so the softmax normalizer is cheap. For decoding, build a **candidate list** per source sentence (frequent words plus dictionary translations from fast_align). Beats smaller-vocabulary baselines.

## Key points

- Base: Bahdanau attention, BiGRU, 1000 hidden, 620-d embeddings, beam 12.
- Training-time and decode-time vocabulary are separate problems.
- Decoding per token: 0.12 s CPU / 0.05 s GPU with candidate lists vs 0.8 / 0.25 s without.
- Reshuffling and repartitioning helps but is expensive.

## Critique (Denny Britz)

Effect of the partitioning strategy? The UNK-replacement model is unexplained, yet gives a bigger gain than the vocabulary increase. Compare under a fixed total time budget, including setup cost. Per-sentence candidate lists are glossed over.
