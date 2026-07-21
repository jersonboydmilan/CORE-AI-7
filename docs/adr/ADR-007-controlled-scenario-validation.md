# ADR-007 — Controlled Scenario Validation

## Context

Claims about system behavior — performance, recovery correctness,
retrieval quality — need evidence, but the private implementation cannot
be published for independent verification without violating the
public/private boundary this repository operates under.

## Decision

Claims are validated through the controlled laboratory methodology in
[../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md):
defined scenario, defined build, defined workload, explicit measurement,
and — where relevant — failure injection and recovery verification. Only
claims that pass this chain are published as validated, and every claim's
status is tracked honestly in [../EVIDENCE-MAP.md](../EVIDENCE-MAP.md).

## Alternatives considered

- **No public evidence at all.** Publish only architecture and thesis,
  with no evidence claims. Rejected: this would understate work that has
  actually been done and verified, reducing the credibility of the
  research record.
- **Publish raw private benchmark output directly.** Rejected: raw output
  risks exposing implementation detail, infrastructure, or configuration
  that belongs on the private side of the boundary in
  [../PUBLIC-PRIVATE-BOUNDARY.md](../PUBLIC-PRIVATE-BOUNDARY.md).
- **Claim independent reproduction status without an independent
  reproducer.** Rejected outright as a matter of policy — see the claims
  discipline in [../EVIDENCE-MAP.md](../EVIDENCE-MAP.md).

## Tradeoffs

Sanitized, self-reported evidence is weaker than independent, third-party
verification, and this repository says so explicitly wherever the
distinction matters. The alternative — silence or overclaiming — was
judged worse for long-term credibility.

## Consequences

Every published evidence entry must be traceable to a specific scenario,
build, and methodology run. No sanitized number is published without the
methodology that produced it also being public.
