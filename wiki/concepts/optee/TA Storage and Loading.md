---
type: concept
title: "TA Storage and Loading"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - trusted-applications
  - secure-storage
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000079
related:
  - "[[ldelf TA Loader]]"
  - "[[TA Properties and Manifest]]"
  - "[[Secure Boot Chain of Trust]]"
  - "[[optee_client]]"
sources:
  - "https://optee.readthedocs.io/en/latest/architecture/trusted_applications.html"
---

# TA Storage and Loading

Where a user-mode TA's bytes physically come from, *before* [[ldelf TA Loader]] ever
gets to map them. Three different sources, one unified loading path once the bytes
reach secure memory. This page follows the upstream architecture doc; it hasn't been
independently cross-checked against the signature-handling source the way the boot
flow and ldelf pages were: treat the exact crypto details as a starting point, not
gospel, if you're about to implement something security-sensitive here (see
[[Secure Boot Chain of Trust]] for the general caution on that).

## Three sources

| Source | Where it lives | Available from |
|---|---|---|
| **Early TA** | Linked into the core blob itself, a special data section | Boot time, before [[optee_client]]'s `tee-supplicant` or any filesystem is up |
| **REE filesystem TA** | Signed (optionally encrypted) ELF in the untrusted normal-world filesystem, named `<uuid>.ta` | Once `tee-supplicant` is running |
| **Secure storage TA** | Encrypted, indexed by UUID in an encrypted `dirf.db` in the untrusted REE filesystem | Once secure storage is available |

Early TAs exist specifically so a TA can be available before normal-world userspace
(`tee-supplicant`) has started: the `TA_FLAG_DEVICE_ENUM*` flags in
[[TA Properties and Manifest]] control which of these availability points a given TA
is enumerated at.

## Getting REE-filesystem bytes into secure memory

1. [[OP-TEE OS]] RPCs out to `tee-supplicant` (normal world), which allocates
   nonsecure shared memory and populates it with the TA's binary.
2. Core validates the signature against its stored key (RSA,
   `TEE_ALG_RSASSA_PKCS1_V1_5_SHA256` by default, any `TEE_ALG_RSASSA_PKCS1_*`
   variant accepted) and, for bootstrap-format binaries, checks the UUID; if
   `CFG_RPMB_FS=y`, also checks a rollback-protection counter in a `ta_ver.db` file.
3. Validated bytes move from shared (nonsecure) memory into secure memory; the shared
   memory allocation is freed.
4. From here on, loading is identical to an early TA: handed to [[ldelf TA Loader]].

Three on-disk binary formats exist (legacy: signed hash + stripped ELF; bootstrap:
adds a subheader + UUID check; encrypted: AES-GCM or AES-CCM wraps the stripped ELF,
the whole thing RSA-signed): which one a given TA uses depends on how it was signed
at build time, not something to assume without checking the actual `.ta` file's
header.

## Secure storage TAs

Same idea, decrypted first: AES-GCM using the IV/key/tag stored in the encrypted
`dirf.db` entry for that UUID, then the same validate-and-load sequence as a
REE-filesystem TA.

## Why this unification matters

The upstream docs are explicit that this three-way split is invisible past the
loading boundary: *"User mode TAs are loaded into final memory in the same way using
the user mode ELF loader `ldelf`."* If you're adding a new TA storage backend, the
contract to preserve is exactly this: whatever gets the bytes into secure memory,
hand off to the same `ldelf`-based path rather than inventing a parallel loading
mechanism.
