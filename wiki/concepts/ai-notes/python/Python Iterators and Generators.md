---
type: concept
title: "Python Iterators and Generators"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - python
complexity: beginner
domain: programming
status: developing
address: c-000391
related:
  - "[[Python Decorators]]"
  - "[[Python File Handling]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Iterator, Generator and Decorator/Iterator.md]]"
---

# Iterators and Generators (Python)

From [[ai-notes|AI-Notes]] (CampusX notebooks).

- **Iteration**: accessing items one after another.
- **Iterable**: an object you can loop over; it has `__iter__` (lists, strings, files).
- **Iterator**: an object that produces the next item on demand; it has **both** `__iter__` and `__next__`. It doesn't load everything into memory, so it suits **large or streaming data**.

Check with `dir(obj)`, or `isinstance(obj, collections.abc.Iterator)`. (The source has a typo calling an `__iter__`-only object an "iterator"; it's an **iterable**.)

- `iter(iterable)` creates an iterator; `iter(iterator)` returns **the same** iterator.
- **How `for` works**: calls `iter()` on the iterable, then repeatedly calls `next()` until `StopIteration`.

## Custom iterators

1. A class with `__iter__` (returning `self`) and `__next__` (returning the next value or raising `StopIteration`).
2. Simpler: a **generator**.

## Generators

(The source page is a link-only stub.) A function using `yield` returns a generator, a lazy iterator that pauses between values:

```python
def read_batches(path, n):
    with open(path) as f:
        batch = []
        for line in f:
            batch.append(line)
            if len(batch) == n:
                yield batch
                batch = []
        if batch:
            yield batch
```

Generator expressions: `(x*x for x in range(10**9))` use constant memory. Common in ML data loaders (Keras generators, PyTorch `IterableDataset`), as in [[Mini-Batch Gradient Descent]].
