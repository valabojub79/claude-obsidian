---
type: source
title: "Distributed Representations of Sentences and Documents"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1405.4053"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - embeddings
status: ingested
address: c-000236
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Word2Vec and Negative Sampling]]"
  - "[[Document Embedding with Paragraph Vectors]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/distributed-representations-of-sentences-and-documents.md]]"
---

# Distributed Representations of Sentences and Documents

[Paper](http://arxiv.org/abs/1405.4053) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Le and Mikolov's **Paragraph Vector** (doc2vec) learns a fixed-length vector for text of any length by adding a per-paragraph embedding to a word2vec-style model. Two variants:

- **PV-DM** (distributed memory): predict the next word from the paragraph vector plus the preceding words.
- **PV-DBOW** (bag of words): predict words sampled from the paragraph using the paragraph vector alone.

New paragraphs require **inference-time training** of a new vector, which is slow.

## Results

SST binary 12.2% error, fine-grained 51.3%; IMDB 7.42% (a strong result then); internal search retrieval 3.82%.

## Key points

- 400-d vectors; window 5 to 12 (on IMDB the window size changes error by about 0.7%).
- PV-DM alone is good; **concatenating DM and DBOW** is consistently a bit better.
- In PV-DM, **concatenate** rather than average (keeps order). Hierarchical softmax. IMDB training takes about 30 minutes on 16 cores.

## Critique (Denny Britz)

How was the final classifier (LR vs MLP) chosen? How big is the gap? Hierarchical word, sentence and document representations? How does it compare to attention-based RNN autoencoders? (Note: the IMDB number later proved hard to reproduce.)
