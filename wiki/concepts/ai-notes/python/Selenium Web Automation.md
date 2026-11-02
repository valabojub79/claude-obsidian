---
type: concept
title: "Selenium Web Automation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - python
  - automation
  - testing
complexity: beginner
domain: programming
status: developing
address: c-000395
related:
  - "[[Python File Handling]]"
sources:
  - "[[.raw/repos/AI-Notes/Python/Automation/Selenium.md]]"
---

# Selenium Web Automation

From [[ai-notes|AI-Notes]] (`Automation/Selenium.md`, `Automation/Locators.md`; Udemy Selenium course).

## Selenium

Open-source automation for **web applications**: Chrome, Firefox, Edge/IE, Safari on Windows, macOS and Linux, with bindings for Java, C#, Python, JavaScript, PHP and Ruby. Your code talks to a **browser driver** (chromedriver and so on), which drives the browser; browsers don't expose themselves to automation tools directly. `selenium` is the package and `webdriver` the module inside it.

## Locators

How you find elements: id, name, class, tag, link text, **XPath**, **CSS selector**.

| | XPath | CSS selector |
|-|-------|--------------|
| Child step | `/` | space or `>` |
| Indexing | `[2]` | `:nth-child(2)` |
| Can match on | Tags, attributes, **text**, axes (parent, sibling) | Tags, attributes, classes |

Build XPaths from tags when stable attributes are missing.

## Stray notes in the source (system-design snippets)

- Servers understand IP addresses, query the DBMS, compute, and return data as packets (see [[Client-Server Architecture]]).
- CDNs are global content-distribution networks; cache servers are local to an app or network (see [[Content Delivery Network]]).
