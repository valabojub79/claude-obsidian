---
type: concept
title: "Content Delivery Network"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - system-design
  - system-design
  - caching
complexity: beginner
domain: system-design
status: developing
address: c-000397
related:
  - "[[Client-Server Architecture]]"
  - "[[Domain Name System]]"
sources:
  - "[[.raw/repos/AI-Notes/System Design/Content Delivery Network (CDN).md]]"
---

# Content Delivery Network (CDN)

A geographically distributed network of **edge servers** that cache and serve (mostly static) content close to users for the lowest latency. It offloads the origin and helps absorb **DDoS** attacks. From [[ai-notes|AI-Notes]] (Cloudflare; Giphy engineering).

## Flow

1. A user requests an asset.
2. The nearest CDN edge checks its cache: on a **hit** it responds immediately.
3. On a **miss** it fetches from the **origin server**, caches the response (per TTL), then serves it.

## Multi-layer caching (origin shield)

A region can have hundreds or thousands of edge servers with **independent caches**. A popular new object can trigger a stampede of misses to the origin. An **origin shield** layer (a mid-tier cache between the edges and the origin) collapses those misses into one origin request.

**Case study**: Giphy serves about **10 billion GIFs a day** via Fastly using this tiered approach.

CDN vs a cache server: a CDN is a large-scale global distribution network; a cache server (Redis or Varnish) is typically local to one app or data center. See [[Client-Server Architecture]].
