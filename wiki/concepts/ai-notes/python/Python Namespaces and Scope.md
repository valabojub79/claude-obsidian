---
type: concept
title: "Python Namespaces and Scope"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - python
complexity: beginner
domain: programming
status: developing
address: c-000392
related:
  - "[[Python Decorators]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Namespace.md]]"
---

# Namespaces and Scope (Python)

From [[ai-notes|AI-Notes]] (CampusX; Python Tutor visualizations).

- **Namespace**: a mapping from names (identifiers) to objects. Keeps names from colliding.
- **Scope**: the region of code where a namespace is directly accessible.

## Four levels: the LEGB rule

Name lookup goes **L**ocal, then **E**nclosing (outer function), then **G**lobal (module), then **B**uilt-in (`len`, `print`). First match wins.

```python
x = "global"
def outer():
    x = "enclosing"
    def inner():
        x = "local"
        print(x)     # local
    inner()
```

## Reading vs writing outer names

- **Reading** an outer name from an inner scope: allowed.
- **Rebinding** it: needs `global x` (module level) or `nonlocal x` (enclosing function). Without it, assignment creates a new local name, and reading it before assignment raises `UnboundLocalError`. Rebinding outer names is discouraged.
- You **can't create** an enclosing-scope name from inside the inner function (`global` can create module-level names, however).

Closures and [[Python Decorators]] rely on enclosing scopes.
