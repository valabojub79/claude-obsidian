---
type: concept
title: "Transfer Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - transfer-learning
complexity: intermediate
domain: deep-learning
status: developing
address: c-000199
related:
  - "[[Multi-Task Learning]]"
  - "[[Convolutional Neural Networks]]"
  - "[[Fine-Tuning LLMs]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Transfer Learning

Reuse what a network learned on task A (lots of data) for task B (less data). Example: an ImageNet classifier repurposed for radiology images.

## How

1. **Pretrain** on A.
2. Remove the output layer (or last few); add new layer(s) for B with fresh random weights.
3. **Fine-tune**:
   - Small B dataset: freeze the pretrained layers and train only the new ones. You can precompute and cache frozen-layer activations to save time.
   - More B data: unfreeze more layers.
   - Lots of B data: retrain everything, using the pretrained weights as initialization.

## When it makes sense

- A and B share the same input type (images, audio).
- You have much more data for A than B.
- Low-level features from A (edges, phonemes) plausibly help B.

## In computer vision (DLAI Course 4)

Open-source pretrained weights (ImageNet, COCO) are almost always a better start than random initialization, unless you have a very large dataset and compute budget.

## Beyond DLAI

Transfer learning is the basis of modern NLP: pretrain a language model, then fine-tune or prompt it. See [[Fine-Tuning LLMs]] (AI-Notes) and paper notes like [[Semi-Supervised Sequence Learning]] (and ULMFiT in [[deep-learning-reading-list|the reading list]]).
