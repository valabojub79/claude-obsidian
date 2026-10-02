---
type: entity
title: "optee_examples"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - trusted-execution
  - examples
status: developing
address: c-000106
related:
  - "[[Example TA Structure]]"
  - "[[GlobalPlatform Client API Model]]"
  - "[[optee_client]]"
sources:
  - "optee_examples/ (local checkout: /home/bhaskarv/optee/optee_examples)"
---

# optee_examples

Upstream: `github.com/linaro-swg/optee_examples` (pulled in by the [[OP-TEE Build Repo]] manifest). Reference normal-world-app + Trusted-Application pairs, each self-contained under its own directory: `hello_world`, `aes`, `sha`, `random`, `acipher`, `ecdh`, `ecdsa`, `sign_verify`, `hotp`, `secure_storage`, `plugins`.

Every example follows the same two-sided layout: a `host/` normal-world client using [[optee_client]]'s GP Client API, and a `ta/` secure-world Trusted Application implementing the matching GP TEE Internal Core API entry points. See [[Example TA Structure]] for the exact pattern, walked through via `hello_world`, and [[GlobalPlatform Client API Model]] for what the host side is actually calling.

These are the first thing to read before writing a new TA from scratch: find the example closest to what's being built (e.g. `acipher` for asymmetric crypto, `secure_storage` for persistent TA data) and start from its structure rather than `hello_world`'s minimal one.
