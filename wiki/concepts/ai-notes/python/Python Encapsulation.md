---
type: concept
title: "Python Encapsulation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - python
  - oop
complexity: beginner
domain: programming
status: developing
address: c-000388
related:
  - "[[Python Abstraction]]"
  - "[[Object-Oriented Programming in Python]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Object Oriented Programming/Encapsulation.md]]"
---

# Encapsulation (Python)

Bundle data and the methods that operate on it into one unit, and control access to internal state. From [[ai-notes|AI-Notes]].

- **Strongly encapsulated**: members plus controlled-access mechanisms (getters and setters).
- **Loosely encapsulated**: members exposed without controlled access.

**Abstraction vs encapsulation**: abstraction hides *how* (complexity); encapsulation hides and protects *state* ([[Python Abstraction]]).

## Access levels (by convention)

| Level | Syntax | Meaning |
|-------|--------|---------|
| Public | `name` | Accessible anywhere |
| Protected | `_name` | *Intended* for the class and its subclasses; not enforced |
| Private | `__name` | **Name-mangled** to `_ClassName__name`, which discourages outside access but can still be reached that way |

## Getters and setters

Controlled access to protected and private state, with validation. The Pythonic form is `@property`:

```python
class BankAccount:
    def __init__(self): self.__balance = 0
    @property
    def balance(self): return self.__balance
    def deposit(self, amt):
        if amt <= 0: raise ValueError("positive only")
        self.__balance += amt
```

Practice in the source: `BankAccount` with private balance; `Student` with private grades and an average method.
