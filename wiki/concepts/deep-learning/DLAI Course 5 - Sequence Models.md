---
type: concept
title: "DLAI Course 5 - Sequence Models"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - dlai-course
  - nlp
  - sequence-models
complexity: intermediate
domain: deep-learning
status: developing
address: c-000143
related:
  - "[[deeplearning-ai-summary|DeepLearning.ai Summary]]"
  - "[[DLAI Course 4 - Convolutional Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# DLAI Course 5: Sequence Models

The final course of the specialization ([[deeplearning-ai-summary|DeepLearning.ai Summary]]): models for sequence data such as text, audio, DNA and video frames.

## Course map

| Week | Topic | Wiki pages |
|------|-------|-----------|
| 1 | Recurrent networks | [[Recurrent Neural Networks]], [[Language Models and Sequence Generation]], [[Gated Recurrent Unit]], [[Long Short-Term Memory]] |
| 2 | NLP and word embeddings | [[Word Embeddings]], [[Word2Vec and Negative Sampling]], [[GloVe]] |
| 3 | Seq2seq and attention | [[Sequence to Sequence Models]], [[Beam Search]], [[BLEU Score]], [[Attention Mechanism]], [[Speech Recognition and CTC]] |

## Sequence problem shapes

| Example | Input | Output | Shape |
|---------|-------|--------|-------|
| Speech recognition | audio | text | many-to-many (Tx != Ty) |
| Music generation | nothing or a genre | audio | one-to-many |
| Sentiment classification | text | 1 to 5 stars | many-to-one |
| DNA analysis, NER | sequence | label per position | many-to-many (Tx = Ty) |
| Machine translation | French | English | many-to-many, encoder-decoder |
| Video activity | frames | label | many-to-one |

## Notation

`x<t>` is the t-th element; `x(i)<t>` is that element of example i; `Tx(i)` and `Ty(i)` lengths vary per example. Words are one-hot vectors over a vocabulary (10k to 50k typical, plus `<UNK>` and `<EOS>`), later replaced by [[Word Embeddings]].

## After this course

The 2018 repo predates Transformers. Attention without recurrence ([[Transformer Architecture]]) has since replaced RNNs for most NLP. Later DLAI editions added a Transformers week. See [[Large Language Models]] for the AI-Notes account of that transition.
