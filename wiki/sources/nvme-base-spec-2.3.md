---
type: source
title: "NVM Express Base Specification, Revision 2.3"
author: "NVM Express, Inc."
date_published: 2025-07-31
date_ingested: 2026-05-22
created: 2026-05-22
updated: 2026-05-22
language: English
format: specification
tags:
  - source
  - storage
  - nvme
  - specification
  - hardware
  - protocol
status: ingested
address: c-000015
related:
  - "[[NVMe]]"
  - "[[NVMe Queue Model]]"
  - "[[NVMe Namespaces]]"
  - "[[NVMe over Fabrics]]"
  - "[[NVM Express Consortium]]"
sources:
  - ".raw/NVM-Express-Base-Specification-Revision-2.3-2025.08.01-Ratified.pdf"
---

# NVM Express Base Specification, Revision 2.3

Ratified July 31, 2025. The authoritative technical specification for the NVMe protocol — the interface standard for connecting non-volatile memory storage to hosts over PCIe and network fabrics. 784 pages. Published by [[NVM Express Consortium]].

## Scope

Defines data structures, registers, command sets, and behavior requirements for NVMe controllers and hosts. Does not define physical layer or transport specifics — those are delegated to transport binding specifications (PCIe, TCP, RDMA, FC). See [[NVMe]] for the conceptual overview.

## Document Structure

| Section | Topic |
|---|---|
| 1 | Scope, conventions, terminology |
| 2 | Theory of Operation — architecture overview |
| 3 | NVMe Architecture — controller types, queues, registers |
| 4 | Data Structures — SQE, CQE, command formats |
| 5 | Admin Command Set |
| 6 | Fabrics Command Set |
| 7 | I/O Commands (NVM Command Set) |
| 8 | Extended Capabilities |
| 9 | Error Handling and Recovery |
| Annex A | Sanitize Operation Considerations |
| Annex B | Host Considerations (informative) |
| Annex C | Power Management (informative) |

## Key Changes in Revision 2.3 (vs 2.2)

- **Flexible Data Placement (FDP)**: expanded data placement controls for write placement into Reclaim Units within Endurance Groups — improves SSD wear leveling and latency for write-heavy workloads.
- **Zoned Namespaces (ZNS)** enhancements: additional zone operations and state transitions.
- **NVMe-MI (Management Interface)**: expanded controller management commands.
- **TLS 1.3 support** for NVMe-TCP authentication and in-band security.
- **Track Memory Changes**: new capability enabling hosts to query regions of host memory that were modified by the controller (DMA write tracking).
- **Predictable Latency Mode (PLM)**: refinements to latency window reporting.
- **Capacity Management**: enhanced namespace capacity reporting.
- **Power Loss Notification (PLN)**: clarifications to PLN flag behavior.
- Various clarifications to SR-IOV virtual function behavior and queue sharing rules.

## Specification Family

This document is the base of a layered family:

```
NVMe Base Specification (this document)
    ├── NVM Command Set Specification (block I/O)
    ├── Key Value Command Set Specification
    ├── Zoned Namespace Command Set Specification
    └── Transport Binding Specifications
            ├── PCIe (ACPI/ECAM register interface)
            ├── NVMe over TCP
            ├── NVMe over RDMA
            └── NVMe over Fibre Channel
```
