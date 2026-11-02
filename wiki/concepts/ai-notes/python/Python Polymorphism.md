---
type: concept
title: "Python Polymorphism"
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
address: c-000393
related:
  - "[[Python Inheritance]]"
  - "[[Python Abstraction]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Object Oriented Programming/Polymorphism.md]]"
---

# Polymorphism (Python)

"Many forms": the same operation name works on different object types, and the method to run is resolved **at runtime** (dynamic dispatch). From [[ai-notes|AI-Notes]].

## Kinds (as the source classifies them)

- **Compile-time (static)**: operator overloading and function overloading.
- **Run-time (dynamic)**: method **overriding**, where the child's method replaces the parent's for child instances.

> [!contradiction] Python has no true function overloading
> Defining two functions with the same name in Python simply **rebinds** the name, so the last definition wins. "Overloading" in Python is done with default and variable arguments (`*args`, `**kwargs`) or `functools.singledispatch`. There is also no compile-time dispatch: Python is dynamically typed. Operator overloading works via dunder methods (`__add__`, `__eq__`, `__lt__`).

## Examples

- `__str__`: `print(obj)` calls each class's own `__str__`, polymorphism through a common protocol.
- Overriding: `Animal.speak()` overridden by `Dog.speak()` and `Cat.speak()`; `Shape.area()` by `Circle` and `Square`.
- Calling the parent's version: `super().speak()` inside the override.
- Preventing overriding: Python can't strictly; use naming conventions, `typing.final` (static checkers only), or `__slots__` and metaclass tricks.
- Duck typing: any object with the right method works, with no shared base class required.

Exercises in the source: shapes and areas, animal sounds, operator-overloaded comparisons, rental-cost polymorphism, an `Employee` salary hierarchy. See [[Python Abstraction]].
