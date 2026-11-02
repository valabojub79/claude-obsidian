---
type: concept
title: "Language Models and Sequence Generation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - sequence-models
complexity: intermediate
domain: deep-learning
status: developing
address: c-000178
related:
  - "[[Recurrent Neural Networks]]"
  - "[[Sequence to Sequence Models]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# Language Models and Sequence Generation

A **language model** assigns a probability to any sequence of words. Speech recognition uses it to pick "pear salad" over "pair salad".

## RNN language model

1. Training set: a large corpus. Tokenize; one-hot over the vocabulary; add `<EOS>`; map rare words to `<UNK>`.
2. Set `x<t> = y<t-1>` (the previous true word, with `x<1> = 0`); at each step predict a softmax over the next word.
3. Loss: `L = - sum_t sum_i y_i<t> log y_hat_i<t>`.

Sentence probability by the chain rule:

```
P(y<1>, y<2>, y<3>) = P(y<1>) P(y<2> | y<1>) P(y<3> | y<1>, y<2>)
```

## Sampling novel sequences

1. Feed `a<0> = 0`, `x<1> = 0`.
2. Sample the first word from the softmax with `np.random.choice` (not argmax).
3. Feed the sample as the next input; repeat until `<EOS>` or a length limit. Optionally reject `<UNK>`.

## Word-level vs character-level

| | Word | Character |
|-|------|-----------|
| Vocabulary | 10k to 1M words | a-z, A-Z, 0-9, punctuation |
| `<UNK>` | needed | never |
| Sequence length | short | much longer |
| Long-range dependencies | better | worse; costlier to train |

In 2018 word-level dominated; character-level was used in special cases. Modern LMs use **subword** tokens (BPE, WordPiece), getting the best of both.

## Related

- Course assignment: dinosaur-name generation and Shakespeare-style poetry (character-level).
- Modern successors: [[Large Language Models]] (in [[ai-notes|AI-Notes]]).
