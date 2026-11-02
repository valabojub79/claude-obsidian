---
type: source
title: "WebNav - A New Large-Scale Task for Natural Language Based Sequential Decision Making"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1602.02261"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
  - nlp
  - dataset
status: ingested
address: c-000303
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Deep Reinforcement Learning with a Natural Language Action Space]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/webnav.md]]"
---

# WebNav - A New Large-Scale Task for Natural Language Based Sequential Decision Making

[Paper](http://arxiv.org/abs/1602.02261) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Nogueira and Cho propose a navigation task: starting from a Wikipedia page, follow links to find the page that contains a **query** (a few sentences), under limits on memory, path length and explored nodes. Datasets WikiNav-4 / 8 / 16 (6k / 890k / 12M training examples).

## Key points

- Pages are bags of pretrained word2vec vectors; actions are the outgoing links; the agent may **peek** at neighbor pages.
- Trained on a single correct path; beam search at prediction. NeuAgent-FF (one tanh layer) vs NeuAgent-Rec (LSTM).
- Neural agents usually **beat human volunteers**.

## Critique (Denny Britz)

Peeking is unrealistic (humans use link context). This is text matching, not language understanding: longer queries help, which suggests matching. The claimed advantage of the recurrent agent at high hop counts isn't visible in the data. Training on one path ignores the many valid paths.

## Connections

A forerunner of today's web-browsing LLM agents (WebShop, WebArena).
