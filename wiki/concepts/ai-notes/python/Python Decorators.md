---
type: concept
title: "Python Decorators"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - python
complexity: intermediate
domain: programming
status: developing
address: c-000387
related:
  - "[[Python Namespaces and Scope]]"
  - "[[Python Iterators and Generators]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Iterator, Generator and Decorator/Decorators.md]]"
---

# Decorators (Python)

A design pattern to **add behavior to a function (or class) without modifying it**. From [[ai-notes|AI-Notes]] (DataCamp tutorial).

## Why it works: functions are first-class citizens

They can be passed as arguments, returned from functions, assigned to variables, and stored in data structures. A decorator is a function that takes a function and returns a wrapped one; it relies on closures ([[Python Namespaces and Scope]]).

```python
import functools, time

def timed(fn):
    @functools.wraps(fn)              # keep __name__, __doc__ of fn
    def wrapper(*args, **kwargs):
        t = time.perf_counter()
        out = fn(*args, **kwargs)
        print(f"{fn.__name__}: {time.perf_counter() - t:.3f}s")
        return out
    return wrapper

@timed            # same as: train = timed(train)
def train(): ...
```

## Common patterns (the source lists these as practice)

Logging, call counting, **caching** (`functools.lru_cache`), timing, input validation, **retry on exception**, run-once, output transformation, memory measurement.

- **Decorators with arguments**: an extra outer layer, `def retry(n): def deco(fn): ...`.
- **Stacking**: `@a @b def f` means `a(b(f))`, applied bottom-up.
- **Class-based decorators**: a class with `__call__`.
- Method decorators: `@staticmethod`, `@classmethod`, `@property`.
- Pitfalls: losing metadata without `@wraps`; hidden side effects; harder debugging.
