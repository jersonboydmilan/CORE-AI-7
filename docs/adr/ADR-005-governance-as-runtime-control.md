# ADR-005 — Governance as Runtime Control

## Context

Guardrails on AI system output are frequently implemented as external
review, prompt-level instruction, or a post-hoc filter that is easy to
bypass by construction.

## Decision

Governance (L7) is a runtime layer that sits structurally above
orchestration and coordination: agent output must pass evaluation before
it is persisted to memory or surfaces to a user, enforced by the system's
control flow rather than by convention.

## Alternatives considered

- **Guardrails as documentation/policy.** Rely on agent instructions or
  external process to enforce correct behavior. Rejected: this cannot
  address the context-corruption cascade, since a single non-compliant
  write bypasses the whole control.
- **Guardrails as an optional post-processing step.** Rejected: optional
  steps are the first thing skipped under time or resource pressure; the
  goal is a control that cannot be skipped by omission.

## Tradeoffs

Runtime-enforced governance adds latency and complexity to every write
path, and requires the evaluation gate itself to be trustworthy and
maintained. It buys an architectural (not merely procedural) guarantee
that unvetted output cannot become future context.

## Consequences

L5/L6 (orchestration/coordination) cannot write to L3 (memory) without
passing through L7. This ordering constraint is treated as a structural
invariant of the architecture, not a convention.
