---
type: concept
title: "BLEU Score"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - evaluation
complexity: intermediate
domain: deep-learning
status: developing
address: c-000132
related:
  - "[[Sequence to Sequence Models]]"
  - "[[Evaluation Metrics and Dev Sets]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# BLEU Score

**Bil**ingual **E**valuation **U**nderstudy (Papineni et al. 2002). It scores a machine translation by n-gram overlap with one or more human references, giving a single-number metric for problems with many correct answers. It is also used for image captioning.

## Modified (clipped) precision

References: "The cat is on the mat." and "There is a cat on the mat." Output: "the the the the the the the".

- Plain unigram precision: 7/7, which is useless.
- **Clipped**: count each n-gram at most as often as it appears in any single reference: "the" at most 2, giving **2/7**.

Bigrams for "the cat the cat on the mat": counts {the cat 2, cat the 1, cat on 1, on the 1, the mat 1} = 6; clipped {1, 0, 1, 1, 1} = 4, so `p_2 = 4/6`.

```
p_n = sum clipped n-gram counts / sum n-gram counts
```

## Combined score

```
BLEU = BP * exp( (1/4) * sum_{n=1..4} log p_n )
BP   = 1                       if output length > reference length
       exp(1 - ref_len/out_len)  otherwise           # brevity penalty
```

The brevity penalty stops very short outputs from scoring high precision.

Use an open-source implementation (sacreBLEU); scores are not comparable across tokenizations.
