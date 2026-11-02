---
type: concept
title: "Python Abstraction"
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
address: c-000386
related:
  - "[[Python Encapsulation]]"
  - "[[Python Polymorphism]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Object Oriented Programming/Abstraction.md]]"
---

# Abstraction (Python)

Expose **what** an object does and hide **how**. In Python this is done with **abstract base classes** from the `abc` module. From [[ai-notes|AI-Notes]].

```python
from abc import ABC, abstractmethod
class Shape(ABC):
    @abstractmethod
    def area(self): ...
    def describe(self):                 # concrete method: shared default behavior
        return f"{type(self).__name__} with area {self.area()}"
```

- An **abstract class** is a blueprint and **can't be instantiated** (`TypeError`) until a subclass implements every abstract method.
- **Abstract methods** define the **interface** (the contract) subclasses must fulfil.
- Abstract classes can include **concrete methods** with default behavior.
- An abstract class can inherit from another abstract class and add more abstract methods.

| Abstract class | Concrete class |
|---------------|----------------|
| Blueprint; can't be instantiated | Instantiable |
| Declares (maybe partly implements) the interface | Implements everything |

**vs encapsulation**: see [[Python Encapsulation]].

**Exercise from the source**: a library management system with abstract `Book`, `Member` and `Transaction` interfaces (borrow and return).
