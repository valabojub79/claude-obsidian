---
type: concept
title: "NVMe Queue Model"
created: 2026-05-22
updated: 2026-05-22
tags:
  - concept
  - storage
  - nvme
  - concurrency
  - hardware
complexity: intermediate
domain: storage-systems
status: developing
address: c-000017
related:
  - "[[NVMe]]"
  - "[[NVMe Namespaces]]"
  - "[[nvme-base-spec-2.3]]"
sources:
  - "[[nvme-base-spec-2.3]]"
---

# NVMe Queue Model

The Submission Queue / Completion Queue (SQ/CQ) pair mechanism is the core of [[NVMe]]'s performance advantage over legacy storage interfaces. It enables massive command parallelism with minimal CPU overhead.

## Fundamentals

Every command exchange uses two circular ring buffers in host memory:

- **Submission Queue (SQ)**: host writes 64-byte command entries; doorbell-notifies the controller
- **Completion Queue (CQ)**: controller writes 16-byte completion entries; MSI/MSI-X interrupts the host

One SQ maps to exactly one CQ. Multiple SQs may share one CQ (fan-in).

```
Host Memory                          Controller
┌─────────────────┐                  ┌────────────────┐
│ Submission Queue│──── doorbell ───▶│  Command Fetch │
│  [SQE][SQE]...  │                  │  + Execute     │
└─────────────────┘                  └───────┬────────┘
                                             │ CQE write
┌─────────────────┐                          ▼
│ Completion Queue│◀──── DMA ─────────────────
│  [CQE][CQE]...  │──── interrupt ──▶ Host ISR
└─────────────────┘
```

## Queue Sizes

- Entries per queue: 2 to 65,536 (must be power of 2 for PCIe; CAP.MQES gives max)
- Number of I/O queues: up to 65,535 SQ + 65,535 CQ pairs
- Admin Queue: exactly 1 SQ + 1 CQ, sizes set via AQA register

In practice, drivers typically create one SQ/CQ pair per CPU core to avoid cross-CPU locking.

## Submission Queue Entry (SQE) — 64 bytes

| DWord | Field | Notes |
|---|---|---|
| 0 | Opcode (7:0), FUSE (9:8), PSDT (15:14), CID (31:16) | CID is host-assigned command identifier |
| 1 | NSID | Namespace ID; FFFFFFFFh = broadcast |
| 2-3 | MPTR | Metadata pointer |
| 4-5 | PRP1 or SGL Segment 1 | Data transfer pointer |
| 6-7 | PRP2 or SGL Segment 2 | Continuation or second segment |
| 8-15 | Command-specific | Opcode-dependent fields |

**FUSE field** enables fused operations: two consecutive commands execute atomically (e.g., Compare + Write). First command has FUSE=01b, second has FUSE=10b.

**PSDT field** selects data transfer mode: PRP (00b), SGL single segment (01b), SGL multiple segments (10b).

## Completion Queue Entry (CQE) — 16 bytes

| DWord | Field |
|---|---|
| 0 | Command-specific result |
| 1 | Reserved |
| 2 | SQ Head Pointer (15:0), SQ Identifier (31:16) |
| 3 | Status (15:1), Phase Tag (0), Command Identifier (31:16) |

**Phase Tag (P):** Alternates 0/1 each queue wrap. Host polls by looking for P != current_phase instead of tracking a head pointer — no shared mutable state needed.

**Status Code Types:** Generic (0h), Command Specific (1h), Media/Data Integrity Error (2h), Path-Related (3h).

## Data Transfer: PRP vs SGL

### Physical Region Pages (PRP)
- Page-aligned (4KB default, configurable via CC.MPS)
- PRP1: first page address; PRP2: second page OR pointer to PRP list for larger transfers
- Simpler but requires contiguous 4KB-aligned host pages

### Scatter-Gather Lists (SGL)
- Arbitrary segments, not page-aligned
- Segment descriptor types: Data Block, Keyed Data Block, Segment, Last Segment, Transport SGL Data Block (for Fabrics)
- Controllers advertise SGL support via Identify; not all controllers support all SGL types

## Doorbell Mechanism (PCIe)

After writing new SQEs into the SQ ring buffer, the host writes the new SQ Tail to the SQ Tail Doorbell register (MMIO). The controller reads this and fetches new commands.

After processing CQEs, the host writes the new CQ Head to the CQ Head Doorbell register, releasing the consumed CQE slots back to the controller.

**Shadow Doorbell Buffer (optional):** An optimization where the controller exposes a host-accessible shadow of the doorbell registers in host memory, allowing doorbells to be updated via non-posted writes (avoiding PCIe posted-write ordering issues at high queue depths).

## Admin Queue

A single mandatory queue pair created during controller initialization:
- Handles controller management: Create/Delete queues, Identify, Get/Set Features, Firmware, Sanitize, etc.
- Not subject to I/O arbitration; always highest priority
- Maximum 4096 entries per queue (CAP.MQES may further limit)
- The first command after CC.EN=1 is issued here

## Queue Creation Flow

```
1. Host issues Create I/O Completion Queue (opcode 05h) on Admin SQ
   → specifies CQ base address, size, interrupt vector, IEN
2. Host issues Create I/O Submission Queue (opcode 01h) on Admin SQ
   → specifies SQ base address, size, queue priority, associated CQ ID
3. Controller completes both commands via Admin CQ
4. I/O queue pair is now ready for commands
```

## Interrupt Modes

- **MSI-X** (preferred): one vector per CQ, hardware delivers to specific CPU
- **MSI**: single or multiple interrupt vectors shared across CQs
- **Polling**: driver polls CQ Phase Tag without interrupts (used by latency-sensitive workloads)

## Outstanding Commands

The host tracks in-flight commands via CID. CID space is per-SQ (16-bit). The controller may execute commands from a single SQ out of order (subject to ordering constraints like fused operations and reservations).

The maximum number of outstanding commands across all I/O queues is bounded by the total queue depth (sum of all SQ sizes). The controller may also report a Command Capsule Supported Size limit.

## Connections

[[NVMe]] covers the full architecture. [[NVMe Namespaces]] covers what commands target. See [[nvme-base-spec-2.3]] sections 3.3-3.5 for register definitions, and section 4 for complete command format tables.
