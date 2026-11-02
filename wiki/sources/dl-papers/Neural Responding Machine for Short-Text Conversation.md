---
type: source
title: "Neural Responding Machine for Short-Text Conversation"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1503.02364"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
  - attention
status: ingested
address: c-000270
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[A Neural Conversational Model]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/neural-responding-machine.md]]"
---

# Neural Responding Machine for Short-Text Conversation

[Paper](http://arxiv.org/abs/1503.02364) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Shang, Lu and Li generate replies to **Weibo** posts (short-text conversation: single post to response, with no dialogue state). Three encoder variants:

- **NRM-glo**: last encoder state.
- **NRM-loc**: attention.
- **NRM-hyb**: both concatenated. Hard to train jointly, so train separately and then fine-tune.

## Key points

- 200k posts, 4M responses; GRUs with 1000 units; 40k vocabulary per side; beam size 10.
- Human evaluation: about **75% of responses are reasonable**, beating retrieval-based and SMT systems.
- Tradeoff: retrieval replies are human-written and grammatical but don't generalize to new inputs.
