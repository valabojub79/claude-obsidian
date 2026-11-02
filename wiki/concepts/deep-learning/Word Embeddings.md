---
type: concept
title: "Word Embeddings"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - embeddings
complexity: intermediate
domain: deep-learning
status: developing
address: c-000204
related:
  - "[[Word2Vec and Negative Sampling]]"
  - "[[GloVe]]"
  - "[[Transfer Learning]]"
  - "[[Siamese Networks and Triplet Loss]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Text/Word Embeddings.md]]"
---

# Word Embeddings

## From one-hot to dense features

A one-hot vector `o_j` treats every word as unrelated: all inner products are 0 and all distances equal. So "orange juice" teaches nothing about "apple juice". An **embedding** `e_j` (for example 300-d) learns features (gender, royal, food, size...) so similar words sit close together. Visualize with t-SNE, but don't trust the 2-D picture for analogies.

## Transfer learning with embeddings

1. Learn embeddings on 1B to 100B words of unlabeled text (or **download pretrained** ones).
2. Use them for a task with a small labeled set (say 100k words). Unseen words like "durian cultivator" still work because "durian" lies near other fruits.
3. Optionally fine-tune the embeddings if the task data is large.

Biggest gains when task data is small. They also shrink inputs from 10k-d to 300-d.

Analogy to [[Face Recognition]]: "encoding" and "embedding" mean the same thing. The difference is that word embeddings are learned for a fixed vocabulary.

## Analogies and cosine similarity

```
e_man - e_woman  ~  e_king - e_?        =>  ? = queen
sim(u, v) = u . v / (||u|| ||v||)
argmax_w sim(e_w, e_king - e_man + e_woman)
```

## Embedding matrix

`E` has shape `(300, 10000)`; `E @ o_j = e_j`. In practice use a lookup (Keras `Embedding` layer), not a matrix product. `E` is learned like any other weight.

## Learning algorithms

- Neural language model (Bengio 2003): predict the next word from the previous few.
- [[Word2Vec and Negative Sampling]]: skip-gram, CBOW.
- [[GloVe]]: factorize co-occurrence counts.

Advice: try pretrained vectors first; train your own only with lots of data. Embedding axes are generally **not** human-interpretable.

## Application: sentiment classification

- Simple: average the embeddings of a review, then softmax. Order-blind: "Completely lacking in good taste, good service..." looks positive.
- Better: embeddings into a many-to-one **LSTM**. Generalizes to unseen words ("absent of good taste").

## Debiasing (Bolukbasi et al. 2016)

Embeddings absorb societal bias ("man : programmer :: woman : homemaker").

1. **Identify** the bias direction: average `e_he - e_she`, `e_male - e_female`, ...
2. **Neutralize** non-definitional words (doctor, babysitter): project out the bias direction.
3. **Equalize** definitional pairs (grandmother/grandfather) to be equidistant from neutral words.

## Related

Contextual embeddings (ELMo, BERT) superseded static vectors: see [[deeplearning-papernotes|Deep Learning Paper Notes]] and [[Hybrid Search]] (dense retrieval embeddings).

## AI-Notes perspective: frequency-based vs prediction-based

[[ai-notes|AI-Notes]] adds the classic baselines DLAI skips.

### Frequency-based

- **Bag of words**: vocabulary-sized count vector per document (binary BoW records presence only). Sparse and high-dimensional; no semantics; no out-of-vocabulary handling.
- **TF-IDF**: `tf = count / doc length`; `idf = log(N / docs containing the word)`. The inverse down-weights common words; the **log smooths** extremes. With N = 10: a word in 2 docs gets `log 5 = 0.69`, a word in 8 docs `log 1.25 = 0.09` (natural log, rounded). Still little semantics; no OOV.

### Prediction-based

word2vec, FastText, GloVe, ELMo. Dense, low-dimensional, semantic.

- **CBOW**: predict the target from context. Faster; good for huge corpora. **Skip-gram**: predict context from target. Better for rare words. (See [[Word2Vec and Negative Sampling]].)
- **Window size**: small (2 to 3) captures syntax (POS, NER); large (5 to 10) captures topical relations (classification, sentiment).
- **word2vec limits**: no OOV words; words are atomic, so "run" and "running" share nothing. **FastText** (FAIR) fixes both with **character n-gram** subword vectors.

> [!contradiction] Which weights are the embeddings?
> AI-Notes says the hidden-to-output weights form the embedding. In standard word2vec the **input-to-hidden** matrix (one row per word) is used; the output matrix is a second, "context" embedding that is sometimes averaged in (as GloVe does with `e` and `theta`).
