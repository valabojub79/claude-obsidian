---
type: concept
title: "Word2Vec and Negative Sampling"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - embeddings
complexity: advanced
domain: deep-learning
status: developing
address: c-000205
related:
  - "[[Word Embeddings]]"
  - "[[GloVe]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# Word2Vec and Negative Sampling

Mikolov et al., 2013. If the goal is **embeddings** (not a good language model), simple context-target tasks work remarkably well.

## Context choices (to predict "juice" in "a glass of orange juice to go along with")

- Last 4 words (classic LM).
- 4 words on each side (CBOW).
- Last word only.
- **A nearby word** (skip-gram).

## Skip-gram

Sample a **context** word `c`, then a **target** `t` within about plus or minus 10 words. Predict `t` from `c`:

```
e_c = E o_c
P(t | c) = exp(theta_t . e_c) / sum_j exp(theta_j . e_c)     # softmax over 10k+ words
```

Problem: the denominator sums over the whole vocabulary. Fixes:

- **Hierarchical softmax**: a tree of binary classifiers, `O(log V)`; frequent words near the root.
- **Negative sampling** (below).

Sampling `c`: uniform sampling would be dominated by "the, of, a"; use heuristics that down-weight frequent words.

## Negative sampling

Turn it into binary classification:

| context | word | target |
|---------|------|--------|
| orange | juice | 1 (true neighbor) |
| orange | king | 0 |
| orange | book | 0 |
| orange | the | 0 |
| orange | of | 0 (random, even though it occurs nearby) |

```
P(y = 1 | c, t) = sigmoid(theta_t . e_c)
```

Each step trains only `k + 1` of the 10,000 logistic units. `k` is 5 to 20 for small corpora, 2 to 5 for large ones.

**Choosing negatives:** between uniform and empirical frequency, sample with `P(w) proportional to f(w)^(3/4)`.

## Related

- [[GloVe]], a count-based alternative.
- Paper notes in [[deeplearning-papernotes|Deep Learning Paper Notes]] cover follow-ups (subword, contextual embeddings).
