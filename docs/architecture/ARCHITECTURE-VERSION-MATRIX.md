# Architecture Version Matrix

Tracks CORE-AI/7 architecture revisions across the canonical specification,
the research thesis framing, the public research architecture documents,
and the private implementation mapping, to prevent silent architecture
drift.

| Version | Date | Change | Reason | Affected layers | Backward compatibility | Evidence affected |
|---|---|---|---|---|---|---|
| 0.1 | 2026-07-21 | Initial public architecture: informal 7-layer model (Computation, Embeddings, Memory & Context Management, Primitives/Reasoning, Orchestration, Coordination, Governance & Audit) plus an 8-stage doctrine pipeline (AI MODEL→CONTEXT→MEMORY→RETRIEVAL→REASONING→AGENTS→GOVERNANCE→AUDIT→RECOVERY). | Initial public research record publication. | L1–L7 (informal) | N/A — initial version | Initial `docs/EVIDENCE-MAP.md` |
| 0.2 | 2026-07-21 | Canonicalized to `docs/architecture/CORE-AI-7-SPECIFICATION.md`: renamed L2 Embeddings → Knowledge & Data, L3 Memory & Context Management → Memory & Retrieval, L4 Primitives/Reasoning → Reasoning, L6 Coordination → Agent Coordination; expanded per-layer scope (session isolation, divergence detection, circuit breakers, human-in-the-loop checkpoints, cryptographic signing); made Recovery an explicit cross-cutting model instead of an implicit property. | Establish one canonical, versioned architecture definition that all other documents conform to, and make recovery ownership explicit per layer instead of assumed. | L2, L3, L4, L6; Recovery (cross-cutting, all layers) | Layer numbering (L1–L7) preserved; layer names and scope changed — see conformance note below | `docs/EVIDENCE-MAP.md` layer labels updated; new `docs/evidence/CLAIMS-REGISTER.md` and `docs/evidence/EVIDENCE-REGISTRY.md` established at this version |

## Conformance note (v0.1 → v0.2)

Layer *numbers* did not change — a document referencing "L3" before and
after v0.2 refers to the same position in the stack. Layer *names and
scope* changed for L2, L3, L4, and L6. Documents written under v0.1 naming
have been updated to v0.2 naming as part of this revision; see the
per-file changes recorded in
[../../RESEARCH-CHANGELOG.md](../../RESEARCH-CHANGELOG.md).

## Future revisions

Any future change to the canonical specification must add a row here
before or in the same change as the specification edit, stating what
changed, why, which layers are affected, whether the change is backward
compatible, and which published evidence (claims, evidence entries,
benchmarks) is affected by the change.
