---
type: concept
title: "NVMe over Fabrics"
created: 2026-05-22
updated: 2026-05-22
tags:
  - concept
  - storage
  - nvme
  - networking
  - distributed-systems
complexity: intermediate
domain: storage-systems
status: developing
address: c-000019
related:
  - "[[NVMe]]"
  - "[[NVMe Queue Model]]"
  - "[[NVMe Namespaces]]"
  - "[[nvme-base-spec-2.3]]"
sources:
  - "[[nvme-base-spec-2.3]]"
---

# NVMe over Fabrics

NVMe over Fabrics (NVMe-oF) extends the [[NVMe]] protocol beyond PCIe to network transports, enabling disaggregated storage architectures where hosts access NVM subsystems over data center fabrics. The NVMe command model and namespace hierarchy remain identical; only the transport binding changes.

## Motivation

PCIe NVMe is point-to-point (one host, one device). NVMe-oF enables:
- **Many-to-one**: multiple hosts sharing a centralized NVM subsystem
- **One-to-many**: one host accessing many disaggregated NVM subsystems
- **HA/failover**: namespace accessible from multiple controllers via multiple network paths
- **Storage pooling**: decouple compute nodes from storage capacity

## Transport Models

The Base Specification defines two transport models:

### Memory-Based Transport (PCIe)
- SQ/CQ reside in host memory; controller DMAs to/from host
- Doorbells are MMIO writes to controller registers
- Metadata can travel as extended LBA data or separate MPTR

### Message-Based Transport (Fabrics)
- Commands travel as **capsules** (messages) over the network
- Each capsule contains the SQE + optionally inline data
- No shared memory required; transport layer provides delivery
- Supported fabrics: **NVMe-TCP**, **NVMe-RDMA** (RoCE v2, iWARP, InfiniBand), **NVMe-FC** (Fibre Channel)

## NVMe-oF Architecture

```
Host                          NVM Subsystem
┌─────────────────┐           ┌──────────────────────────────┐
│  NVMe Driver    │           │  NVMe-oF Target              │
│  ┌───────────┐  │  Capsule  │  ┌──────────┐  ┌──────────┐ │
│  │ SQ/CQ     │──┼──────────▶│  │Controller│  │Controller│ │
│  │ (logical) │  │           │  └────┬─────┘  └──────────┘ │
│  └───────────┘  │           │       │ Namespace 1          │
└─────────────────┘           └───────▼──────────────────────┘
         │                          NVM Sets + Media
    NVMe Transport
   (TCP/RDMA/FC)
```

## Discovery Controller

A lightweight controller type that serves as a directory of NVM subsystems. Hosts query it to discover available NVM subsystems and their transport addresses.

Discovery flow:
1. Host connects to well-known Discovery Controller (port 8009 for TCP)
2. Host issues Get Log Page (Discovery Log page) to retrieve subsystem entries
3. Each entry: NVM subsystem NQN, transport type, address, port, NSID
4. Host connects directly to the target NVM subsystem

Persistent Discovery Controllers (PDC) maintain state across host reconnects. Referral entries chain discovery controllers for large deployments.

## Connect / Disconnect (Fabrics Commands)

**Connect** (Fabrics opcode 01h):
- Establishes a Queue Pair (SQ + CQ) between host and controller
- Parameters: Host NQN, Subsystem NQN, Host ID, Queue ID, Queue Size, keep-alive timer
- Controller returns a Controller ID (CNTLID)
- First Connect must specify QID=0 (Admin Queue); subsequent Connects add I/O queues

**Disconnect** (Fabrics opcode 02h):
- Terminates all queues or a specific queue
- Controller cleans up resources

## NVMe Qualified Names (NQN)

Every host and NVM subsystem has an NQN — a URN-style string uniquely identifying it:
```
nqn.2025-04.io.nvmexpress:uuid:<UUID>       (host or well-known subsystem)
nqn.2014-08.org.nvmexpress:NVMf:uuid:<UUID> (typical subsystem)
nqn.2014-08.org.nvmexpress.discovery        (well-known discovery NQN)
```

## Keep Alive

NVMe-oF connections are kept alive via periodic Keep Alive (Fabrics opcode 06h) commands. If the controller does not receive a Keep Alive within the Keep Alive Timeout (KATO) period:
- Controller aborts all outstanding commands
- Controller terminates all queues for the host
- Connection is considered lost

The host negotiates KATO during Connect. Minimum granularity: 100ms.

## Authentication (NVMe 2.x)

In-band authentication using **DH-HMAC-CHAP**:
- Mutual authentication between host and controller
- Supports SHA-256 and SHA-512 hash
- Diffie-Hellman key agreement for session key establishment
- Enabled per-subsystem; mandatory for secure deployments

**TLS 1.3** (NVMe-TCP only): transport-layer encryption. Negotiated during TCP connection setup before any NVMe traffic. Provides confidentiality and integrity for all capsules.

## Asymmetric Namespace Access (ANA)

In Fabrics deployments, a namespace may be accessible from multiple controllers with varying performance characteristics. See [[NVMe Namespaces]] for ANA states and multipath handling.

## Transport Comparison

| Transport | Latency | Throughput | CPU overhead | Typical use |
|---|---|---|---|---|
| PCIe (local) | ~10 µs | >10 GB/s | Low (MMIO) | Direct-attach SSD |
| NVMe-RDMA | ~20-50 µs | >10 GB/s | Low (kernel bypass) | HPC, financial |
| NVMe-TCP | ~100-500 µs | ~10 GB/s | Higher (kernel TCP) | Cloud storage, cost-sensitive |
| NVMe-FC | ~50-100 µs | ~6 GB/s | Low-medium | Enterprise SAN |

## Connections

[[NVMe]] covers the base protocol. [[NVMe Queue Model]] covers the SQ/CQ model that Fabrics extends. [[NVMe Namespaces]] covers ANA for multi-path access. Source: [[nvme-base-spec-2.3]] sections 2.2, 3.2.2, 6 (Fabrics Commands).
