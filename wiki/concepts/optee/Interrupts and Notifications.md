---
type: concept
title: "Interrupts and Notifications"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - interrupts
  - notifications
  - core-internals
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000064
related:
  - "[[Thread Model and RPC]]"
  - "[[Normal World vs Secure World]]"
  - "[[OP-TEE OS]]"
sources:
  - "optee_os/core/kernel/interrupt.c"
  - "optee_os/core/kernel/notif.c"
  - "optee_os/core/drivers/gic.c"
---

# Interrupts and Notifications

Two related but distinct mechanisms inside [[OP-TEE OS]]: handling hardware
interrupts that fire while secure world is running, and notifying normal world of
secure-world events asynchronously. Easy to conflate; source keeps them in separate
files for a reason.

## Interrupts: `core/kernel/interrupt.c` + `core/drivers/gic.c`

Generic interrupt-controller abstraction, with the GIC driver (`drivers/gic.c`) as
the concrete arm implementation. Verified structure:

- `struct itr_chip`: the abstraction for an interrupt controller; a platform's GIC
  driver registers one.
- `interrupt_main_init(chip)`: registers the platform's primary interrupt chip (the
  GIC, on arm platforms) as `itr_main_chip`.
- `interrupt_configure()` / `interrupt_create_handler()`: wire up a specific interrupt
  number (`itr_num`) on a chip to a handler function.
- `interrupt_call_handlers(chip, itr_num)`: the actual dispatch, called from the
  low-level exception vector when an IRQ/FIQ fires while secure world has control.

This is conventional interrupt-controller plumbing: not OP-TEE-specific in concept,
but necessary context before touching any driver that needs an interrupt line (e.g.
a crypto accelerator signaling completion).

## Notifications: `core/kernel/notif.c`

A separate, higher-level mechanism: secure world telling normal world "something
happened" without normal world having to poll. Gated by `CFG_CORE_ASYNC_NOTIF`.

- A `notif_driver` (one per platform/transport) registers itself on
  `notif_driver_head`, a `SLIST` of available notification backends.
- The actual normal-world-visible signal travels as an `OPTEE_RPC_CMD_NOTIFICATION`
  RPC (see [[Thread Model and RPC]]'s RPC command list) rather than as a raw
  interrupt crossing the world boundary directly.
- Under `CFG_NS_VIRTUALIZATION`, notification state is kept per-guest
  (`virt_get_guest_spec_data`) rather than as one global, since multiple normal-world
  guests may each need independent notification delivery.

## Why they're separate

An interrupt is a hardware event secure world's own exception vector sees directly
(e.g. a secure timer, a crypto accelerator's completion line). A notification is
secure world *choosing* to tell normal world something, over the RPC channel, often
*triggered by* having handled an interrupt. Conflating the two would hide the fact
that notification delivery depends on the RPC/thread machinery in
[[Thread Model and RPC]], not just on the interrupt controller.
