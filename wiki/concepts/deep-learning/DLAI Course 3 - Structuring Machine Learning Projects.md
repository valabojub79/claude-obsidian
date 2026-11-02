---
type: concept
title: "DLAI Course 3 - Structuring Machine Learning Projects"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - dlai-course
  - ml-strategy
complexity: intermediate
domain: deep-learning
status: developing
address: c-000141
related:
  - "[[deeplearning-ai-summary|DeepLearning.ai Summary]]"
  - "[[DLAI Course 2 - Improving Deep Neural Networks]]"
  - "[[DLAI Course 4 - Convolutional Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# DLAI Course 3: Structuring Machine Learning Projects

The shortest course (two weeks), and the one with no math: how to decide **what to try next** when you have a dozen ideas (more data, bigger network, Adam, dropout, L2...) and limited time. Much of it comes from Ng's book draft *Machine Learning Yearning*.

## Course map

| Week | Topic | Wiki pages |
|------|-------|-----------|
| 1 | ML Strategy 1 | [[Orthogonalization]], [[Evaluation Metrics and Dev Sets]], [[Human-Level Performance]] |
| 2 | ML Strategy 2 | [[Error Analysis]], [[Data Mismatch]], [[Transfer Learning]], [[Multi-Task Learning]], [[End-to-End Deep Learning]] |

## Workflow in one picture

1. Set up dev and test sets and a single-number metric ([[Evaluation Metrics and Dev Sets]]).
2. Build a first system **quickly**.
3. Use [[Bias and Variance]] (relative to [[Human-Level Performance]]) and [[Error Analysis]] to choose the next step.
4. Iterate.

## The full error decomposition

| Gap | Name | Fix |
|-----|------|-----|
| Human to train | Avoidable bias | Bigger model, longer or better optimization, architecture search |
| Train to train-dev | Variance | More data, regularization, architecture search |
| Train-dev to dev | Data mismatch | Error analysis, make training data more like dev ([[Data Mismatch]]) |
| Dev to test | Overfitting the dev set | Bigger dev set |
