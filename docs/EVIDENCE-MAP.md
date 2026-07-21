# Evidence Map

Every claim CORE-AI/7 makes publicly is listed here with the design it
maps to, its evidence category, whether public evidence exists, and its
honest status. `IMPLEMENTED — PRIVATE` and `TESTED — PRIVATE` are never
represented as `PUBLICLY REPRODUCIBLE`.

## Status values

```
DOCUMENTED
DESIGNED
IMPLEMENTED — PRIVATE
TESTED — PRIVATE
SANITIZED EVIDENCE AVAILABLE
SCENARIO-VALIDATED
INDEPENDENTLY REPRODUCED
PRODUCTION VALIDATED
```

## Claims

| Claim | Design | Evidence Category | Public Evidence | Status |
|---|---|---|---|---|
| Local, dynamic-graph automatic differentiation, gradients verified against numerical differentiation | L4 (Reasoning/Primitives) | Unit-test suite | Sanitized test-count summary | TESTED — PRIVATE |
| Transformer-style sequence model trainable end-to-end on local CPU compute | L4 | Training run + benchmark | Sanitized throughput summary | SANITIZED EVIDENCE AVAILABLE |
| Native local-compute acceleration path as an alternative substrate to a general numerical library | L1 (Computation) | Benchmark comparison | Sanitized throughput summary | SANITIZED EVIDENCE AVAILABLE |
| Crash-safe durable storage: write-ahead log with fsync-before-acknowledge and checksum-verified recovery | L3 (Memory & Context) | Fault-injection test suite | Methodology + sanitized summary | SCENARIO-VALIDATED |
| Approximate nearest-neighbor retrieval index built from scratch (no third-party ANN library) | L3 | Recall/latency benchmark vs. brute-force ground truth | Sanitized recall/latency summary | SANITIZED EVIDENCE AVAILABLE |
| Deletion handling that does not require a full index rebuild per delete | L3 | Structural test + benchmark | Methodology public, detailed results private | TESTED — PRIVATE |
| Offline retrieval-augmented generation pipeline, zero required network calls | L5 (Orchestration) | End-to-end evaluation dataset | Sanitized quality-metric summary | SANITIZED EVIDENCE AVAILABLE |
| Dependency-aware multi-agent scheduling with cascade failure containment | L6 (Coordination) | Scenario test suite | Methodology public | SCENARIO-VALIDATED |
| Hallucination / grounding evaluation gate | L7 (Governance & Audit) | Adversarial evaluation set | Sanitized summary | SANITIZED EVIDENCE AVAILABLE |
| Regression gate against a checked-in quality baseline | L7 | Automated gate, run per build | Sanitized pass/fail summary | SANITIZED EVIDENCE AVAILABLE |
| Tamper-evident audit logging via hash-chained records | L7 | Structural verification test | Methodology public | TESTED — PRIVATE |
| Zero required outbound network dependency across all layers | Cross-cutting (sovereignty) | Dependency-surface audit | Documented policy | DOCUMENTED |
| Independent third-party reproduction of any result above | — | — | — | not established |
| Production-scale deployment validation | — | — | — | not established |

## How to read this table

- `DESIGNED` means the property is an architectural intent with no
  implementation evidence cited here.
- `IMPLEMENTED — PRIVATE` / `TESTED — PRIVATE` mean the property has a
  private implementation and private test evidence, but nothing publicly
  reproducible.
- `SANITIZED EVIDENCE AVAILABLE` means a summary exists under
  [../evidence/](../evidence/) or [../../benchmarks/](../../benchmarks/)
  that does not expose private implementation.
- `SCENARIO-VALIDATED` means the claim passed the full validation chain in
  [validation/VALIDATION-METHODOLOGY.md](validation/VALIDATION-METHODOLOGY.md)
  at least once, under laboratory conditions.
- `INDEPENDENTLY REPRODUCED` and `PRODUCTION VALIDATED` are not currently
  used for any claim in this repository.
