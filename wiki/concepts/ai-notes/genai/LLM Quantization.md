---
type: concept
title: "LLM Quantization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - model-compression
complexity: intermediate
domain: generative-ai
status: developing
address: c-000332
related:
  - "[[Fine-Tuning LLMs]]"
  - "[[Distilling the Knowledge in a Neural Network]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/Finetuning and Quantization/Quantization of LLM.md]]"
---

# LLM Quantization

From [[ai-notes|AI-Notes]] (Krish Naik; Symbl.ai guide).

## Why

Billion-parameter models need lots of RAM and GPU memory for inference. Quantization is what makes **running LLMs locally** feasible.

## What

Model compression that maps parameters (and sometimes activations) from high precision (FP32) to low precision (FP16, INT8, INT4):

```
x_q = round(x / S + Z)        # S = scale, Z = zero point
```

Float-to-float (FP32 to FP16) is easy since the representations are similar; float to 4-bit integer needs careful scale and zero-point choices.

## Two families

| | PTQ (post-training quantization) | QAT (quantization-aware training) |
|-|---------------------------------|------------------------------------|
| When | After training | During a fine-tuning phase |
| How | Quantize the trained weights directly | Insert **fake-quant** nodes that simulate rounding in forward and backward passes, fine-tune, then convert |
| Cost | Cheap | Needs training compute and data |
| Accuracy | More loss | Less loss |

## Trade-offs

- **Pros**: smaller models (cheaper storage, weaker hardware), more scalable deployments, **faster inference** (less memory bandwidth).
- **Cons**: accuracy loss, which grows as bit width shrinks (4-bit, 3-bit...).

## Related

QLoRA combines 4-bit quantization with LoRA fine-tuning ([[Fine-Tuning LLMs]]). Other compression routes: [[Distilling the Knowledge in a Neural Network|distillation]], pruning, [[Sequence-Level Knowledge Distillation]].
