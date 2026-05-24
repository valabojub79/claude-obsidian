---
type: concept
title: "NVMe"
created: 2026-05-22
updated: 2026-05-22
tags:
  - concept
  - storage
  - protocol
  - hardware
  - nvme
complexity: intermediate
domain: storage-systems
status: developing
address: c-000016
related:
  - "[[NVMe Queue Model]]"
  - "[[NVMe Namespaces]]"
  - "[[NVMe over Fabrics]]"
  - "[[NVM Express Consortium]]"
  - "[[nvme-base-spec-2.3]]"
sources:
  - "[[nvme-base-spec-2.3]]"
---

# NVMe

NVM Express (NVMe) is an open host-controller interface and storage protocol designed from the ground up for non-volatile memory (flash/NAND, persistent memory, emerging media). It replaces AHCI/SATA as the logical interface for SSDs attached over PCIe, and extends to network-attached storage via [[NVMe over Fabrics]].

Governed by the [[NVM Express Consortium]] (nvmexpress.org). Current base specification: Revision 2.3 (July 31, 2025).

## Why NVMe Replaced SATA/AHCI

AHCI was designed for spinning disks with ~1 ms seek latency and a single command queue of 32 entries. NVMe is built for flash, which has:
- Sub-100 µs access latency
- Massive internal parallelism (many NAND die operating simultaneously)
- No need for seek optimization

NVMe's key architectural differences:

| | AHCI | NVMe |
|---|---|---|
| Queue depth | 1 queue, 32 entries | 65,535 queues, 65,536 entries each |
| Command overhead | ~6 µs | ~2.5 µs |
| Transport | SATA (serial) | PCIe (lanes) |
| Namespace support | Single disk | Multiple namespaces per subsystem |
| Fabrics extension | No | Yes (NVMe-oF) |

## Architecture Overview

An NVMe system consists of a **host** and an **NVM Subsystem** connected over a transport.

### NVM Subsystem

The physical storage device (SSD). Contains:
- **Domains**: administrative isolation boundaries; separate controllers may not cross domain boundaries
- **Endurance Groups**: physical media pools with shared wear-leveling (map to NAND packages)
- **NVM Sets**: partitions within an Endurance Group; each namespace belongs to exactly one NVM Set
- **Namespaces**: logical block address (LBA) spaces presented to hosts; see [[NVMe Namespaces]]
- **Controllers**: the functional interface between host and storage; see Controller Types below

### Controller Types

```
NVMe Controllers
├── I/O Controller       — serves read/write commands on namespaces
├── Administrative       — manages subsystem (namespace create/delete, FW update)
└── Discovery            — NVMe-oF only; directory of available NVM subsystems
```

A single NVM Subsystem may contain multiple controllers. In PCIe deployments one controller per PCIe function is typical. In Fabrics deployments a subsystem may expose hundreds of controllers.

### Queue Model

See [[NVMe Queue Model]] for the full Submission Queue / Completion Queue mechanism.

### Transport Models

**Memory-Based (PCIe):** Host and controller share memory. Commands written to Submission Queues in host memory; controller DMAs completions to host memory Completion Queues. Doorbells are MMIO registers the host writes to notify the controller of new commands.

**Message-Based (Fabrics):** Commands and data travel as messages over TCP, RDMA, or FC. [[NVMe over Fabrics]] defines the connect/disconnect handshake and capsule format.

## Key Registers (PCIe/Memory-Based)

| Register | Offset | Description |
|---|---|---|
| CAP | 00h | Controller Capabilities: max queue size, timeout, arbitration, etc. |
| VS | 08h | Version |
| INTMS/INTMC | 0Ch/10h | Interrupt mask |
| CC | 14h | Controller Configuration: enable bit (EN), I/O command set select |
| CSTS | 1Ch | Controller Status: ready (RDY), fatal status (CFS), shutdown status |
| AQA | 24h | Admin Queue Attributes: Admin SQ/CQ sizes |
| ASQ | 28h | Admin Submission Queue Base Address |
| ACQ | 30h | Admin Completion Queue Base Address |
| PMRCAP/PMRCTL | ... | Persistent Memory Region capability and control |

### Initialization Sequence

1. Host sets AQA, ASQ, ACQ to configure Admin Queue
2. Host sets CC.EN = 1
3. Controller sets CSTS.RDY = 1 when ready (within CAP.TO timeout)
4. Host issues Identify controller command on Admin Queue
5. Host creates I/O Submission and Completion Queues via Admin commands
6. Host issues I/O commands on I/O Queues

## Command Structure

All commands are 64-byte Submission Queue Entries (SQE). All completions are 16-byte Completion Queue Entries (CQE).

**Common Command Format (SQE fields):**
- DW0: Opcode (8b), FUSE (2b), PSDT (2b), CID (16b)
- DW1: Namespace ID (NSID)
- DW2-3: Metadata Pointer (MPTR)
- DW4-7: Data Pointer (PRP1, PRP2 or SGL)
- DW8-15: Command-specific fields

Data is transferred via **PRP** (Physical Region Page — 4K-aligned page list) or **SGL** (Scatter-Gather List — arbitrary segments). PRPs are simpler; SGLs more flexible.

**Completion Queue Entry:**
- DW0: Command-specific result
- DW1: Reserved
- DW2: SQ Head Pointer + SQ Identifier
- DW3: Status Field (Phase Tag, Status Code Type, Status Code) + CID

## Command Sets

### Admin Commands (mandatory subset)
Delete/Create SQ and CQ, Get/Set Features, Identify, Abort, Async Event Request, Firmware Commit/Download, Format NVM, Namespace Management, Sanitize.

### I/O Commands (NVM Command Set)
Flush, Write, Read, Write Uncorrectable, Compare, Write Zeroes, Dataset Management (TRIM), Verify, Copy.

### Fabrics Commands
Connect, Disconnect, Property Get/Set, Authentication Send/Receive.

## Extended Capabilities (Section 8)

Optional features negotiated via Identify:
- **Namespace Management**: dynamic create/delete/attach/detach
- **SR-IOV**: up to 65,535 Virtual Functions per PCIe Physical Function
- **Virtualization Management**: NVM Subsystem Reset, per-VF queue allocation
- **Capacity Management**: thin-provisioning, namespace capacity reporting
- **Autonomous Power State Transitions**: controller self-manages power states
- **Power Loss Notification**: host signals impending power loss via PLN pin
- **Keep Alive**: periodic health-check timer between host and controller
- **Sanitize**: cryptographic erase, block erase, overwrite patterns
- **Security**: TCG Opal, TLS 1.3 for NVMe-TCP, in-band authentication (DH-HMAC-CHAP)
- **Firmware Update**: multi-slot firmware with activation sequence
- **Flexible Data Placement (FDP)**: placement hint directives for write amplification reduction
- **Zoned Namespaces (ZNS)**: append-only zones with zone state machine
- **Predictable Latency Mode**: window-based latency guarantees
- **Track Memory Changes**: host-memory write-tracking by controller

## Arbitration

The controller selects commands from Submission Queues via one of:
- **Round Robin (RR)**: equal service across all I/O queues
- **Weighted Round Robin with Urgent Priority (WRR+UP)**: four priority classes (Urgent, High, Medium, Low) with configurable burst sizes (AB field in Set Features)
- **Vendor-specific**: implementation-defined

Admin Queue always has highest priority and is not subject to WRR arbitration.

## Connections

[[NVMe Queue Model]] covers the SQ/CQ mechanism in depth. [[NVMe Namespaces]] covers the storage hierarchy. [[NVMe over Fabrics]] covers network transport. Spec source: [[nvme-base-spec-2.3]].
