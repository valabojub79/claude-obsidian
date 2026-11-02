---
type: source
title: "Adversarial Training Methods for Semi-Supervised Text Classification"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1605.07725"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - adversarial
  - semi-supervised
status: ingested
address: c-000217
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Word Embeddings]]"
  - "[[Regularization]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/adversarial-text-classification.md]]"
---

# Adversarial Training Methods for Semi-Supervised Text Classification

[Paper](https://arxiv.org/abs/1605.07725) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Words are discrete, so apply adversarial perturbations to the **word embeddings** instead. Use adversarial training (AT) on labeled data and virtual adversarial training (VAT) on unlabeled data. Plain LSTMs match or beat the state of the art on several text-classification benchmarks.

## Key points

- **Normalize embeddings**; otherwise the model can make perturbations irrelevant by growing embedding norms.
- **AT:** find the worst-case perturbation `r_adv` within norm `eps` (linear approximation) and add an adversarial loss.
- **VAT:** minimize the KL divergence between predictions on clean and perturbed inputs. Needs no labels.
- AT is a **stronger regularizer than random noise**: it explicitly maximizes the cost.
- Setup: pretrain a 1-layer LSTM language model on all data, then fine-tune a uni- or bidirectional LSTM classifier.
- Results: IMDB (VAT reaches state of the art with a unidirectional LSTM), Amazon, RCV1, Rotten Tomatoes, DBpedia. AT separates "good" from "bad" in embedding space, which the baseline doesn't.

## Critique (Denny Britz)

Inconsistent winners (VAT alone vs AT+VAT; bi-LSTM helps or hurts) with no explanation; some bi-LSTM runs are missing; hyperparameters differ across datasets. Is embedding dropout still needed given AT?
