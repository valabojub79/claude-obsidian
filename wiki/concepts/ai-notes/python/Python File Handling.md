---
type: concept
title: "Python File Handling"
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
address: c-000389
related:
  - "[[Python Serialization]]"
  - "[[Python Iterators and Generators]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Handling/File Handling.md]]"
---

# File Handling (Python)

From [[ai-notes|AI-Notes]] (CampusX).

## Data kinds

- **Text**: a sequence of Unicode characters (`'1'` is U+0031).
- **Binary**: raw bytes (images, audio, video, executables). Open with `'rb'` / `'wb'`.

## Operations and modes

Open, read, write, close. Modes: `r`, `w` (truncates), `a` (**append** without overwriting), `x` (create), plus `b` (binary) and `+` (read and write).

## Context manager

```python
with open("data.txt", "a", encoding="utf-8") as f:
    f.write("line\n")
```

`with` closes the file automatically, even on exceptions, so there are no leaked handles.

## How reads travel

The OS loads file data from disk into RAM through a **buffer** (a temporary area) that batches I/O for efficiency.

## Choosing methods

- `write(str)` for one string; `writelines(iterable)` for many.
- `read()` loads everything (fine for small files); `readline()`, or iterating `for line in f`, streams line by line when RAM is limited ([[Python Iterators and Generators]]). `read(n)` reads chunks.
- `tell()` gives the current position; `seek(offset)` moves it.

## Why not always text?

Text files store only strings, so dicts, custom objects and media lose their structure. Use binary formats plus **serialization** ([[Python Serialization]]).

> [!gap] Source stub
> `Exception Handling.md` is empty. In brief: `try / except SpecificError / else / finally`, raise custom exceptions, and don't swallow bare `except:`.
