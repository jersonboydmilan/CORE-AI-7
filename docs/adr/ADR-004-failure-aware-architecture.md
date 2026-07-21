# ADR-004 — Failure-Aware Architecture

## Context

Failure handling is often added to AI systems reactively, after a specific
incident, rather than designed in from the start.

## Decision

Every layer must define its expected behavior under failure — the
taxonomy in
[../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md)
— as part of its initial design, and that behavior is exercised under the
validation methodology before being considered complete.

## Alternatives considered

- **Best-effort with incident-driven hardening.** Handle failures as they
  are discovered in practice. Rejected as the primary strategy: this
  produces an architecture whose failure behavior is unknown until it is
  tested by an actual incident, which is precisely the risk the research
  program investigates.
- **Failure handling as a separate cross-cutting layer bolted on later.**
  Rejected: failure behavior interacts with data durability and agent
  coordination too directly to be added after the fact without redesign.

## Tradeoffs

Designing for failure up front is slower and requires defining acceptance
criteria (what counts as correct recovery) before a feature is considered
done. It produces a system whose failure behavior is characterized rather
than discovered in production.

## Consequences

New capability requiring durable state or multi-step coordination must
specify its failure categories and recovery expectations as part of its
design, not as a follow-up.
