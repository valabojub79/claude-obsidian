---
type: entity
title: "Buildroot"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - build-system
  - linux-userspace
status: developing
address: c-000050
related:
  - "[[OP-TEE Build System]]"
  - "[[U-Boot]]"
  - "[[optee_client]]"
sources:
  - "buildroot/ (local checkout: /home/bhaskarv/optee/buildroot)"
---

# Buildroot

Upstream: `github.com/buildroot/buildroot`. Generic embedded-Linux root-filesystem builder; OP-TEE's `build` repo uses it to produce the minimal normal-world userspace for QEMU targets: this is the project where the PATH-with-spaces build failure surfaced (`support/dependencies/dependencies.mk` explicitly refuses to run if `PATH` contains whitespace, which WSL's Windows-PATH import introduces).

## Output

Configured/built under `/home/bhaskarv/optee/out-br/` (via `common.mk`'s `buildroot` target, `O=.../out-br`). Produces `out-br/images/rootfs.cpio.gz`, which `build/qemu_v8.mk` symlinks into `out/bin/` for [[U-Boot]] / Linux to boot. [[optee_client]]'s `tee-supplicant` and the GP Client API library get packaged into this rootfs so normal-world test/example binaries can actually talk to the TEE at runtime.
