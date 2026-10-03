---
type: concept
title: "Storage Key Hierarchy"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - storage
  - crypto
complexity: advanced
domain: trusted-execution
status: developing
address: c-000092
related:
  - "[[Secure Storage Architecture]]"
  - "[[Hash Tree Anti-Rollback]]"
  - "[[OP-TEE Crypto Architecture]]"
  - "[[Secure Boot Chain of Trust]]"
sources:
  - "optee_os/core/tee/tee_fs_key_manager.c"
  - "https://optee.readthedocs.io/en/latest/architecture/secure_storage.html"
---

# Storage Key Hierarchy

Four key tiers, each derived from the one above it, used to encrypt
[[Secure Storage Architecture|secure storage]] files. Verified against
`core/tee/tee_fs_key_manager.c`.

## HUK: Hardware Unique Key

Platform-specific secret burned into (or derived from fuses/OTP in) the SoC, read via
`kernel/tee_common_otp.h`'s platform hook. Never written to disk, never leaves the
chip. This is the root of trust for everything below: it's also what makes storage
device-bound: move the encrypted files to another device and there's no way to
re-derive the keys that protect them.

## SSK: Secure Storage Key

Derived once at boot: `HMAC-SHA256(HUK, chip_id || static_string)`. `tee_fs_
key_manager.c` holds it in a static `struct tee_fs_ssk tee_fs_ssk` (confirmed field
name), initialized by `tee_fs_init_key_manager()` and gated by an `is_init` flag that
`tee_fs_fek_crypt()` checks before using it. One SSK per device, shared across all
TAs.

## TSK: TA Storage Key

Derived per-TA, on demand, **not stored**: recomputed each time it's needed:
`HMAC-SHA256(SSK, TA_UUID)`. Confirmed directly in `tee_fs_fek_crypt()`: it calls
`do_hmac(tsk, ..., tee_fs_ssk.key, ..., uuid, sizeof(*uuid))` inline, then zeroes the
`tsk` buffer (`memzero_explicit`) before returning. This is what gives each TA
storage isolation from every other TA: a TA can't decrypt another TA's files even
though they share the same device-wide SSK, because it doesn't have the other TA's
UUID-derived TSK (and has no legitimate way to ask the kernel to compute one for a
UUID it doesn't own).

## FEK: File Encryption Key

Random, generated per file on creation (`generate_fek()` → `crypto_rng_read()`), then
immediately encrypted under that TA's TSK via `crypto_cipher_init`/`_update`/`_final`
(confirmed: `TEE_FS_KM_ENC_FEK_ALG`) and stored *encrypted* in the file's own
metadata: the plaintext FEK only exists in secure-world memory while a file is open.
This is the key that actually encrypts the file's data blocks.

## Chain, end to end

```
HUK (in silicon, never leaves chip)
 └─ SSK = HMAC-SHA256(HUK, chip_id + static string)      [per device, derived at boot]
     └─ TSK = HMAC-SHA256(SSK, TA_UUID)                   [per TA, derived on demand, never stored]
         └─ FEK = random, encrypted under TSK             [per file, stored encrypted in file metadata]
             └─ actual file content, encrypted under FEK
```

Compromising one file's FEK (e.g. via a bug that leaks it) doesn't expose any other
file: it doesn't even expose the TSK that encrypted it, since that derivation runs
one-way. Compromising the HUK compromises everything, which is precisely why it's
hardware-rooted rather than software-managed.

Note: `core/tee/fs_htree.c` (see [[Hash Tree Anti-Rollback]]) defines its own
similarly-named `TSK`/`SSK`-sized constants scoped to encrypting/authenticating the
hash-tree's own internal nodes: worth confirming in source whether that's the literal
same TSK from this chain or a second, htree-local derivation before assuming they're
identical in a security-sensitive patch.
