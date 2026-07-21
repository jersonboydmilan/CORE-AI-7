# System Overview

**Canonical reference:** [CORE-AI-7-SPECIFICATION.md](CORE-AI-7-SPECIFICATION.md)
is the authoritative layer definition. This document is a narrative
companion — read the specification for exact scope per layer.

## Layer stack

```
        ┌───────────────────────────────────────────────────────────┐
        │  L7  GOVERNANCE & AUDIT                                    │
        │      policy enforcement · guardrails · audit logging ·     │
        │      tamper evidence                                       │
        ├───────────────────────────────────────────────────────────┤
   ▲    │  L6  AGENT COORDINATION                                    │
   │    │      agent identity/capabilities · dependency graphs ·     │
   │    │      trust flow · cascade failure containment              │
   │    ├───────────────────────────────────────────────────────────┤
   │    │  L5  ORCHESTRATION                                         │
   d    │      workflow execution · retry/backoff · recovery         │
   a    │      coordination                                          │
   t    ├───────────────────────────────────────────────────────────┤
   a    │  L4  REASONING                                             │
   │    │      local model inference · context construction ·        │
   l    │      output validation                                     │
   i    ├───────────────────────────────────────────────────────────┤
   f    │  L3  MEMORY & RETRIEVAL                                    │
   e    │      durable storage · approximate retrieval · context      │
   c    │      assembly · retrieval trust                            │
   y    ├───────────────────────────────────────────────────────────┤
   c    │  L2  KNOWLEDGE & DATA                                      │
   l    │      ingestion · chunking · embedding generation ·          │
   e    │      data provenance                                       │
        ├───────────────────────────────────────────────────────────┤
        │  L1  COMPUTE & RUNTIME                                     │
        │      local execution substrate · local inference runtime   │
        └───────────────────────────────────────────────────────────┘
```

## Layer responsibilities

**L1 — Compute & Runtime.** The execution substrate every layer above
ultimately runs on. Local-only by design: no layer above may depend on a
remote compute or inference service to function.

**L2 — Knowledge & Data.** Converts raw documents and structured data into
the representations the rest of the stack operates on, and is the point
where provenance of external material first enters the system.

**L3 — Memory & Retrieval.** Durable storage and retrieval. This is the
layer where context enters an agent's working set, and therefore the
primary choke point for provenance and integrity control — see
[boundaries.md](boundaries.md) and the failure-research documentation.

**L4 — Reasoning.** Local model inference and the primitives it depends
on: prompt/context construction, context-window management, structured
output.

**L5 — Orchestration.** The agent loop — plan, act, observe — plus
workflow execution, retry/backoff, and the retrieval-augmented generation
pipeline that connects reasoning to memory.

**L6 — Agent Coordination.** Multi-agent scheduling and message passing.
Agents exchange typed messages rather than sharing raw state directly,
which bounds how far a single agent's corrupted state can propagate.

**L7 — Governance & Audit.** Evaluation gates that outputs must pass
before they are allowed to affect persistent state, plus an audit layer
that records decisions in a tamper-evident form.

## Relationship between layers

Data flows upward: local compute at the bottom, governed and audited
intelligence at the top. Control flows are layer-local — a layer only
depends on the layer(s) immediately beneath it, so that substituting an
implementation at one layer (for example, a different local inference
backend at L1) does not require changes above L2.

## Trust and failure boundaries

Each layer boundary is also a trust boundary: data crossing from L3 into
L4/L5 is treated as context, not as ground truth, until it has passed
through governance (L7). Failure boundaries are discussed in
[../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md)
and specific cases in
[../failures/FAILURE-CASE-INDEX.md](../failures/FAILURE-CASE-INDEX.md).

## Recovery

Recovery is a cross-cutting property, not a layer — each layer above
defines its own recovery concern. See
[CORE-AI-7-SPECIFICATION.md#recovery-model](CORE-AI-7-SPECIFICATION.md#recovery-model).

This is a design description, not an implementation disclosure — internal
module names, class structures, and algorithms live in the private
implementation repository.
