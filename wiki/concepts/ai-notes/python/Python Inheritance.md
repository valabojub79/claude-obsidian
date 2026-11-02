---
type: concept
title: "Python Inheritance"
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
address: c-000390
related:
  - "[[Object-Oriented Programming in Python]]"
  - "[[Python Polymorphism]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Object Oriented Programming/Inheritance.md]]"
---

# Inheritance (Python)

A child (sub) class inherits the attributes and methods of a parent (super) class. It **reuses code** (no rewriting of shared components) and helps **abstract** details. From [[ai-notes|AI-Notes]].

## Instance vs class variables

- **Instance variables** (`self.x`): unique per object.
- **Class (static) variables**: defined in the class body and **shared** by all instances (counters, constants). Access them via the class name (`Cls.count`); access through an instance works for reading, but assigning via an instance creates a shadowing instance attribute.

## Types of inheritance

1. **Single**: one parent, one child.
2. **Multiple**: several parents, one child (`class C(A, B)`).
3. **Multi-level**: grandparent, then parent, then child.
4. **Hierarchical**: one parent, many children (tree-shaped).
5. **Hybrid**: a combination.

## `super()` and the diamond problem

(Unanswered in the source.)

- `super().__init__(...)` calls the next class in the **MRO** (method resolution order), so parent initializers run correctly.
- **Diamond** (`D(B, C)` with both `B` and `C` inheriting from `A`): Python resolves it with **C3 linearization**. `D.__mro__` gives `D, B, C, A, object`, and cooperative `super()` calls make `A` initialize exactly once.

See also [[Python Polymorphism]] (method overriding).
