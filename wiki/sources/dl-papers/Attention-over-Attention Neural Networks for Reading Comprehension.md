---
type: source
title: "Attention-over-Attention Neural Networks for Reading Comprehension"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1607.04423"
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
status: ingested
address: c-000222
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Natural Language Comprehension with the EpiReader]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/att-over-att.md]]"
---

# Attention-over-Attention Neural Networks for Reading Comprehension

[Paper](https://arxiv.org/abs/1607.04423) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** For cloze-style QA (predict one missing word), the AoA reader:

1. Encodes document and query with BiGRUs.
2. Builds a pairwise document-query matching matrix.
3. Computes query-to-document attention.
4. Averages document-to-query attention per query word.
5. Multiplies the two into final document-word scores.
6. Aggregates those scores per vocabulary word.

State of the art on CNN News and CBTest, beating EpiReader and the AS Reader.

## Critique (Denny Britz)

Excellent model visualization; simpler than EpiReader **and** better.
