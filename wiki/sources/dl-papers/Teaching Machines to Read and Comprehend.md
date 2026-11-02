---
type: source
title: "Teaching Machines to Read and Comprehend"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.03340"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - reading-comprehension
  - attention
  - dataset
status: ingested
address: c-000298
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[SQuAD - 100,000+ Questions for Machine Comprehension of Text]]"
  - "[[Natural Language Comprehension with the EpiReader]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/teaching-machines-to-read-and-comprehend.md]]"
---

# Teaching Machines to Read and Comprehend

[Paper](http://arxiv.org/abs/1506.03340) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Hermann et al. (DeepMind) build about 1M **cloze-style QA** examples from CNN and Daily Mail article **bullet summaries**: delete an entity and ask the model to fill it from the article. Entities are **anonymized** per document (consistent IDs within a document, shuffled across documents), so models must read rather than use world knowledge.

## Results (accuracy, CNN / Daily Mail)

| Model | CNN | DM |
|-------|-----|----|
| Max-frequency entity | 33.2 | 25.5 |
| Exclusive-frequency entity | 39.3 | 32.8 |
| Frame-semantic | 40.2 | 35.5 |
| Word distance | 50.9 | 55.5 |
| Deep LSTM Reader | 57.0 | 62.2 |
| Uniform Reader | 39.4 | 34.4 |
| **Attentive Reader** | 63.0 | **69.0** |
| **Impatient Reader** | **63.8** | 68.0 |

Documents average 763 tokens (up to 2,000); attention models are clearly better, with nice attention visualizations.

## Critique (Denny Britz)

How does document length affect the Deep LSTM? Is BPTT truncated? The math notation is hard to parse. Restricting outputs to document entities would help. Apply attentive embeddings to classification?
