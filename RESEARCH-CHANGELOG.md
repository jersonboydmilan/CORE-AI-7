# Research Changelog

Tracks the evolution of the CORE-AI/7 research program itself — distinct
from [CHANGELOG.md](CHANGELOG.md), which tracks changes to this
repository's published documents.

## 2026-07-21 — Public research record: initial publication

- Research thesis and research questions published
  ([docs/doctrine/](docs/doctrine/)).
- Informal seven-layer architecture and eight-stage doctrine pipeline
  published in README and `docs/architecture/system-overview.md`.
- Initial `docs/EVIDENCE-MAP.md` published with 14 claims.
- Validation methodology, failure taxonomy, seven ADRs, sanitized
  benchmark entries, and roadmap published.

## 2026-07-21 — Architecture canonicalization

- Established `docs/architecture/CORE-AI-7-SPECIFICATION.md` as the
  single canonical architecture definition, superseding the informal
  layer descriptions previously scattered across `README.md` and
  `docs/architecture/system-overview.md`.
- Renamed L2 (Embeddings → Knowledge & Data), L3 (Memory & Context
  Management → Memory & Retrieval), L4 (Primitives/Reasoning →
  Reasoning), and L6 (Coordination → Agent Coordination); expanded scope
  for session isolation, divergence detection, circuit breakers,
  human-in-the-loop checkpoints, and cryptographic signing. Layer numbers
  L1–L7 unchanged. Full record:
  `docs/architecture/ARCHITECTURE-VERSION-MATRIX.md`.
- Made recovery an explicit cross-cutting model (per-layer recovery
  concerns) rather than an implicit property.
- Reconciled the doctrine research-thesis pipeline (AI MODEL → CONTEXT →
  MEMORY → RETRIEVAL → REASONING → AGENTS → GOVERNANCE → AUDIT →
  RECOVERY) against the canonical specification: the pipeline is retained
  as the research narrative; the canonical specification governs
  implementation and evidence mapping where the two vocabularies differ.

## 2026-07-21 — Evidence and traceability infrastructure established

- `docs/evidence/CLAIMS-REGISTER.md` — 16 stable claim IDs
  (CORE-AI-7-C-001 through C-016), each rated on an E0–E6 evidence scale,
  replacing informal status words in the original evidence map.
- `docs/evidence/EVIDENCE-REGISTRY.md` — 8 evidence artifacts
  (CORE-AI-7-E-001 through E-008), each with method, environment, result,
  interpretation, and limitations.
- `docs/evidence/BENCHMARK-REGISTRY.md` — 4 benchmark entries
  (CORE-AI-7-BM-001 through BM-004), each with full workload/hardware/
  methodology context; no benchmark published as a bare number.
- `docs/implementation/RESEARCH-TO-IMPLEMENTATION-MAP.md` — 15 mappings
  from architectural requirement to implementation capability to
  validation method to evidence status.
- `docs/implementation/PRIVATE-IMPLEMENTATION-ATTESTATION.md` — states
  what the existence of a private implementation does and does not
  establish about public claims; no fabricated hashes or signatures.
- `docs/reproducibility/REPRODUCE.md` — explicit statement that
  independent reproduction has not yet been established for any claim,
  and what would be required for it to become possible.
- `docs/failures/FAILURE-CASE-INDEX.md` — 4 specific failure cases
  (CORE-AI-7-FC-001 through FC-004), distinct from the general taxonomy.
- `docs/EVIDENCE-MAP.md` reconciled to the E0–E6 scale and canonical
  layer names, retained as a high-level index pointing to the claims and
  evidence registries as the source of truth.

## No claim was strengthened during this revision

This pass audited existing published claims against their evidence and
found no claim published above its supported evidence level. Several
claims (session isolation/divergence detection at L6; context provenance
at L3; workflow recovery at L5) were made more conservative — rated E1/E2
rather than left ambiguous — where dedicated public evidence does not yet
exist. See the "Claims Downgraded or Clarified" section of the associated
audit report.

## 2026-07-21 — C-012 explicitly deprioritized

Session isolation / divergence detection (L6 Agent Coordination) was the
weakest-attested claim in scope (E1, designed only, no evidence entry).
Rather than fabricate an evidence entry to close the gap, it was moved to
an explicit "Deprioritized" section in `roadmap/README.md`, with the
reasoning stated (C-011 cascade-cancellation containment is judged the
higher-value L6 investment, since it directly addresses the
context-corruption cascade). Cross-referenced from the claims register,
implementation map, and evidence-map summary so the status is visible
everywhere it appears, not silently dropped.

## Future milestones (not yet reached)

- Independent reproduction of any claim by a third party.
- Publication of a public, runnable artifact sufficient to exercise at
  least one claim end to end.
- Production-scale validation, once laboratory-scale validation across
  the current scenario set is judged sufficiently mature.
