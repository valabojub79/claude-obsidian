---
type: concept
title: "Client-Server Architecture"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - system-design
  - system-design
  - networking
complexity: beginner
domain: system-design
status: developing
address: c-000396
related:
  - "[[Domain Name System]]"
  - "[[Content Delivery Network]]"
  - "[[Horizontal and Vertical Scaling]]"
  - "[[Database Fundamentals]]"
sources:
  - "[[.raw/repos/AI-Notes/System Design/Client-Server Architecture.md]]"
---

# Client-Server Architecture

Clients (browser, mobile app) send requests; servers process them and respond. From [[ai-notes|AI-Notes]] (RedSwitches blog).

| Tiers | Layout | Example | Trade-off |
|-------|--------|---------|-----------|
| **1-tier** | UI, logic and data on one machine | MP3 player, desktop app | Simple; doesn't share or scale |
| **2-tier** | Client (UI plus logic) and DB server | Older web apps | Fine for small apps; the DB is exposed and the server is overloaded as users grow |
| **3-tier** | Client, **application server** (business logic), DB | Modern web apps | Better security (no direct DB access), thin clients, independent scaling |

## A request's journey (2-tier growth example)

1. The browser asks **DNS** to resolve `www.swiggy.com` to an IP ([[Domain Name System]]).
2. It requests the server at that IP.
3. As traffic grows, static assets move to a **CDN**, which serves cached content near the user ([[Content Delivery Network]]); servers scale out behind load balancers ([[Horizontal and Vertical Scaling]]).

Servers understand IP addresses, query the DBMS, compute, and return data as packets ([[Database Fundamentals]]).
