---
type: source
title: "Document Embedding with Paragraph Vectors"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1507.07998"
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
address: c-000238
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Distributed Representations of Sentences and Documents]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/document-embedding-with-pv.md]]"
---

# Document Embedding with Paragraph Vectors

[Paper](http://arxiv.org/abs/1507.07998) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Dai, Olah and Le evaluate Paragraph Vectors (PV-DBOW only, for efficiency) on large Wikipedia and arXiv retrieval tasks. PV matches or beats LDA, bag-of-words and averaged word vectors, and supports **vector arithmetic** on documents.

## Results (triplet accuracy with cosine similarity)

| Dataset | PV | LDA |
|---------|----|-----|
| Wikipedia, hand-built | 93% | 82% |
| Wikipedia, distant supervision | 78.8% | 67.7% |
| arXiv | 85% | 85% |

Jointly training word vectors with PV helps; hierarchical softmax with a Huffman tree.

## Critique (Denny Britz)

Why the discrepancy between datasets: BoW is strong on Wikipedia but not arXiv, and LDA the opposite?
