---
type: entity
title: "optee_client"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - trusted-execution
  - client-api
status: developing
address: c-000051
related:
  - "[[OP-TEE OS]]"
  - "[[Normal World vs Secure World]]"
  - "[[Buildroot]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "optee_client/ (local checkout: /home/bhaskarv/optee/optee_client)"
---

# optee_client

Upstream: `github.com/OP-TEE/optee_client`. Normal-world counterpart to [[OP-TEE OS]]: implements the GlobalPlatform **TEE Client API** as a userspace library (`libteec`), plus the `tee-supplicant` daemon.

## Why tee-supplicant exists

Trusted Applications running in secure world sometimes need normal-world services they can't perform themselves: e.g. reading/writing REE filesystem-backed secure storage files, or RPC-ing out to a hardware service. `tee-supplicant` is the normal-world daemon that services those RPCs over the `/dev/tee0`-style kernel driver interface, relaying requests between secure-world TAs and the Linux filesystem/network. Note: the Linux-side kernel driver itself lives in the mainline kernel under `drivers/tee/optee/`, not in this repo.

Packaged into the [[Buildroot]] rootfs so that `optee_examples`/`optee_test` binaries in normal-world Linux can open sessions with TAs.
