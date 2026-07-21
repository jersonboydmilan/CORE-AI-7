# ADR-003 — Explicit Intelligence System Boundaries

## Context

In many agentic AI systems, memory, reasoning, and governance are not
cleanly separated — an agent can write to memory and take actions without
a defined checkpoint between "generated" and "trusted."

## Decision

CORE-AI/7 requires every layer transition to be a named, explicit boundary
— trust, failure, or governance — documented in
[../architecture/boundaries.md](../architecture/boundaries.md), rather than
an implicit consequence of code structure.

## Alternatives considered

- **Implicit boundaries.** Let boundaries emerge from module structure.
  Rejected: implicit boundaries are easy to erode over time as code
  changes, and give no fixed point to reason about failure containment.
- **A single global boundary (input validation only).** Rejected: this
  does not address the context-corruption cascade, which requires
  boundaries at multiple points in the memory/reasoning/agent loop, not
  just at system input.

## Tradeoffs

Explicit boundaries add structural overhead — every new capability has to
declare which boundary it crosses and how. This is deliberate friction, in
exchange for a system where trust and failure containment can be reasoned
about layer by layer.

## Consequences

Governance (L7) sits structurally above orchestration and coordination.
Memory (L3) is required to record provenance at the point of context
assembly, since that is the boundary where corrupted context could
otherwise enter reasoning unmarked.
