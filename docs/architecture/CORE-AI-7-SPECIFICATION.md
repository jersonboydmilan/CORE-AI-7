# CORE-AI/7 Canonical Specification

**Status:** Canonical. This document is the authoritative architectural
definition of CORE-AI/7. All other architecture documents, diagrams,
evidence maps, essays, implementation maps, and future research artifacts
must conform to it. Version history:
[ARCHITECTURE-VERSION-MATRIX.md](ARCHITECTURE-VERSION-MATRIX.md).

## Layer model

```
        ┌───────────────────────────────────────────────────────────┐
        │  L7  GOVERNANCE & AUDIT                                    │
        │      policy enforcement · guardrails · decision            │
        │      authorization · audit logging · tamper evidence ·     │
        │      cryptographic signing · audit replay · human review   │
        ├───────────────────────────────────────────────────────────┤
   ▲    │  L6  AGENT COORDINATION                                    │
   │    │      agent identity/capabilities · dependency graphs ·     │
   │    │      communication · trust flow · session isolation ·      │
   │    │      divergence detection                                  │
   │    ├───────────────────────────────────────────────────────────┤
   │    │  L5  ORCHESTRATION                                         │
   d    │      workflow execution · task routing · retry/backoff ·   │
   a    │      circuit breakers · human-in-the-loop checkpoints ·     │
   t    │      failure escalation · recovery coordination            │
   a    ├───────────────────────────────────────────────────────────┤
   │    │  L4  REASONING                                             │
   l    │      local model inference · model interfaces · prompt/    │
   i    │      context construction · context-window management ·    │
   f    │      structured output · output validation                │
   e    ├───────────────────────────────────────────────────────────┤
   c    │  L3  MEMORY & RETRIEVAL                                    │
   y    │      persistent memory · vector storage · retrieval ·       │
   c    │      approximate nearest-neighbor search · context          │
   l    │      assembly · session isolation · freshness · integrity   │
   e    │      metadata · retrieval trust                            │
        ├───────────────────────────────────────────────────────────┤
        │  L2  KNOWLEDGE & DATA                                      │
        │      documents · structured data · knowledge corpus ·       │
        │      ingestion · chunking · embedding generation · index   │
        │      construction · data provenance                        │
        ├───────────────────────────────────────────────────────────┤
        │  L1  COMPUTE & RUNTIME                                     │
        │      physical compute · hardware · OS · runtime            │
        │      environment · local model execution · inference       │
        │      runtime · resource constraints · hardware monitoring   │
        └───────────────────────────────────────────────────────────┘
```

## Layer definitions

### L1 — Compute & Runtime

Scope: physical compute, hardware, operating system, runtime environment,
local model execution, inference runtime, resource constraints, hardware
monitoring. The substrate every layer above ultimately runs on. Local-only
by design — no layer above may depend on a remote compute or inference
service to perform its core function.

### L2 — Knowledge & Data

Scope: documents, structured data, knowledge corpus, ingestion, chunking,
embedding generation, index construction, data provenance. Owns the
contract between raw input and the representations L3/L4 consume, and is
the point where provenance of external material first enters the system.

### L3 — Memory & Retrieval

Scope: persistent memory, vector storage, retrieval, approximate
nearest-neighbor search, context assembly, session isolation, freshness,
integrity metadata, retrieval trust. The primary choke point for context
entering an agent's working set — see the trust-boundary discussion in
[boundaries.md](boundaries.md).

### L4 — Reasoning

Scope: local model inference, model interfaces, prompt/context
construction, context-window management, structured output, output
validation, reasoning execution. Consumes L3 memory as context, not as
ground truth.

### L5 — Orchestration

Scope: workflow execution, task routing, retry logic, backoff, circuit
breakers, human-in-the-loop checkpoints, failure escalation, recovery
coordination. The agent loop and the pipelines that connect reasoning to
memory and to L6 coordination.

### L6 — Agent Coordination

Scope: agent identity, agent capabilities, dependency graphs,
communication, trust flow, session isolation, divergence detection,
multi-agent coordination. Agents exchange typed messages, not raw shared
state, bounding how far one agent's corrupted state can propagate.

### L7 — Governance & Audit

Scope: policy enforcement, guardrails, decision authorization, audit
logging, tamper evidence, cryptographic signing, audit replay, human
review, accountability. Sits structurally above L5/L6: no output reaches
persistent memory or a user without passing through this layer.

## Recovery model

**Recovery is a cross-cutting property of the architecture, not an eighth
layer.** Every layer defines its own recovery behavior; there is no single
"recovery layer" that owns failure handling for the whole system.

| Layer | Recovery concern |
|---|---|
| L1 | Hardware/runtime recovery — process restart, resource-exhaustion handling |
| L2 | Ingestion/index recovery — resuming or re-running interrupted ingestion and index builds |
| L3 | Memory/index recovery — durable-write recovery, crash-safe index rebuild |
| L4 | Inference failure recovery — handling a failed or malformed model response |
| L5 | Workflow retry and escalation — retry/backoff, circuit breaking, escalation to a human checkpoint |
| L6 | Agent cascade cancellation and isolation — containing a failed agent's blast radius |
| L7 | Governance escalation and audit replay — escalating a policy violation, replaying an audit chain during incident review |

See [../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md)
for the general failure categories and
[../failures/FAILURE-CASE-INDEX.md](../failures/FAILURE-CASE-INDEX.md) for
specific investigated cases.

## Relationship to the research thesis

The research thesis in
[../doctrine/research-thesis.md](../doctrine/research-thesis.md) frames the
same problem as a conceptual pipeline (AI MODEL → CONTEXT → MEMORY →
RETRIEVAL → REASONING → AGENTS → GOVERNANCE → AUDIT → RECOVERY). That
pipeline is a research narrative describing *why* each concern matters; this
specification is the canonical, versioned architectural definition of *how*
CORE-AI/7 structures those concerns into seven implementable layers plus a
cross-cutting recovery model. Where the two differ in vocabulary, this
specification governs implementation and evidence mapping.

## Conformance

Every other document in this repository that describes the architecture —
`system-overview.md`, `architectural-principles.md`, `boundaries.md`, the
evidence and claims registries, the implementation map, diagrams, and the
README — must use the layer names and scopes defined here. Deviations are
tracked as revisions in
[ARCHITECTURE-VERSION-MATRIX.md](ARCHITECTURE-VERSION-MATRIX.md), not as
silent drift.
