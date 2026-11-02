---
type: source
title: "Third-Person Imitation Learning"
source_type: paper
year: 2017
url: "http://openreview.net/forum?id=B16dGcqlx"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - reinforcement-learning
  - imitation-learning
  - gan
status: ingested
address: c-000300
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Deep Q-learning from Demonstrations]]"
  - "[[Generative Adversarial Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/third-person-imitation-learning.md]]"
---

# Third-Person Imitation Learning

[Paper](http://openreview.net/forum?id=B16dGcqlx) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Stadie, Abbeel and Sutskever learn a policy by watching a demonstrator from a **different viewpoint** (third person), unlike standard imitation, which assumes a shared view. Builds on **GAIL** (a discriminator separates teacher from student behavior). Problem: the discriminator would just learn to tell **viewpoints** apart. Fix: add a **domain-confusion** discriminator over the same features, so the features become viewpoint-invariant while still separating expert from novice behavior. Also feed observations from `t+n` (n = 4) to expose dynamics. Works on simple control tasks (point mass, reacher, pendulum).
