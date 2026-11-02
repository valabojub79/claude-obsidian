---
type: concept
title: "Voting Ensembles"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - ensemble
complexity: beginner
domain: machine-learning
status: developing
address: c-000373
related:
  - "[[Ensemble Learning]]"
  - "[[Stacking]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Ensemble Learning/Voting.md]]"
---

# Voting Ensembles

Different algorithms are trained on the **same data**; at prediction time their outputs are aggregated. From [[ai-notes|AI-Notes]].

- **Hard voting** (classification): each model votes for a class; the **majority** wins.
- **Soft voting**: average the predicted **probabilities**; the highest average wins. It uses confidence, so it's usually better when the models are calibrated.

Example (soft): A `[0.7, 0.3]`, B `[0.4, 0.6]`, C `[0.8, 0.2]` average to `[0.63, 0.37]`, so class 1. (Hard voting would also say class 1, 2 votes to 1.)

- **Regression**: average the predictions (optionally weighted).

scikit-learn: `VotingClassifier(voting='hard'|'soft')`, `VotingRegressor`. When the combination should be learned rather than averaged, use [[Stacking]].
