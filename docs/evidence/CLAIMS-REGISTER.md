# Claims Register

Every important public claim about CORE-AI/7 has a stable ID here. Each
claim is rated at the **highest evidence level it actually supports** —
never higher. See [EVIDENCE-REGISTRY.md](EVIDENCE-REGISTRY.md) for the
underlying evidence and [BENCHMARK-REGISTRY.md](BENCHMARK-REGISTRY.md) for
performance detail.

## Evidence level scale

| Level | Name | Meaning |
|---|---|---|
| E0 | Conceptual | Idea or thesis only |
| E1 | Designed | Formal architecture or specification exists |
| E2 | Implemented | Capability exists in an implementation |
| E3 | Internally validated | Automated tests or controlled internal/laboratory experiments support the claim |
| E4 | Publicly reproducible | An external researcher can reproduce the result from public materials |
| E5 | Independently validated | An independent party has reproduced or verified the result |
| E6 | Production validated | Sustained operational performance demonstrated in a documented production environment |

No claim in this register is currently above **E3**. None are E4, E5, or
E6.

---

## CORE-AI-7-C-001

**Claim.** Core execution requires no outbound network dependency (local
compute sovereignty).
**Layer.** L1 — Compute & Runtime.
**Claim type.** Architectural.
**Evidence.** Dependency-surface policy and audit; see
[EVIDENCE-REGISTRY.md#core-ai-7-e-006](EVIDENCE-REGISTRY.md#core-ai-7-e-006).
**Evidence level.** E3.
**Limitations.** Audited against the private implementation's dependency
manifest at a point in time; not continuously enforced by a public,
independently-run check.
**Does NOT establish.** That no future dependency could reintroduce a
network requirement; that the private implementation has been audited by
a third party.

## CORE-AI-7-C-002

**Claim.** Model inference executes via a local backend (in-process or
local subprocess), with no cloud inference path in the default
configuration.
**Layer.** L1.
**Claim type.** Implementation.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-001](EVIDENCE-REGISTRY.md#core-ai-7-e-001).
**Evidence level.** E3.
**Limitations.** Validated for the reference build's supported inference
backend only.
**Does NOT establish.** Performance or correctness of arbitrary
third-party local model weights.

## CORE-AI-7-C-003

**Claim.** Knowledge/data locality: ingestion, chunking, and embedding
generation operate on local corpora without transmitting source documents
off-device.
**Layer.** L2 — Knowledge & Data.
**Claim type.** Architectural.
**Evidence.** Dependency-surface policy; scenario evaluation in
[EVIDENCE-REGISTRY.md#core-ai-7-e-003](EVIDENCE-REGISTRY.md#core-ai-7-e-003).
**Evidence level.** E3.
**Limitations.** Evaluated on a small fixed corpus, not production-scale
data volumes.
**Does NOT establish.** Behavior on corpora with materially different
size, format diversity, or adversarial document content.

## CORE-AI-7-C-004

**Claim.** Tokenization and embedding-generation are round-trip correct
and deterministic for a given input.
**Layer.** L2.
**Claim type.** Implementation.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-006](EVIDENCE-REGISTRY.md#core-ai-7-e-006).
**Evidence level.** E3.
**Limitations.** Internal unit-test evidence only.
**Does NOT establish.** Semantic quality of the representations produced.

## CORE-AI-7-C-005

**Claim.** Persistent memory is crash-safe: durability is acknowledged
only after a write is committed, and recovery restores exactly the
committed prefix after an interruption.
**Layer.** L3 — Memory & Retrieval.
**Claim type.** Implementation / Security.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-004](EVIDENCE-REGISTRY.md#core-ai-7-e-004).
**Evidence level.** E3.
**Limitations.** Validated under a defined, non-exhaustive set of injected
fault conditions in a controlled laboratory environment; detailed fault
technique and pass/fail counts are private (public-safety review pending).
**Does NOT establish.** Resilience against fault classes outside the
tested set, or behavior under sustained high-concurrency write load
(single-writer design — see
[../doctrine/limitations.md](../doctrine/limitations.md)).

## CORE-AI-7-C-006

**Claim.** Approximate nearest-neighbor retrieval achieves recall
approaching exact-search parity at higher search effort, with sub-second
per-query latency at the tested scale.
**Layer.** L3.
**Claim type.** Performance.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-002](EVIDENCE-REGISTRY.md#core-ai-7-e-002);
[BENCHMARK-REGISTRY.md#core-ai-7-bm-002](BENCHMARK-REGISTRY.md#core-ai-7-bm-002).
**Evidence level.** E3.
**Limitations.** Single corpus scale and dimensionality tested; not
benchmarked under high delete/compaction fraction.
**Does NOT establish.** Performance at production-scale corpora or under
concurrent multi-process access.

## CORE-AI-7-C-007

**Claim.** Context assembly at the memory layer records provenance
(source, timestamp, writer) for items entering an agent's context window.
**Layer.** L3.
**Claim type.** Architectural.
**Evidence.** Design specification; see
[boundaries.md](../architecture/boundaries.md).
**Evidence level.** E2.
**Limitations.** Implemented in the private reference build; not yet
covered by a dedicated public evidence entry.
**Does NOT establish.** That provenance metadata is independently
verifiable outside the private implementation.

## CORE-AI-7-C-008

**Claim.** Reasoning (local model inference) treats retrieved memory as
context, not as ground truth, and does not execute against remote model
endpoints.
**Layer.** L4 — Reasoning.
**Claim type.** Architectural.
**Evidence.** Design specification; see
[boundaries.md](../architecture/boundaries.md).
**Evidence level.** E2.
**Limitations.** The trust distinction is architectural; no dedicated
evaluation isolates "context vs. ground-truth" handling as its own
measured claim yet.
**Does NOT establish.** That downstream reasoning is immune to
prompt-injection-style manipulation via retrieved context.

## CORE-AI-7-C-009

**Claim.** The offline retrieval-augmented generation pipeline achieves
high retrieval accuracy and zero hallucinated answers on a fixed
adversarial probe set, at low measured latency (excluding live large-model
inference).
**Layer.** L4/L5 (reasoning output, exercised through the orchestration
pipeline).
**Claim type.** Performance.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-003](EVIDENCE-REGISTRY.md#core-ai-7-e-003);
[BENCHMARK-REGISTRY.md#core-ai-7-bm-003](BENCHMARK-REGISTRY.md#core-ai-7-bm-003).
**Evidence level.** E3.
**Limitations.** Small fixed corpus and question set; extractive backend,
not a live large local model, was in the loop for this measurement.
**Does NOT establish.** Hallucination behavior with a live local model
backend or at production corpus scale.

## CORE-AI-7-C-010

**Claim.** Orchestration provides workflow recovery: retry/backoff and
failure escalation for interrupted or failed tasks.
**Layer.** L5 — Orchestration.
**Claim type.** Architectural / Implementation.
**Evidence.** Design specification; see
[../architecture/CORE-AI-7-SPECIFICATION.md](../architecture/CORE-AI-7-SPECIFICATION.md#recovery-model).
**Evidence level.** E2.
**Limitations.** Not yet covered by a dedicated scenario-validation
evidence entry in this register.
**Does NOT establish.** Recovery behavior under compound/cascading
multi-task failure at scale.

## CORE-AI-7-C-011

**Claim.** Multi-agent task graphs are acyclic by construction and contain
failure to a task's dependents via cascade cancellation, rather than
propagating failure across the whole graph.
**Layer.** L6 — Agent Coordination.
**Claim type.** Implementation.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-007](EVIDENCE-REGISTRY.md#core-ai-7-e-007).
**Evidence level.** E3.
**Limitations.** Validated under the private test suite's injected-failure
scenarios; not benchmarked at large agent-graph scale.
**Does NOT establish.** Behavior under adversarial or Byzantine agent
inputs.

## CORE-AI-7-C-012

**Claim.** Agent coordination supports session isolation and divergence
detection between cooperating agents.
**Layer.** L6.
**Claim type.** Architectural.
**Evidence.** None published yet.
**Evidence level.** E1.
**Limitations.** Designed scope per
[../architecture/CORE-AI-7-SPECIFICATION.md](../architecture/CORE-AI-7-SPECIFICATION.md);
implementation and validation status not yet documented publicly.
**Does NOT establish.** That divergence detection is implemented or
tested in the current reference build. Stated conservatively pending
confirmation.

## CORE-AI-7-C-013

**Claim.** Agent/pipeline output is evaluated against a governance gate
before it may be persisted to memory or surfaced to a user.
**Layer.** L7 — Governance & Audit.
**Claim type.** Architectural / Implementation.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-008](EVIDENCE-REGISTRY.md#core-ai-7-e-008).
**Evidence level.** E3.
**Limitations.** Gate content (evaluation criteria, adversarial set size)
is private; only the pass/fail outcome and methodology category are
public.
**Does NOT establish.** That the gate is comprehensive against all
possible harmful or corrupted outputs.

## CORE-AI-7-C-014

**Claim.** Audit records are tamper-evident via hash-chaining: tampering
is structurally detectable from the log content, independent of file
permissions.
**Layer.** L7.
**Claim type.** Security.
**Evidence.** Structural verification test, private; see
[../adr/ADR-006-auditability-and-integrity.md](../adr/ADR-006-auditability-and-integrity.md).
**Evidence level.** E3.
**Limitations.** Tamper-*evident*, not tamper-*proof* — an attacker able
to rewrite an entire chain from scratch is not caught by this mechanism
alone; stated explicitly in ADR-006.
**Does NOT establish.** Tamper-proofing, or protection against a fully
compromised host.

## CORE-AI-7-C-015

**Claim.** A regression gate compares each build against a checked-in
quality baseline and blocks regressions.
**Layer.** L7.
**Claim type.** Validation.
**Evidence.** [EVIDENCE-REGISTRY.md#core-ai-7-e-005](EVIDENCE-REGISTRY.md#core-ai-7-e-005).
**Evidence level.** E3.
**Limitations.** Baseline and gate thresholds are private and
self-defined by the implementers.
**Does NOT establish.** That the baseline itself represents an externally
validated quality bar.

## CORE-AI-7-C-016

**Claim.** Recovery is addressed as an explicit, per-layer concern across
the architecture (Cross-Cutting), not as a single bolted-on recovery
subsystem.
**Layer.** Cross-Cutting (L1–L7).
**Claim type.** Architectural.
**Evidence.** [../architecture/CORE-AI-7-SPECIFICATION.md](../architecture/CORE-AI-7-SPECIFICATION.md#recovery-model);
per-layer evidence varies — see
[../implementation/RESEARCH-TO-IMPLEMENTATION-MAP.md](../implementation/RESEARCH-TO-IMPLEMENTATION-MAP.md).
**Evidence level.** E2 (varies by layer — L3 and L6 recovery reach E3 via
C-005 and C-011; L2, L4, L5, L7 recovery concerns are currently designed
or implemented without a dedicated validation entry).
**Limitations.** This claim intentionally aggregates uneven per-layer
maturity; readers should consult the per-layer claims above rather than
treat "recovery" as a single validated property.
**Does NOT establish.** Uniform recovery maturity across all seven
layers.
