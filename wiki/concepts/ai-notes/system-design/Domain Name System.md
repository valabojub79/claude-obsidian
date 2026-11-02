---
type: concept
title: "Domain Name System"
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
address: c-000398
related:
  - "[[Client-Server Architecture]]"
  - "[[Content Delivery Network]]"
sources:
  - "[[.raw/repos/AI-Notes/System Design/Domain Name System (DNS).md]]"
---

# Domain Name System (DNS)

The "phonebook of the internet": it maps domain names to IP addresses (and back, via reverse lookups), so people don't need to remember IPs. From [[ai-notes|AI-Notes]] (Technical Guftgu, Cloudflare, Arpit Bhayani).

## Four servers behind a lookup

1. **Recursive resolver** (usually your ISP's, or 8.8.8.8 / 1.1.1.1): does the whole lookup for the client and caches results.
2. **Root name server**: doesn't know IPs; points to the right **TLD** server (`.com`, `.org`, `.in`).
3. **TLD name server**: points to the domain's **authoritative** server.
4. **Authoritative name server**: holds the actual records (A/AAAA for IPs, CNAME, MX, TXT) and returns the IP.

Caching at the browser, OS and resolver (per record **TTL**) means most lookups never reach the root.

DNS also enables **geo-routing and load balancing** (different IPs per region), used by CDNs ([[Content Delivery Network]]). Next step in a request: [[Client-Server Architecture]].
