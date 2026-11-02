---
type: source
title: "Learning Document Embeddings by Predicting N-grams for Sentiment Classification of Long Movie Reviews"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1512.08183"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - embeddings
  - sentiment
status: ingested
address: c-000256
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Distributed Representations of Sentences and Documents]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/learning-document-embeddings-ngrams.md]]"
---

# Learning Document Embeddings by Predicting N-grams for Sentiment Classification of Long Movie Reviews

[Paper](http://arxiv.org/abs/1512.08183) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** **DV-ngram**: like Paragraph Vector, but the document vector **alone** must predict the document's words **and n-grams** (each n-gram treated as a token), trained with negative sampling. It beats n-gram and neural baselines on IMDB.

## Key insight

In standard PV-DM, if neighboring word vectors already predict the next word, the document vector learns nothing. Removing that shortcut forces it to capture document semantics.

## Critique (Denny Britz)

Would word-level dropout achieve the same? The n-gram vocabulary is enormous and sparse, so how does it scale? And it's not really "deep learning", since the network isn't deep.
