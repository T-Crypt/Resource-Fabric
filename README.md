# Aphotic Resource Engine

A distributed resource-awareness engine for Aphotic and beyond.

Aphotic Resource Engine explores a simple idea:

> Compute should understand the resources available to it — locally, across the network, and eventually across infrastructure.

The project begins as the resource engine behind [Aphotic-Hypr](https://github.com/T-Crypt/aphotic-hypr), but is designed as an independent system capable of discovering, modeling, claiming, negotiating, and scheduling heterogeneous resources.

## Vision

Resource awareness evolves through three layers:

### 1. System Aware

Understand resources on a single machine.

- CPU
- Memory
- GPU
- VRAM
- Storage
- Network
- Power
- Processes and workloads

### 2. Network Aware

Discover resources across trusted systems and treat them as part of a shared compute fabric.

- Node discovery
- Capability advertisement
- Resource claims
- Workload placement
- Scheduling
- Priority and policy
- Failure detection
- Resource availability changes

### 3. Globally Aware

Unify desktops, servers, clusters, accelerators, and infrastructure behind a common resource model.

Potential providers include:

- Linux desktops
- Bare-metal servers
- Proxmox
- Kubernetes
- GPU compute nodes
- AI inference systems
- Cloud infrastructure

## Core Model

The engine is built around a small set of primitives:

`Node → Resource → Capability → Claim → Policy → Negotiation → Action → Observation`

Resources belong to providers rather than being assumed to exist on the local machine.

This allows workloads to describe **what they need** instead of **where they must run**.

For example:

`GPU VRAM >= 20 GB`

The engine may determine that the resource exists locally, elsewhere on the network, within a cluster, or is currently unavailable.

## Why?

Modern systems increasingly contain specialized and underutilized compute.

A workstation may contain a powerful GPU. A homelab may have unused CPU and memory. A Kubernetes cluster may have available workers. A GPU server may appear on the network only periodically.

These resources are normally managed as separate systems.

Aphotic Resource Engine investigates what happens when they become part of one resource-aware environment.

## Initial POC

The first milestone is intentionally small:

1. Discover participating Linux nodes.
2. Advertise CPU, RAM, GPU, VRAM, and basic capabilities.
3. Maintain a unified resource inventory.
4. Submit resource claims.
5. Evaluate eligible nodes.
6. Make deterministic and explainable placement decisions.
7. React when resources join, leave, or change state.

No distributed magic.

First make resource awareness reliable.

## Aphotic

[Aphotic-Hypr](https://github.com/T-Crypt/aphotic-hypr) is the project's first consumer and proving ground.

Aphotic adds something particularly valuable to resource scheduling: **desktop intent**.

A GPU being technically available does not necessarily mean it should be consumed by a background workload. Gaming, development, AI inference, battery state, interactive workloads, and user activity can change the effective priority of resources.

The long-term goal is therefore not simply resource utilization.

It is **resource awareness**.

## Status

**Experimental / Proof of Concept**

Architecture and protocols are expected to change significantly while the core resource model is validated.
