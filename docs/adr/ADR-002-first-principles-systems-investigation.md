# ADR-002 — First-Principles Systems Investigation

## Context

Framework-assembled AI systems obscure how their components actually work:
autodiff, retrieval indexing, and agent scheduling are typically opaque
dependencies rather than reviewable code.

## Decision

Components with direct educational or security value to the research
thesis — automatic differentiation, sequence-model primitives, approximate
retrieval indexing, durable storage, agent scheduling — are investigated
and implemented from first principles rather than assembled from
general-purpose frameworks, so their behavior is fully attributable and
reviewable.

## Alternatives considered

- **Framework composition.** Assemble the system from established
  frameworks and libraries. Rejected as the primary approach: it would
  answer "can a sovereign system be assembled," not "what does sovereign
  system design actually require" — the latter is the research question.
- **First-principles everywhere, including non-load-bearing utility code.**
  Rejected: reimplementing components with no research or security value
  (general numerical kernels, standard data formats) would dilute focus
  without answering a research question.

## Tradeoffs

First-principles implementation is slower to build and carries real risk
of falling short of specialized libraries on raw performance (documented
per-component in sanitized benchmarks). It buys reviewability, no opaque
dependency risk, and direct evidence for the research questions in
[../doctrine/research-questions.md](../doctrine/research-questions.md).

## Consequences

Every load-bearing algorithmic component must be attributable to a
specific research question. A general-purpose numerical substrate is
retained underneath first-principles components where its role is
execution, not modeling — the distinction is what is being investigated
versus what is being relied upon.
