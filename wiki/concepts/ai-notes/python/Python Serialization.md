---
type: concept
title: "Python Serialization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - python
  - io
complexity: beginner
domain: programming
status: developing
address: c-000394
related:
  - "[[Python File Handling]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Handling/Serialization and Deserialization.md]]"
---

# Serialization and Deserialization (Python)

From [[ai-notes|AI-Notes]].

- **Serialization**: convert an object or data structure into a storable or transmittable format, to save state or send it over a network.
- **Deserialization**: rebuild the object from that format.

```python
import json, pickle
json.dump(obj, open("d.json", "w"))          # serialize to text
obj = json.load(open("d.json"))              # deserialize
pickle.dump(model, open("m.pkl", "wb"))      # serialize to binary
model = pickle.load(open("m.pkl", "rb"))
```

| | JSON | Pickle |
|-|------|--------|
| Format | Human-readable text | Binary |
| Types | dict, list, str, number, bool, None | Almost any Python object (classes, models) |
| Portability | Language-neutral | Python-only; can be version-fragile |
| Safety | Safe to load | **Never unpickle untrusted data** (it can execute code) |

ML practice: `joblib` for scikit-learn models; framework formats (`.pt`, SavedModel, safetensors) for neural nets. The LISA tutorials advise pickling **arrays, not compiled functions** for long-term storage ([[LISA Tutorial - Getting Started]]).
