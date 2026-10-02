---
type: concept
title: "Secure Storage Architecture"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - storage
complexity: advanced
domain: trusted-execution
status: developing
address: c-000091
related:
  - "[[OP-TEE OS]]"
  - "[[optee_client]]"
  - "[[Storage Key Hierarchy]]"
  - "[[Hash Tree Anti-Rollback]]"
  - "[[Normal World vs Secure World]]"
sources:
  - "optee_os/core/tee/tee_svc_storage.c"
  - "optee_os/core/tee/tee_ree_fs.c"
  - "optee_os/core/tee/tee_rpmb_fs.c"
  - "optee_os/core/tee/tee_fs_rpc.c"
  - "optee_os/mk/config.mk"
  - "https://optee.readthedocs.io/en/latest/architecture/secure_storage.html"
---

# Secure Storage Architecture

OP-TEE implements GlobalPlatform's TEE Internal Core API persistent-object storage
with **two independent, coexistable backends**. Which one(s) are active is a build
config choice, not a runtime one.

## The syscall layer

TA calls to the persistent-object API (`TEE_OpenPersistentObject`, `TEE_WriteObject
Data`, ...) cross into `core/tee/tee_svc_storage.c`'s `syscall_storage_obj_*()`
functions (confirmed: `syscall_storage_obj_open`, `_create`, `_del`, `_rename`,
`_read`, plus the enumeration syscalls). This layer is backend-agnostic: it picks a
backend based on the `storage_id` the TA requested.

## Backend 1: REE FS (`CFG_REE_FS ?= y`: the default)

Implemented in `core/tee/tee_ree_fs.c`. Secure-world data gets encrypted/authenticated
*before* ever crossing into Normal World, then handed to [[optee_client]]'s
`tee-supplicant` via RPC (`core/tee/tee_fs_rpc.c`) to actually be written to Linux's
filesystem, under `/data/tee/` (per-object files named by an internal integer id,
plus a `dirf.db` directory listing). tee-supplicant and the kernel driver never see
plaintext: they're just dumb block storage from OP-TEE's point of view. Content
confidentiality/integrity on top of that raw storage comes from a per-file
[[Hash Tree Anti-Rollback|hash tree]] (`core/tee/fs_htree.c`), keyed per the
[[Storage Key Hierarchy]].

**Rollback protection**: none, by itself (GlobalPlatform "level 0"): Normal World's
filesystem is outside the TEE's trust boundary, so an attacker with Normal World
access could replay an old encrypted file + its htree state. See
`CFG_REE_FS_INTEGRITY_RPMB` below for the fix.

## Backend 2: RPMB FS (`CFG_RPMB_FS ?= n`: opt-in)

Implemented in `core/tee/tee_rpmb_fs.c`. Uses the eMMC's Replay Protected Memory
Block partition directly, via `tee-supplicant` and the kernel's RPMB ioctl. Each
RPMB write increments a monotonic hardware write counter authenticated by the eMMC
controller itself (confirmed in source: `wr_cnt`, with an explicit check that
`write_counter` incremented by exactly 1 per write): this is what makes RPMB
rollback-resistant even against a fully compromised Normal World, unlike REE FS.

## Combining them: `CFG_REE_FS_INTEGRITY_RPMB`

When RPMB hardware exists but you still want REE FS's bulk storage capacity (RPMB
partitions are small), `CFG_REE_FS_INTEGRITY_RPMB` (defaults to whatever
`CFG_RPMB_FS` is set to; `cfg-depends-all` in `mk/config.mk` enforces it can't be `y`
without `CFG_RPMB_FS=y`) lets REE FS store its anti-rollback state in RPMB instead of
in the REE filesystem itself: bulk encrypted data stays in `/data/tee/`, but the
rollback-critical counters get the RPMB write-counter's hardware guarantee.

## Where this sits relative to the rest of OP-TEE

Secure storage is the clearest example of the [[Normal World vs Secure World]] split
actually surfacing in a TA-visible API: every persistent-object call crosses the
world boundary at least once (RPC to tee-supplicant), even though the TA code calling
`TEE_WriteObjectData()` has no idea that's happening.
