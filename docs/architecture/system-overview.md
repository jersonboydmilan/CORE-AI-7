# System Overview

CORE-AI/7 defines eight conceptual stages an intelligence system passes
through, from the AI model itself to full sovereign infrastructure, and
seven architectural layers that implement that path. The public description
here is deliberately at a conceptual abstraction level: it names layer
responsibilities and boundaries, not internal classes, module names, or
implementation strategy.

## Layer stack

```
        ┌───────────────────────────────────────────────────────────┐
        │  L7  GOVERNANCE & AUDIT                                    │
        │      evaluation gates · output policy ·                    │
        │      tamper-evident audit logging                          │
        ├───────────────────────────────────────────────────────────┤
   ▲    │  L6  COORDINATION                                          │
   │    │      multi-agent task graphs · typed message passing ·     │
   │    │      cascade failure containment                           │
   │    ├───────────────────────────────────────────────────────────┤
   │    │  L5  ORCHESTRATION                                         │
   d    │      agent loop · scheduling · retrieval-augmented         │
   a    │      generation pipeline                                   │
   t    ├───────────────────────────────────────────────────────────┤
   a    │  L4  REASONING / PRIMITIVES                                │
   │    │      learned representations · attention · sequence        │
   │    │      modeling primitives                                   │
   l    ├───────────────────────────────────────────────────────────┤
   i    │  L3  MEMORY & CONTEXT MANAGEMENT                            │
   f    │      durable storage · approximate retrieval · context      │
   e    │      assembly                                              │
   c    ├───────────────────────────────────────────────────────────┤
   y    │  L2  EMBEDDINGS                                            │
   c    │      tokenization · representation learning                │
   l    ├───────────────────────────────────────────────────────────┤
   e    │  L1  COMPUTATION                                           │
   │    │      local execution substrate · local inference backend   │
        └───────────────────────────────────────────────────────────┘
```

## Layer responsibilities

**L1 — Computation.** The execution substrate every layer above ultimately
runs on. Local-only by design: no layer above may depend on a remote
compute or inference service to function.

**L2 — Embeddings.** Converts raw input into the representations the rest
of the stack operates on. Owns the tokenization and representation-learning
contract that L3 and L4 depend on.

**L3 — Memory & Context Management.** Durable storage and retrieval. This
is the layer where context enters an agent's working set, and therefore
the primary choke point for provenance and integrity control — see
[boundaries.md](boundaries.md) and the failure-research documentation.

**L4 — Reasoning / Primitives.** Learned computation over representations:
attention, sequence modeling, and the primitive operations reasoning is
built from.

**L5 — Orchestration.** The agent loop — plan, act, observe — and the
retrieval-augmented generation pipeline that connects reasoning to memory.

**L6 — Coordination.** Multi-agent scheduling and message passing. Agents
exchange typed messages rather than sharing raw state directly, which
bounds how far a single agent's corrupted state can propagate.

**L7 — Governance & Audit.** Evaluation gates that outputs must pass before
they are allowed to affect persistent state, plus an audit layer that
records decisions in a tamper-evident form.

## Relationship between layers

Data flows upward: raw compute at the bottom, governed and audited
intelligence at the top. Control flows are layer-local — a layer only
depends on the layer(s) immediately beneath it, so that substituting an
implementation at one layer (for example, a different local inference
backend at L1) does not require changes above L2.

## Trust and failure boundaries

Each layer boundary is also a trust boundary: data crossing from L3 into
L4/L5 is treated as context, not as ground truth, until it has passed
through governance (L7). Failure boundaries are discussed in
[../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md).

This is a design description, not an implementation disclosure — internal
module names, class structures, and algorithms live in the private
implementation repository.
