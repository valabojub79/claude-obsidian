---
type: concept
title: "OP-TEE Crypto Architecture"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - crypto
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000090
related:
  - "[[OP-TEE OS]]"
  - "[[Storage Key Hierarchy]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "optee_os/core/crypto/crypto.c"
  - "optee_os/core/include/crypto/crypto.h"
  - "optee_os/core/include/crypto/crypto_impl.h"
  - "optee_os/core/drivers/crypto/crypto_api/drvcrypt.c"
  - "optee_os/mk/config.mk"
  - "https://optee.readthedocs.io/en/latest/architecture/crypto.html"
---

# OP-TEE Crypto Architecture

How a Trusted Application's `TEE_DigestUpdate()`-style call actually gets executed, and
how OP-TEE swaps in a different crypto backend without touching callers.

## Layering

TA code calls the GlobalPlatform Crypto Operations API (`libutee`). That crosses into
the kernel via syscall (`core/tee/tee_svc_cryp.c`), which validates parameters and
calls into the **internal crypto API** declared in `core/include/crypto/crypto.h`:
functions like `crypto_hash_alloc_ctx()`, `crypto_cipher_init()`, `crypto_mac_update()`
(all verified in `optee_os/core/crypto/crypto.c`).

## The abstraction point

Each of those generic functions dispatches through a small ops-struct interface
defined in `core/include/crypto/crypto_impl.h`: e.g. `struct crypto_hash_ops` with
`init`/`update`/`final`/`free_ctx` function pointers. `crypto_hash_alloc_ctx()`
allocates a context and attaches whichever backend's ops struct implements the
requested algorithm. Everything above this line (syscall layer, TA API) is identical
regardless of which backend actually computes the hash.

## Software backends

Two options, picked at build time via `CFG_CRYPTOLIB_NAME`/`CFG_CRYPTOLIB_DIR`
in `optee_os/mk/config.mk`:
- **LibTomCrypt** (`core/lib/libtomcrypt/`): the default: `CFG_CRYPTOLIB_NAME ?= tomcrypt`.
- **Mbed TLS**: the alternative; also used unconditionally on the TA side for
  big-number/MPI support (`CFG_TA_MBEDTLS_MPI`, forced `y`) regardless of which
  library backs the core-side crypto.

Individual algorithm families can be compiled out (`CFG_CRYPTO_AES=n`, etc.): the
API surface stays the same, disabled algorithms just return
`TEE_ERROR_NOT_IMPLEMENTED` rather than disappearing.

## Hardware accelerators

`core/drivers/crypto/crypto_api/drvcrypt.c` implements a second, driver-facing
registration table (`drvcrypt_register()`, keyed by `enum drvcrypt_algo_id`, gated
per-algorithm-family by `CFG_CRYPTO_DRV_{HASH,CIPHER,MAC,ACIPHER,AUTHENC}`). Vendor
hardware accelerator drivers live under `core/drivers/crypto/<vendor>/`
(e.g. `caam/`, `hisilicon/`, `se050/`, `aspeed/`, `ele/`) and call `drvcrypt_register()`
to plug themselves in as the backend for specific algorithms, ahead of the software
library. There's a separate, narrower acceleration path too:
`CFG_CRYPTO_WITH_CE` (ARMv8 Crypto Extensions) switches `core/arch/arm/crypto/` in
and `core/crypto/`'s plain-C AES implementations out at the instruction level, not
through the `drvcrypt` driver table: on this checkout's `qemu_v8` target (actually
QEMU, so no real CE silicon, but the vexpress platform config sets
`CFG_CRYPTO_WITH_CE ?= y`), confirm whether QEMU's CPU model actually exposes the
ARMv8 crypto instructions before relying on this path meaning anything on real
hardware.

## Why this matters for feature design

(See the `optee-feature-design` Claude Code skill in this checkout's `.claude/skills/`.)

Adding a new hardware crypto accelerator means implementing the `drvcrypt` ops for
the relevant algorithm family under `core/drivers/crypto/<new-vendor>/`, not touching
`core/crypto/crypto.c` or the TA-facing API at all.
