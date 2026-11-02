---
type: source
title: "Sequence-Level Knowledge Distillation"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1606.07947"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - model-compression
  - knowledge-distillation
  - nmt
status: ingested
address: c-000291
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Distilling the Knowledge in a Neural Network]]"
  - "[[Beam Search]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/seq-knowledge-distillation.md]]"
---

# Sequence-Level Knowledge Distillation

[Paper](https://arxiv.org/abs/1606.07947) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Kim and Rush extend [[Distilling the Knowledge in a Neural Network|distillation]] to NMT:

1. **Word-level KD**: match the teacher's per-token distributions (cross-entropy).
2. **Sequence-level KD**: train the student on the teacher's **beam-search outputs**, a sparse mode approximation of the sequence distribution.
3. **Sequence-level interpolation**: train on a teacher-generated sequence that is both high-probability under the teacher and close to the reference.

On WMT'14 and IWSLT'15, large parameter reductions with minor BLEU loss; the methods are complementary.

## Key insights

- Students model only the teacher's **mode**, so **greedy decoding** on a distilled student is about as good as beam search on the teacher.
- **Perplexity does not equal BLEU**: distilled models have much higher perplexity (22.7 vs 8.2) yet **+4.2 BLEU**.
