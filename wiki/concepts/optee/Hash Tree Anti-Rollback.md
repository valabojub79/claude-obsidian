---
type: concept
title: "Hash Tree Anti-Rollback"
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
address: c-000093
related:
  - "[[Secure Storage Architecture]]"
  - "[[Storage Key Hierarchy]]"
sources:
  - "optee_os/core/tee/fs_htree.c"
  - "optee_os/core/tee/tee_rpmb_fs.c"
  - "https://optee.readthedocs.io/en/latest/architecture/secure_storage.html"
---

# Hash Tree Anti-Rollback

Two different mechanisms protect [[Secure Storage Architecture|secure storage]]
against a malicious Normal World rewinding files to an old state: one per backend.

## REE FS: the per-file hash tree

`core/tee/fs_htree.c`'s own header comment (confirmed verbatim in source): *"The
hash tree is implemented as a binary tree with the purpose to ensure integrity of the
data in the nodes. The data in the nodes their turn provides both integrity and
confidentiality of the data blocks."* Each node protects its two children plus a data
block; a header node sits at the top protecting the root. Per the upstream
architecture doc, every field (header, nodes, and blocks) is **duplicated as two
versions** (0 and 1) specifically so an update can always leave one fully-consistent
version on disk even though the underlying write to Normal World storage isn't
atomic: if the write to version 1 is interrupted, version 0 is still intact and
readable. Encryption uses AES-GCM per the architecture doc, keyed via the
[[Storage Key Hierarchy]].

**What this does and doesn't protect against**: it detects tampering with or
corruption of a file's own data (any single-file rewrite, truncation, or bit-flip
shows up as an authentication failure on read). It does **not**, by itself, stop an
attacker from reverting the *entire file* (data + its own htree state) back to an
older, validly-signed version they captured earlier: the hash tree proves
"this file is internally consistent," not "this is the newest version of this file."
That's exactly the gap `CFG_REE_FS_INTEGRITY_RPMB` closes, by anchoring the
rollback-critical counter in RPMB instead of trusting Normal World to keep it current.

## RPMB: hardware write-counter rollback protection

`core/tee/tee_rpmb_fs.c` takes a completely different, hardware-anchored approach:
the eMMC RPMB partition has a strictly monotonic write counter maintained *by the
eMMC controller itself*, authenticated via HMAC with a key provisioned once and never
exposed again. Confirmed in source (`struct` fields `wr_cnt`, `wr_cnt_synced`): each
RPMB write is checked to have incremented the counter by exactly 1
(`if (*rawdata->write_counter != wr_cnt + 1)` → treated as an error). Because the
counter lives in tamper-resistant eMMC hardware rather than in a file Normal World
can copy and replay, this protects against rollback even if Normal World (Linux,
tee-supplicant, the bootloader) is fully compromised: which a pure REE FS hash tree
structurally cannot do, no matter how it's built.

## Practical takeaway

If a feature or review touches anything in this area, the question to ask isn't just
"is this encrypted and integrity-checked" (REE FS already gives you that) but
specifically "can this be rolled back by an attacker who controls Normal World": and
the honest answer for pure REE FS is yes, by design, unless RPMB-backed rollback
protection (`CFG_RPMB_FS=y` and/or `CFG_REE_FS_INTEGRITY_RPMB=y`) is also in play. See
[[Secure Boot Chain of Trust]] for the analogous "what does and doesn't get verified"
question on the boot side.
