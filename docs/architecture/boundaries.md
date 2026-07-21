# Boundaries

Layer names follow [CORE-AI-7-SPECIFICATION.md](CORE-AI-7-SPECIFICATION.md)
(L3 = Memory & Retrieval, L6 = Agent Coordination).

## Trust boundaries

Every layer transition in CORE-AI/7 is a trust boundary, not just a
function call. The most significant transitions:

- **L3 → L4/L5 (memory into reasoning).** Retrieved memory is context, not
  ground truth, until it has been used. Nothing in L4/L5 is entitled to
  treat retrieved content as pre-validated.
- **L5/L6 output → L7 (agent output into governance).** No agent output is
  persisted to memory or surfaced to a user until it has passed governance
  evaluation. This boundary exists specifically to break the context
  corruption cascade described in
  [../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md).
- **L6 agent → agent.** Agents exchange typed messages, not shared mutable
  state, so a compromised or corrupted agent cannot silently mutate
  another agent's working context.

## Failure boundaries

Failure is expected to be contained at the layer where it is detected, not
propagated upward silently:

- A storage-layer (L3) failure must not corrupt in-flight reasoning (L4)
  without detection.
- A single agent's failure (L5/L6) must cascade-cancel only its own
  dependents, not the whole task graph.
- A governance rejection (L7) must not be bypassable by retrying at a lower
  layer.

## Governance boundaries

Governance (L7) sits above orchestration and coordination by design: policy
and audit are architectural concerns, not optional middleware. This is a
deliberate departure from designs where guardrails are bolted onto an agent
loop after the fact.

## Data-flow and control-flow concepts

- **Data flow** is upward and layer-local: each layer consumes only the
  layer(s) immediately beneath it.
- **Control flow** for governance is the exception to the upward-only rule:
  L7 can reject or gate outputs from L5/L6 before they affect L3 state,
  which is a downward control action layered on top of upward data flow.

This document describes conceptual boundaries only. Enforcement mechanisms
are part of the private implementation.
