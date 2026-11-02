---
type: source
title: "Distilling the Knowledge in a Neural Network"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1503.02531"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - model-compression
  - knowledge-distillation
status: ingested
address: c-000235
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Sequence-Level Knowledge Distillation]]"
  - "[[Transfer Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/distilling-the-knowledge-in-a-nn.md]]"
---

# Distilling the Knowledge in a Neural Network

[Paper](http://arxiv.org/abs/1503.02531) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Hinton, Vinyals and Dean compress an ensemble (or big model) into a small one by training it on the teacher's **soft targets**: softmax with a raised **temperature** `T`. Wrong-class probabilities ("dark knowledge") reveal how the teacher generalizes.

## Key points

- Temperatures of 1 to 10 work, depending on the problem; the original training set suffices (unlabeled data is optional).
- MNIST: a student never shown the digit 3 still learns to recognize it from soft targets (after adjusting the bias).
- With less data, **soft targets beat hard targets** by a wide margin, acting as a regularizer.
- Also proposes ensembles of specialist models for confusable classes.

## Critique (Denny Britz)

The specialist section doesn't fit, since it isn't distilled back into one model.

## Connections

Foundation of model compression and today's LLM distillation (small models trained on large-model outputs). Seq2seq version: [[Sequence-Level Knowledge Distillation]].
