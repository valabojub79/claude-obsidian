---
type: concept
title: "Beam Search"
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
address: c-000135
related:
  - "[[Sequence to Sequence Models]]"
  - "[[Error Analysis]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# Beam Search

A heuristic search for the most likely output sequence. Keep the `B` best partial sequences (the **beam width**) at each step.

## Algorithm (B = 3)

1. Step 1: keep the top 3 first words, for example {"in", "jane", "september"}.
2. Step 2: for each, score all 10k next words by `P(y1 | x) P(y2 | x, y1)`; keep the best 3 of the 30k pairs.
3. Repeat until `<EOS>`. Only `B` copies of the decoder run at any time.

`B = 1` is greedy search.

## Refinements

- **Log probabilities**: products of many small numbers underflow, so sum logs.
- **Length normalization**: raw scores favor short outputs. Use

  ```
  (1 / Ty^alpha) * sum_t log P(y<t> | x, y<1..t-1>)
  ```

  with `alpha` about 0.7 (0 means none, 1 means full normalization).
- **Choosing B**: production about 10; research up to 100 to 1000. Larger B is better but slower, with diminishing returns. Unlike BFS or DFS it is not exact.

## Error analysis: beam or model?

Human reference `y*`, model output `y_hat`. Compute both under the RNN:

- `P(y* | x) > P(y_hat | x)`: **beam search** failed to find the better sentence. Increase B.
- `P(y* | x) <= P(y_hat | x)`: the **RNN** scores a worse sentence higher. Fix the model (regularization, data, architecture).

Tally over many errors, then work on whichever is responsible for more (see [[Error Analysis]]).
