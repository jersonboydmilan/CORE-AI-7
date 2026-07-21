# Research Questions

Organized by the architectural concern each question targets.

## Sovereignty

- What is the minimal set of local components needed for a system to
  operate with zero required outbound network dependency, without
  sacrificing capability?
- Where does "sovereign" stop being a binary property and start being a
  spectrum (e.g., a system with an optional, non-required remote backend)?

## System inspectability

- What is the right granularity for logging agent decisions such that logs
  are useful for audit without becoming unreviewable noise?
- Can inspectability be verified structurally (e.g., "this event type is
  guaranteed to be logged") rather than only by convention?

## Memory integrity

- How should a memory layer detect and represent uncertainty about the
  provenance of what it stores?
- What recovery guarantees should a memory layer offer after an
  interrupted write, and how should those guarantees be verified rather
  than assumed?

## Retrieval trust

- How should a retrieval layer represent the difference between "this item
  was retrieved" and "this item is trustworthy"?
- What is the right boundary for treating retrieved content as context
  versus as ground truth?

## Failure recovery

- What categories of failure are specific to agentic systems (as opposed
  to conventional software), and which of the general-purpose recovery
  techniques (checkpointing, write-ahead logging, idempotent replay)
  transfer cleanly?
- How should cascading failure across multiple cooperating agents be
  contained rather than merely detected after the fact?

## Governance enforcement

- Can governance be structured as a runtime gate that is genuinely
  unbypassable by construction, rather than a policy that agents are
  expected to honor?
- How should governance evolve without becoming either too rigid to be
  useful or too permissive to be meaningful?

## Auditability

- What is the minimum structural property (e.g., tamper-evidence via
  hash-chaining) needed for an audit log to be trustworthy without trusting
  the host it runs on?

## Reproducibility

- What has to be fixed (build identity, workload, environment class) for a
  validation scenario to be meaningfully re-runnable, and what can safely
  vary?
- What would it take for an external party to independently reproduce a
  CORE-AI/7 validation result without access to the private implementation?

## Local operation and system resilience

- How does system behavior degrade — gracefully or otherwise — as local
  hardware resources become constrained?
- What is the right abstraction boundary so that swapping a local
  compute or inference backend does not require changes above the layer
  that owns it?

These questions are open. Answers that exist today are documented, with
their evidence class, in [../EVIDENCE-MAP.md](../EVIDENCE-MAP.md).
