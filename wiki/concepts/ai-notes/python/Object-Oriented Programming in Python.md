---
type: concept
title: "Object-Oriented Programming in Python"
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
address: c-000385
related:
  - "[[Python Inheritance]]"
  - "[[Python Polymorphism]]"
  - "[[Python Encapsulation]]"
  - "[[Python Abstraction]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Object Oriented Programming/Introduction to OOP.md]]"
---

# Object-Oriented Programming in Python

From [[ai-notes|AI-Notes]] (CampusX). OOP organizes code around **user-defined types** (classes) alongside primitives, to model real-world entities and keep large codebases manageable.

- **Class**: a user-defined data type (the blueprint). **Object**: an instance of it, which occupies memory.
- **`self`**: reference to the current instance; Python passes it implicitly to methods.
- **`__init__`**: the constructor, which initializes instance attributes.

## Relationships between classes

- **Aggregation ("has-a")**: a `Customer` *has an* `Address`. Pass an `Address` object into `Customer`; no hierarchy. (Composition is the stronger form, where the part's lifetime is owned.)
- **Inheritance ("is-a")**: parent and child; see [[Python Inheritance]].

## The four pillars

[[Python Inheritance]] · [[Python Polymorphism]] · [[Python Encapsulation]] · [[Python Abstraction]]

## Practice and interview list from the source (unanswered there)

Dunder/magic methods, operator overloading, metaclasses, composition vs inheritance, design patterns, SOLID, immutability, `super()`, OOP for data pipelines, ML pipelines and microservices, refactoring procedural code. Exercises: `BankAccount`, a vehicle hierarchy, `Library`, a `Shape` area hierarchy, an inventory system.

scikit-learn itself is an OOP showcase: every estimator implements `fit` / `predict` / `transform` (polymorphism through a shared interface).
