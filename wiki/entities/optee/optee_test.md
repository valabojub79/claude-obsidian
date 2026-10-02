---
type: entity
title: "optee_test"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - trusted-execution
  - testing
status: developing
address: c-000105
related:
  - "[[xtest Test Framework]]"
  - "[[optee_client]]"
  - "[[OP-TEE OS]]"
sources:
  - "optee_test/ (local checkout: /home/bhaskarv/optee/optee_test)"
---

# optee_test

Upstream: `github.com/OP-TEE/optee_test`. The test suite for the whole OP-TEE stack: a normal-world runner (`xtest`) plus a large set of test Trusted Applications it drives through [[optee_client]]'s GP Client API. See [[xtest Test Framework]] for how it's structured and run.

## Directory layout

- `host/xtest/`: the `xtest` binary itself. `xtest_main.c` is the entry point; `adbg/` is OP-TEE's own lightweight test-case/suite framework (ADBG, "assert-debug"); `regression_*.c`, `benchmark_1000.c`, `gp/`, `nist/` hold the actual test cases grouped into named suites.
- `ta/`: dozens of purpose-built test TAs, one per directory (`crypt`, `storage`, `storage2`, `concurrent`, `socket`, `enc_fs`, `large`, `rpc_test`, `tpm_log_test`, `os_test_lib_dl`, `sdp_basic`, `supp_plugin`, etc.): each exists to exercise one specific core feature (concurrency, dynamic shared libraries via [[TA Library Stack]]'s `libdl`, secure storage, RPC to `tee-supplicant`, ...).
- `host/supp_plugin/`: a test supplicant plugin, for exercising `tee-supplicant`'s plugin RPC path.

## Build

Produces the `xtest` binary plus the compiled test TAs, both packaged into the [[Buildroot]] rootfs so they run against a live [[OP-TEE OS]] instance after boot (see [[OP-TEE Boot Flow]]). Getting a new feature's test TA built and packaged correctly is part of what `optee-feature-design` (project skill) should guide.
