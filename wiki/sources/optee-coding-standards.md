---
type: source
title: "OP-TEE Coding Standards"
source_url: https://optee.readthedocs.io/en/latest/general/coding_standards.html
author: "OP-TEE project (Linaro)"
format: documentation
date_ingested: 2026-10-02
created: 2026-10-02
updated: 2026-10-02
tags:
  - source
  - optee
  - trusted-execution
  - coding-style
  - documentation
status: ingested
address: c-000044
related:
  - "[[OP-TEE Coding Standards]]"
  - "[[OP-TEE Contribution Workflow]]"
sources:
  - "https://optee.readthedocs.io/en/latest/general/coding_standards.html"
---

# OP-TEE Coding Standards

Canonical coding-standards page from the official OP-TEE docs. Fetched 2026-10-02.

## Baseline

Linux kernel [CodingStyle](https://www.kernel.org/doc/html/latest/process/coding-style.html), enforced by `checkpatch.pl`.

## Exceptions to plain kernel style

- **CamelCase is allowed** for GlobalPlatform API types (e.g. `TEE_Result`, `TEE_UUID`): these come from the GP TEE Internal Core API spec, not OP-TEE's own code.
- **Third-party libraries are exempt** from checkpatch (LibTomCrypt, MPA, newlib, etc.): kept close to upstream so rebasing stays cheap. Locally, the exempt paths are hard-coded in `optee_os/scripts/checkpatch_inc.sh` (`$CHECKPATCH_IGNORE`): `core/lib/lib{fdt,tomcrypt}`, `core/lib/zlib`, `lib/libutils`, `lib/libmbedtls`, `lib/libutee/include/elf*.h`, `core/arch/arm/include/arm{32,64}.h`, various platform headers, `core/lib/qcbor`, etc.
- **Mandatory variable initialization**: "all variables shall be initialized to a well known value," due to past security bugs and unreliable compiler warnings for uninitialized locals.
  - Scalars → `0` unless context implies otherwise.
  - `optee_client` (must stay portable) → `{ 0 }` for structs with a scalar first member, `memset()` otherwise.
  - Everywhere else (GCC/Clang assumed) → `{ }` for structs/arrays; `memset()` only for things like `pthread_t` that may be scalar-or-composite depending on platform.
  - Fixed-width unsigned constants use `U()`/`UL()`/`ULL()` (or `UINT{8,16,32,64}_C()`), never bare suffix-less literals, so sign/width stay unambiguous across 32/64-bit builds.

## Running checkpatch locally

`checkpatch.pl` itself isn't vendored: point `CHECKPATCH` at a copy (Linux kernel tree, or the one in this checkout's `linux/` repo). Then, from `optee_os/`:

- `./scripts/checkpatch.sh`: working tree (default), or `--cached` / `--diff A B` / `<commit>...` / `<range>`: see `scripts/checkpatch.sh --help`.
- `make checkpatch` / `make checkpatch-staging` / `make checkpatch-working`: same checks as Makefile targets.

It uses `optee_os/typedefs.checkpatch` (GlobalPlatform type list, kept sorted reverse-alphabetically) so checkpatch doesn't flag GP CamelCase types as a style violation.
