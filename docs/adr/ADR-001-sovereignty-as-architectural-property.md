# ADR-001 — Sovereignty as an Architectural Property

## Context

Most AI systems delegate compute, memory, and inference to remote,
third-party services by default, and treat local/offline operation as an
optional deployment mode if it is supported at all.

## Decision

CORE-AI/7 treats sovereignty — the ability to run under local control with
no required outbound network dependency — as a first-class architectural
requirement applied at every layer, not an optional deployment
configuration decided late.

## Alternatives considered

- **Sovereignty as a deployment option.** Build against hosted services by
  default, offer a local mode later. Rejected: retrofitting local operation
  onto a system designed around hosted dependencies tends to leave hidden
  network assumptions throughout the stack.
- **Hybrid-by-default.** Always assume some remote fallback is available.
  Rejected: this reintroduces the exact availability and trust dependency
  the research thesis is investigating (see
  [../doctrine/research-thesis.md](../doctrine/research-thesis.md)).

## Tradeoffs

Local-only operation forecloses some capability that is easiest to get
from large hosted models, and shifts hardware/compute cost to the
operator. It also removes an entire class of external failure and
data-exfiltration risk.

## Consequences

Every layer's design must justify itself without assuming a network is
present. This shapes L1 (local compute/inference), L3 (local durable
storage instead of a hosted database), and the dependency-surface policy
applied throughout.
