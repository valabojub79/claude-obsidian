---
type: concept
title: "Example TA Structure"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - ta-development
complexity: beginner
domain: trusted-execution
status: developing
address: c-000110
related:
  - "[[optee_examples]]"
  - "[[GlobalPlatform Client API Model]]"
  - "[[TA Library Stack]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "optee_examples/hello_world/host/main.c"
  - "optee_examples/hello_world/ta/hello_world_ta.c"
  - "optee_examples/hello_world/ta/user_ta_header_defines.h"
  - "optee_examples/hello_world/ta/sub.mk"
---

# Example TA Structure

The host/TA split pattern every [[optee_examples]] entry follows, walked through
concretely via `hello_world` (verified against its actual source, not paraphrased from
docs).

## The two sides

```
hello_world/
├── host/main.c                       normal-world client (uses libteec)
└── ta/
    ├── hello_world_ta.c               the TA itself
    ├── include/hello_world_ta.h       shared UUID + command-ID definitions
    ├── user_ta_header_defines.h       required TA property file
    └── sub.mk                         build wiring
```

`hello_world_ta.h` is included by **both** sides: it's how the host and the TA agree on
the UUID and command IDs without duplicating them.

## Host side (`host/main.c`)

Runs exactly the [[GlobalPlatform Client API Model]] sequence:
`TEEC_InitializeContext` → `TEEC_OpenSession` (using `TA_HELLO_WORLD_UUID` from the
shared header) → `TEEC_InvokeCommand(&sess, TA_HELLO_WORLD_CMD_INC_VALUE, &op, ...)` →
`TEEC_CloseSession` → `TEEC_FinalizeContext`.

## TA side (`ta/hello_world_ta.c`)

Four entry points, all matched directly against source:

- `TA_CreateEntryPoint()`: called once when the TA instance is created.
- `TA_OpenSessionEntryPoint(param_types, params, sess_ctx)`: called per session; can
  reject the session or stash per-session state into `*sess_ctx`.
- `TA_InvokeCommandEntryPoint(sess_ctx, cmd_id, param_types, params)`: called per
  `TEEC_InvokeCommand`; dispatches on `cmd_id` (here, `TA_HELLO_WORLD_CMD_INC_VALUE`).
- `TA_CloseSessionEntryPoint(sess_ctx)` / `TA_DestroyEntryPoint()`: teardown, mirroring
  the create/open pair.

## The required property file (`user_ta_header_defines.h`)

Every TA needs one of these (comment in the file itself: *"The name of this file must
not be modified"*). Defines, at minimum:

- `TA_UUID`: set to the shared UUID from the TA's own header.
- `TA_FLAGS`: TA properties (e.g. multi-instance vs single-instance).
- `TA_STACK_SIZE`, `TA_DATA_SIZE`: provisioned stack and heap size.
- `TA_VERSION`: the `gpd.ta.version` property string.

## Build wiring (`ta/sub.mk`)

```makefile
global-incdirs-y += include
srcs-y += hello_world_ta.c
```

The minimum a new TA's `sub.mk` needs: its include dir and its source file(s). This is
the exact pattern `optee-feature-design` (project skill) should point to when wiring a
new TA into the build, and what links against the [[TA Library Stack]] (`libutee` at
minimum) at build time.

## Licensing note

`hello_world_ta.c` and `main.c` both carry a `// SPDX-License-Identifier: BSD-2-Clause`
header, consistent with [[OP-TEE Coding Standards]]'s SPDX rule: worth confirming a new
example/TA follows the same BSD-2-Clause choice (examples use a more permissive license
than OP-TEE core's GPL-2.0, intentionally, since they're meant to be copied as starting
points).
