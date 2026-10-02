---
type: concept
title: "xtest Test Framework"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - testing
  - adbg
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000108
related:
  - "[[optee_test]]"
  - "[[GlobalPlatform Client API Model]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "optee_test/host/xtest/xtest_main.c"
  - "optee_test/host/xtest/regression_1000.c"
  - "optee_test/host/xtest/adbg/"
---

# xtest Test Framework

How [[optee_test]]'s `xtest` binary is actually structured and run. Traced from source
(`xtest_main.c`, `regression_1000.c`), not from docs.

## ADBG: the test-case framework

`host/xtest/adbg/` implements OP-TEE's own minimal test framework (no external
dependency like GTest). Two macros drive it:

- `ADBG_SUITE_DEFINE(name)` declares a named suite (e.g. `regression`, `benchmark`,
  `gp`, `pkcs11`, `ffa_spmc`): each suite is a `TAILQ` of cases.
- `ADBG_CASE_DEFINE(Suite, TestID, RunFunction, Title)` registers one test case into a
  suite. Example from `regression_1000.c`:
  `ADBG_CASE_DEFINE(regression, 1001, xtest_tee_test_1001, "Core self tests");`
  The test ID (`1001`) is what the `-t`/numeric CLI args select later.

Test case source files are numbered by the ID range they cover: `regression_1000.c`
(core/PTA tests, 1000s), `regression_2000.c`, `regression_4000.c`/`4100.c` (crypto),
`regression_5000.c`, `regression_6000.c`, `regression_8000.c`/`8100.c`. `gp/` holds the
GlobalPlatform-compliance test suite (built only `#ifdef WITH_GP_TESTS`); `nist/` holds
NIST crypto test vectors.

## Running it (`xtest_main.c`)

```
xtest                              run everything in the default suite (regression)
xtest -t regression                run only the regression suite
xtest -t regression 1001 1002      run specific test IDs
xtest -t regression -x 1027 -x 1028   run the suite excluding specific IDs
xtest -l <level>                   set verbosity/level
xtest --stats / --install-ta / --clear-storage / --sha-perf / --aes-perf / --asym-perf
                                    standalone utility modes, not part of any suite
```

Suite selection at build time is conditional: `gp` only exists if `WITH_GP_TESTS` is
set, `pkcs11` only if `CFG_PKCS11_TA`, `ffa_spmc` only if `CFG_SPMC_TESTS`: so not
every build of `xtest` has every suite available; check the specific build's `CFG_*`
flags before assuming a suite exists.

## What a test case actually does

Each `xtest_tee_test_NNNN()` function is normal-world code that uses exactly the
[[GlobalPlatform Client API Model]] (`TEEC_OpenSession`/`TEEC_InvokeCommand`/...) to
drive one of the purpose-built test TAs under `optee_test/ta/`. `regression_1000.c`
alone links against a dozen test-TA headers (`ta_crypt.h`, `ta_os_test.h`,
`ta_concurrent.h`, `pta_attestation.h`, etc.): one test file commonly exercises several
different test TAs.

## Relevance to contributing

Per `optee-feature-design` (project skill): a new driver, PTA, or core feature without
a corresponding `xtest` case (new or extended) is much harder to get merged.
