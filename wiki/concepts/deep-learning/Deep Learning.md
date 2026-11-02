---
type: domain
title: "Deep Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - domain
  - deep-learning
  - machine-learning
status: developing
address: c-000148
related:
  - "[[deeplearning-ai-summary|DeepLearning.ai Summary]]"
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[ai-notes|AI-Notes]]"
  - "[[Large Language Models]]"
sources:
  - ".raw/repos/"
---

# Deep Learning (domain hub)

Entry point to the deep learning and machine learning knowledge base built from four repositories (ingested 2026-11-02).

| Source | What it gives | Pages |
|--------|---------------|-------|
| [[deeplearning-ai-summary\|DeepLearning.ai Summary]] | Andrew Ng's 5-course specialization: the modern practitioner's foundation | 5 course hubs + 45 concepts |
| [[lisa-deep-learning-tutorials\|LISA Deep Learning Tutorials]] | Hands-on Theano tutorials; the pretraining era, energy-based models, segmentation | 15 tutorials + 6 concepts |
| [[deeplearning-papernotes\|Deep Learning Paper Notes]] | 99 critical paper summaries (2014-2017 NLP, RL, vision) + a 627-paper reading list | 99 paper pages |
| [[ai-notes\|AI-Notes]] | Interview-style notes: classical ML, statistics, GenAI/RAG, Python, SQL, DSA, system design | 101 pages + merges |

## Suggested learning path

1. **Foundations**: [[Logistic Regression]], [[Gradient Descent]], [[Backpropagation]], [[Activation Functions]], [[Deep L-Layer Neural Network]] ([[DLAI Course 1 - Neural Networks and Deep Learning]]).
2. **Making it train**: [[Weight Initialization]], [[Regularization]], [[Dropout]], [[Batch Normalization]], [[Optimization Algorithms]], [[Hyperparameter Tuning]] ([[DLAI Course 2 - Improving Deep Neural Networks]]).
3. **Strategy**: [[Bias and Variance]], [[Error Analysis]], [[Data Mismatch]], [[Transfer Learning]] ([[DLAI Course 3 - Structuring Machine Learning Projects]]).
4. **Vision**: [[Convolutional Neural Networks]], [[Residual Networks]], [[Object Detection]], [[Semantic Segmentation]], [[Face Recognition]] ([[DLAI Course 4 - Convolutional Neural Networks]]).
5. **Sequences and NLP**: [[Recurrent Neural Networks]], [[Long Short-Term Memory]], [[Word Embeddings]], [[Sequence to Sequence Models]], [[Attention Mechanism]] ([[DLAI Course 5 - Sequence Models]]).
6. **Toward LLMs**: [[Transformer Architecture]], [[Large Language Models]], [[Fine-Tuning LLMs]], [[RAG Architecture]].
7. **History and depth**: [[Unsupervised Pretraining]], [[Energy-Based Models]], [[Autoencoders]], [[Generative Adversarial Networks]], plus the paper notes.

## Classical ML and supporting skills (AI-Notes)

- **Algorithms**: [[Linear Regression]], [[Decision Tree]], [[Random Forest]], [[Gradient Boosting]], [[Support Vector Machine]], [[K Nearest Neighbors]], [[Naive Bayes]], [[K-Means Clustering]], [[Principal Component Analysis]].
- **Practice**: [[Feature Scaling]], [[Categorical Encoding]], [[Missing Values]], [[Outliers]], [[Imbalanced Data]], [[Cross Validation]], [[Classification Metrics]].
- **Statistics**: [[Hypothesis Testing]], [[Confidence Interval]], [[Central Limit Theorem]], [[AB Testing]].
- **Engineering**: [[Object-Oriented Programming in Python]], [[SQL Overview]], [[Data Structures and Algorithms]], [[Client-Server Architecture]], [[MLOps Data Management and Versioning]].
- **Curriculum view**: [[AI-Notes Study Roadmap]].

## People and tools

[[Andrew Ng]] · [[Yoshua Bengio]] · [[Denny Britz]] · [[Theano]] · [[Deep Learning Frameworks]]

## Cross-source threads

- **Attention**: Bahdanau attention (DLAI C5, [[Neural Machine Translation by Jointly Learning to Align and Translate]]), then Luong's variants, then multi-row self-attention, then [[Transformer Architecture]]. AI-Notes' encoder-decoder note retells the same history.
- **Pretraining**: LISA's greedy layer-wise pretraining, then word2vec and GloVe, then [[Semi-Supervised Sequence Learning]] and skip-thoughts, then [[Large Language Models]].
- **Normalization**: [[Input Normalization]], then [[Batch Normalization]], then [[Layer Normalization]] (the Transformer default).
- **Depth**: highway networks, then [[Residual Networks]], then [[Deep Networks with Stochastic Depth]].
