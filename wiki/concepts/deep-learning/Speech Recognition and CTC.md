---
type: concept
title: "Speech Recognition and CTC"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - speech
  - sequence-models
complexity: advanced
domain: deep-learning
status: developing
address: c-000196
related:
  - "[[Attention Mechanism]]"
  - "[[End-to-End Deep Learning]]"
  - "[[Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# Speech Recognition and CTC

## Audio preprocessing

A microphone records air-pressure changes over time. Raw waveforms are hard to learn from; the ear works in frequency. Compute a **spectrogram**: slide a window and apply a Fourier transform, giving time against frequency with energy as intensity.

## End-to-end replaces phonemes

Older systems were built on hand-engineered **phonemes**. With big data, [[End-to-End Deep Learning|end-to-end]] models go straight from audio to transcript. Academic datasets have 300 to 3,000 hours; 2018 commercial systems used 100,000+ hours.

Two approaches: an attention-based seq2seq model ([[Attention Mechanism]]), or **CTC**.

## Connectionist Temporal Classification (Graves et al. 2006)

Input is much longer than output (10 s at 100 Hz is 1,000 frames for about 19 characters). Let the RNN (bidirectional in practice) emit one symbol per frame, including a special **blank** `_`:

```
ttt_h_eee___<space>___qqq__   =>   "the q"
```

Rule: **collapse repeated characters not separated by a blank**, then remove blanks. The CTC loss sums over all alignments that collapse to the target. Used in Baidu's DeepSpeech.

## Trigger word detection ("Alexa", "Hey Siri", "Okay Google")

No single agreed-upon algorithm (2018). A simple one:

- Input: spectrogram frames. Output: 1 at the moments just **after** the trigger word ends, 0 elsewhere. An RNN emits per frame.
- The data is very imbalanced (mostly 0s); a hack is to output 1 for a short window of steps after the word.
- Course assignment: synthesize training clips by overlaying "activate" and negative words onto background noise.
