---
type: source
title: "OP-TEE License Header Requirements"
source_url: https://optee.readthedocs.io/en/latest/general/license_headers.html
author: "OP-TEE project (Linaro)"
format: documentation
date_ingested: 2026-10-02
created: 2026-10-02
updated: 2026-10-02
tags:
  - source
  - optee
  - trusted-execution
  - licensing
  - documentation
status: ingested
address: c-000045
related:
  - "[[OP-TEE Coding Standards]]"
  - "[[OP-TEE Contribution Workflow]]"
sources:
  - "https://optee.readthedocs.io/en/latest/general/license_headers.html"
---

# OP-TEE License Header Requirements

Canonical license-header page from the official OP-TEE docs. Fetched 2026-10-02.

## New source files

1. Exactly one SPDX identifier, as the first possible line of the file:
   - C source: `// SPDX-License-Identifier: <expr>`
   - C headers / assembly: `/* SPDX-License-Identifier: <expr> */`
   - Python / shell: `# SPDX-License-Identifier: <expr>`
2. At least one copyright line.
3. **Forbidden**: "All rights reserved" wording, and any license text beyond the SPDX identifier itself: SPDX is the sole licensing mechanism for new files.

## Pre-existing / imported files

When pulling in third-party code: add the SPDX tag matching whatever license notice is already there. Removing existing license text (or "All rights reserved") is only allowed with the copyright holder's permission: same rule for both.

## Practical takeaway for review

A patch adding a new file without an SPDX line on line 1, or with extra boilerplate license text / "All rights reserved", fails this standard regardless of what checkpatch says.
