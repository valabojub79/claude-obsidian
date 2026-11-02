---
type: source
title: "Natural Language Comprehension with the EpiReader"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1606.02270"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - reading-comprehension
status: ingested
address: c-000264
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention-over-Attention Neural Networks for Reading Comprehension]]"
  - "[[Pointer Networks]]"
  - "[[Teaching Machines to Read and Comprehend]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/epireader.md]]"
---

# Natural Language Comprehension with the EpiReader

[Paper](https://arxiv.org/abs/1606.02270) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Two-stage cloze-style QA trained end to end. An **Extractor** (a pointer network) proposes candidate answer words; a **Reasoner** reranks them by estimating textual entailment between the question (with each candidate filled in) and the passage. Beats the Attention Sum Reader and MemNN on CBT and CNN.

## Notes

- In most architectures the right answer is in the top 5 about 95% of the time, so reranking pays.
- Soft attention is a recurring weakness; we need hard attention.
