# Aphotic Resource Engine

**A resource-aware compute fabric for systems, networks, and distributed infrastructure.**

Aphotic Resource Engine is an experimental project exploring a simple question:

> What if computing infrastructure understood not only what resources are available, but what work needs to happen, what that work will require, and when and where it should execute?

The project begins as the resource engine behind [Aphotic-Hypr](https://github.com/T-Crypt/aphotic-hypr), but is being developed as an independent system.

The long-term goal is to create a unified resource-awareness layer spanning personal computers, servers, accelerators, homelabs, clusters, and eventually remote infrastructure.

---

## The Idea

Modern computing resources are fragmented.

A desktop may contain a powerful GPU.

A homelab may have hundreds of gigabytes of unused memory and dozens of idle CPU cores.

A Kubernetes cluster may have available workers.

A workstation may disappear from the network during the day and return with 24 GB of available VRAM overnight.

Applications generally understand only the machine or cluster they were designed to operate within.

Aphotic Resource Engine explores a different model:

**Resources belong to a compute fabric. Workloads describe what they need. The fabric determines how, where, and eventually when that work should execute.**

---

# Awareness Model

The project evolves through five levels of awareness.

## L1 — System Awareness

Understand a single system.

Discover and observe:

- CPU
- Memory
- GPU
- VRAM
- Storage
- Network
- Power
- Processes
- Workloads
- Resource contention

The system establishes a real-time model of its available and consumed resources.

---

## L2 — Network Awareness

Connect trusted systems into a shared resource domain.

Nodes advertise their:

- Resources
- Capabilities
- Availability
- Health
- Network characteristics
- Hardware acceleration
- Current workload state

The engine can determine **where resources exist**, rather than assuming all resources are local.

A workstation, server, laptop, or cluster worker becomes a participating compute node.

---

## L3 — Workload Awareness

Understand what computation actually requires.

Instead of simply observing utilization, the engine models workload behavior:

- CPU requirements
- Memory requirements
- GPU requirements
- VRAM requirements
- Storage I/O
- Network I/O
- Runtime
- Interruptibility
- Hardware capabilities
- Data locality

Historical execution data can eventually allow the engine to predict resource requirements before future executions.

---

## L4 — Intent Awareness

Understand what the system or user is trying to accomplish.

Instead of requesting a specific machine, higher-level workloads can describe an objective and constraints.

For example:

    Analyze this repository before 08:00.

That objective may involve:

    Repository
        │
        ├── Index
        ├── Build
        ├── Test
        ├── Static Analysis
        ├── AI Review
        └── Synthesis

Different stages can execute on different resources.

The objective survives even when individual resources disappear.

The goal becomes:

> Schedule outcomes, not machines.

---

## L5 — Predictive Awareness

Understand not only current resource availability, but likely future availability.

Over time, the engine may learn patterns such as:

- GPU availability
- System idle periods
- recurring workloads
- expected workload duration
- expected VRAM consumption
- network conditions
- power availability
- resource contention
- infrastructure cost

A background workload with a morning deadline might wait for a powerful GPU expected to become available overnight rather than immediately consuming slower resources.

The system transitions from reactive scheduling toward **predictive execution planning**.

---

# Core Architecture

The deterministic resource engine remains the authority.

    Observe
       ↓
    Discover
       ↓
    Model
       ↓
    Claim
       ↓
    Policy
       ↓
    Negotiate
       ↓
    Schedule
       ↓
    Execute
       ↓
    Measure
       └──────────► Observe

Core concepts include:

    Node
    Resource
    Capability
    Workload
    Claim
    Policy
    Priority
    Negotiation
    Action
    Observation

Resources are not assumed to belong to the local machine.

Location is an attribute of a resource, not an architectural boundary.

---

# Intelligence Plane

AI is not required for the Resource Engine to operate.

Deterministic scheduling, policy, safety, and resource accounting remain functional independently.

An optional intelligence layer may provide:

- Workload classification
- Resource requirement prediction
- Runtime estimation
- Future availability prediction
- Workload decomposition
- Execution planning
- Anomaly detection
- Policy recommendations
- Natural-language intent interpretation

The intelligence plane advises.

The deterministic engine authorizes.

    Intent
       │
       ▼
    Intelligence
       │
       │ recommendation
       ▼
    Resource Engine
       │
       ▼
    Policy
       │
       ▼
    Execution

Intelligence providers may eventually include:

- Statistical predictors
- Historical heuristics
- Small local models
- Local inference servers
- Frontier models
- Specialized scheduling models
- Custom policy agents

No specific model should be required by the core.

---

# Resource Claims

Workloads describe requirements rather than machines.

Example:

    Required:
      memory >= 32 GB

    Preferred:
      gpu.vram >= 20 GB
      cuda = true
      latency < 10 ms

    Policy:
      priority = background
      interruptible = true
      deadline = 08:00

The engine determines which resources can satisfy the claim.

That may be:

- The local machine
- Another desktop
- A homelab server
- A Kubernetes worker
- A GPU node
- Remote infrastructure

Or no currently available resource at all.

Waiting can itself be a valid scheduling decision.

---

# Dynamic Infrastructure

Resources are expected to appear and disappear.

For example:

    18:00

    RTX 4090 Workstation
    OFFLINE

    Kubernetes Cluster
    CPU: AVAILABLE
    RAM: AVAILABLE

The engine begins CPU-compatible preparation work.

Later:

    23:14

    RTX 4090 Workstation
    ONLINE

    CUDA: AVAILABLE
    VRAM: 23 GB AVAILABLE

The resource topology has changed.

The engine can reevaluate pending work and determine whether GPU-capable stages should now execute.

This allows infrastructure to behave opportunistically rather than remaining statically assigned.

---

# Aphotic

[Aphotic-Hypr](https://github.com/T-Crypt/aphotic-hypr) is the first consumer and proving ground for the Resource Engine.

A desktop provides something traditional infrastructure schedulers often lack:

**human context.**

A technically idle GPU may not actually be available for background computation if the user is about to launch a game.

A development environment may temporarily prioritize compilation.

An AI workload may consume unused VRAM while the machine is idle.

A security workload may require isolated resources.

Aphotic can translate desktop activity into resource intent.

    Human Activity
          ↓
    Computational Intent
          ↓
    Resource Policy
          ↓
    Distributed Execution

This creates a bridge between interactive personal computing and distributed infrastructure.

---

# Initial Proof of Concept

The first implementation is intentionally small.

### Phase 1

- Discover local CPU and memory
- Discover GPU and VRAM
- Model resource capacity
- Observe utilization
- Define resource claims

### Phase 2

- Connect multiple Linux nodes
- Advertise capabilities
- Maintain node health
- Detect node arrival and departure
- Build unified resource inventory
- Evaluate claims across nodes

### Phase 3

- Execute simple remote workloads
- Introduce scheduling policy
- Handle workload failure
- Handle disappearing resources
- Record workload resource history

### Phase 4

- Kubernetes integration
- Workload prediction
- Dynamic scheduling
- Resource negotiation
- Intelligence providers

The first milestone is not autonomous infrastructure.

It is making resource discovery and scheduling **boring, deterministic, observable, and reliable**.

---

# Potential Resource Providers

The architecture should eventually allow providers for:

- Linux
- Aphotic
- Kubernetes
- Proxmox
- Containers
- Bare-metal servers
- NVIDIA GPUs
- AMD GPUs
- Intel GPUs
- AI inference servers
- Cloud compute
- Remote clusters

Providers expose capabilities.

The core engine decides how those capabilities participate in the resource fabric.

---

# Principles

### Deterministic Core

Critical scheduling and safety decisions must not depend on an LLM.

### Explainable Decisions

The engine should be able to explain why a workload was placed, delayed, rejected, migrated, or interrupted.

### Resource Awareness Before Optimization

Understand the environment before attempting to optimize it.

### Heterogeneous by Design

CPU, RAM, GPU, VRAM, storage, network, accelerators, and future resource types should share a common model without pretending they are interchangeable.

### Location Is Not Ownership

A resource does not need to exist on the requesting machine.

### Intelligence Is Optional

AI enhances the engine. It does not define the engine.

### Human Workloads Matter

Interactive computing is a first-class resource constraint, not background noise.

---

# Status

**Experimental / Proof of Concept**

Architecture, protocols, resource models, and APIs are expected to change significantly while the core concepts are validated.

The immediate goal is deliberately smaller than the long-term vision:

> Make a network understand what compute it has.

Then teach it what that compute can do.

Then teach it what work needs to happen.

Eventually, teach it when and where that work should happen.