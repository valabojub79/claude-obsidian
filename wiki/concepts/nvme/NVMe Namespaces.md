---
type: concept
title: "NVMe Namespaces"
created: 2026-05-22
updated: 2026-05-22
tags:
  - concept
  - storage
  - nvme
  - hardware
complexity: intermediate
domain: storage-systems
status: developing
address: c-000018
related:
  - "[[NVMe]]"
  - "[[NVMe Queue Model]]"
  - "[[NVMe over Fabrics]]"
  - "[[nvme-base-spec-2.3]]"
sources:
  - "[[nvme-base-spec-2.3]]"
---

# NVMe Namespaces

A namespace is the logical unit of NVMe storage — a contiguous block address space (LBA space) that a host accesses via I/O commands. Every read/write command targets exactly one namespace, identified by its Namespace Identifier (NSID).

## Storage Hierarchy

```
NVM Subsystem
└── Domain(s)
    └── Endurance Group(s)        ← physical media pool (NAND packages)
        └── NVM Set(s)            ← partition within Endurance Group
            └── Namespace(s)      ← LBA space presented to host
                └── Reclaim Units ← write placement targets (FDP feature)
```

### Endurance Groups

A pool of physical media with shared wear-leveling counters and endurance budgets. The host can query per-Endurance-Group endurance, available spare capacity, and media errors via the Endurance Group Information log page. Multiple Endurance Groups allow media isolation (e.g., separate write-heavy and read-mostly workloads).

### NVM Sets

A partition within an Endurance Group. Namespaces in the same NVM Set share capacity and may share internal write buffering. NVM Set ID is reported in Identify Namespace data. Useful for QoS isolation — dedicated NVM Sets prevent one workload from affecting another's tail latency.

### Namespace Properties

| Property | Description |
|---|---|
| NSID | 32-bit identifier; 1 to (NN) where NN = max namespaces from Identify Controller |
| NSZE | Total size in logical blocks |
| NCAP | Capacity (used blocks for thin-provisioned namespaces) |
| NUSE | Utilization (allocated logical blocks) |
| LBA Format | Sector size + metadata size; multiple formats supported |
| NGUID | 128-bit globally unique namespace identifier |
| EUI64 | 64-bit IEEE Extended Unique Identifier |
| ANAGRPID | ANA Group ID (for Fabrics asymmetric access reporting) |

### LBA Formats

Each namespace supports one or more LBA formats (up to 64). A format defines:
- **LBADS**: LBA Data Size = 2^LBADS bytes (e.g., 9 = 512B, 12 = 4096B)
- **MS**: Metadata Size (0 = no metadata, or bytes of per-LBA metadata)
- **RP**: Relative Performance (00b = best, 11b = degraded)

The host selects a format via Format NVM command. Current format reported in Identify Namespace (FLBAS field).

## Namespace Attachment

A namespace exists in the subsystem but is only accessible by a controller when **attached**. The Namespace Attachment command (Admin opcode 15h) attaches/detaches namespaces to controllers:

```
Namespace created ──attach──▶ Controller A, Controller B
                  ◀─detach──  (namespace still exists, just not accessible)
```

This enables multi-controller configurations: a namespace can be shared across multiple controllers (for HA/failover) or isolated to a single controller (for exclusive access).

## Namespace Types

| Type | Description |
|---|---|
| NVM | Standard block namespace; NVM Command Set (read/write/trim) |
| Key Value (KV) | Key-value store; KV Command Set |
| Zoned (ZNS) | Zone-based namespace; ZNS Command Set — append-only zones |

The I/O Command Set for a namespace is fixed at creation and reported in the IOCSS field of Identify I/O Command Set data structures.

## Private vs Shared Namespaces

- **Private**: attached to exactly one controller; exclusive access
- **Shared**: attached to multiple controllers; the subsystem arbitrates concurrent access

For shared namespaces across Fabrics controllers, the NVM Subsystem is responsible for coherency. The host may also use Reservation commands to coordinate exclusive access at the application level.

## Namespace Management

Requires the Namespace Management capability (Identify Controller OACS field bit 3).

**Create Namespace** (Namespace Management command, Select=0): host specifies NSZE, NCAP, LBA format, NVM Set ID, Endurance Group ID, command set, security, and gets back a new NSID.

**Delete Namespace** (Select=1): destroys the namespace and returns capacity to the pool.

**Attach/Detach**: Namespace Attachment command (Admin opcode 15h).

Changes take effect immediately and persist across resets.

## Namespace Identifiers

- **NSID 0**: reserved/invalid
- **NSID FFFFFFFFh**: broadcast — command applies to all attached namespaces (e.g., Format NVM, Sanitize)
- **Active namespace list**: returned by Identify with CNS=02h
- **Allocated namespace list**: includes inactive namespaces (CNS=10h)

## Asymmetric Namespace Access (ANA) — Fabrics

In Fabrics deployments with multiple paths to a subsystem, each controller may offer different performance/availability for a given namespace. The ANA log page reports per-namespace access state per controller:

| ANA State | Meaning |
|---|---|
| Optimized | Best path for this namespace on this controller |
| Non-Optimized | Accessible but not optimal (e.g., cross-controller traffic) |
| Inaccessible | Namespace not currently reachable via this controller |
| Persistent Loss | Media failure; namespace permanently inaccessible |
| Change | State is transitioning; re-read ANA log |

Multipath drivers (Linux nvme-multipath, Windows MPIO) use ANA to select the best controller for each namespace.

## Connections

[[NVMe]] covers the full subsystem architecture. [[NVMe Queue Model]] covers how I/O commands are issued. [[NVMe over Fabrics]] covers multi-controller namespace access over networks. Source: [[nvme-base-spec-2.3]] sections 3.2, 3.3, 8.4.
