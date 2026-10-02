---
type: concept
title: "OP-TEE Coding Standards"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - coding-style
  - contribution
complexity: beginner
domain: trusted-execution
status: developing
address: c-000058
related:
  - "[[optee-coding-standards]]"
  - "[[optee-license-headers]]"
  - "[[OP-TEE Contribution Workflow]]"
sources:
  - "[[optee-coding-standards]]"
  - "[[optee-license-headers]]"
---

# OP-TEE Coding Standards

Practical summary for reviewing/writing patches: full detail in the source pages [[optee-coding-standards]] and [[optee-license-headers]].

## Checklist before opening a PR

- [ ] Runs clean through `checkpatch.pl` (`optee_os/scripts/checkpatch.sh`, or `make checkpatch{,-staging,-working}`): set `CHECKPATCH` to a local `checkpatch.pl` first.
- [ ] Follows Linux kernel style, **except**: CamelCase is fine for GlobalPlatform API types; third-party library dirs (LibTomCrypt, MPA, newlib, `core/lib/qcbor`, etc.: full list in `checkpatch_inc.sh`) are exempt entirely.
- [ ] Every variable initialized to a known value (scalars → `0`; structs → `{ }`, or `{ 0 }`/`memset()` in `optee_client` for portability; fixed-width constants via `U()`/`UL()`/`ULL()`).
- [ ] New files start with exactly one SPDX identifier on line 1 (comment style depends on file type) + at least one copyright line. No "All rights reserved", no extra license boilerplate.
- [ ] Imported/third-party files keep their existing license notice; only remove it with the copyright holder's permission.

## Where this applies

Every repo in the [[OP-TEE Build Repo]] manifest that's OP-TEE's own code: not the vendored third-party pieces inside `optee_os/core/lib/*` or `optee_os/lib/libmbedtls`, which deliberately stay close to upstream.
