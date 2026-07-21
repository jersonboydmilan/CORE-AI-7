# Changelog

All notable changes to this repository. Format follows
[Keep a Changelog](https://keepachangelog.com/); versions follow
[Semantic Versioning](https://semver.org/). For the evolution of the
research program itself (as opposed to document changes), see
[RESEARCH-CHANGELOG.md](RESEARCH-CHANGELOG.md).

## [0.2.0] — 2026-07-21

Research traceability, evidence registry, reproducibility, and
architecture canonicalization.

### Added

- `docs/architecture/CORE-AI-7-SPECIFICATION.md` — canonical seven-layer
  architecture definition.
- `docs/architecture/ARCHITECTURE-VERSION-MATRIX.md` — architecture
  revision history.
- `docs/implementation/RESEARCH-TO-IMPLEMENTATION-MAP.md` and
  `docs/implementation/PRIVATE-IMPLEMENTATION-ATTESTATION.md`.
- `docs/evidence/CLAIMS-REGISTER.md`, `EVIDENCE-REGISTRY.md`,
  `BENCHMARK-REGISTRY.md` — 16 claims, 8 evidence artifacts, 4
  benchmarks, all on a shared E0–E6 evidence scale.
- `docs/reproducibility/REPRODUCE.md`.
- `docs/failures/FAILURE-CASE-INDEX.md` — 4 specific investigated cases.
- `docs/RESEARCH-STATUS.md` maturity model (added same day as 0.1.0,
  cross-linked here for completeness).
- `RESEARCH-CHANGELOG.md`.
- Index README files for the new `docs/evidence/`,
  `docs/implementation/`, `docs/reproducibility/`, and `docs/failures/`
  directories.

### Changed

- `docs/EVIDENCE-MAP.md` reconciled from an informal status vocabulary to
  the E0–E6 scale and canonical layer names; retained as a one-page
  summary pointing to the claims/evidence registries as source of truth.
- Renamed layers L2 (Embeddings → Knowledge & Data), L3 (Memory & Context
  Management → Memory & Retrieval), L4 (Primitives/Reasoning →
  Reasoning), L6 (Coordination → Agent Coordination) across README and
  `docs/architecture/`. Layer numbers unchanged.
- Made recovery an explicit cross-cutting model in the canonical
  specification instead of an implicit property.
- README restructured with a Research Traceability section linking every
  new registry/index document.
- `docs/doctrine/research-thesis.md` — added an explicit reconciliation
  note between the 9-stage research pipeline and the canonical
  specification.
- `benchmarks/README.md` cross-linked to `BENCHMARK-REGISTRY.md`; one
  overclaimed limitation ("validated functionally") downgraded to match
  the honest E1 status recorded in the new failure case index.
- `evidence/validation-records/README.md`, `evidence/test-summaries/README.md`,
  `evidence/benchmark-summaries/README.md` cross-linked to the new
  registries with stable claim/evidence IDs.

## [0.1.0] — 2026-07-21

Initial public research record.

### Added

- README with thesis, architecture summary, research areas, validation
  approach, current status, limitations, and roadmap.
- Architecture documentation: system overview, architectural principles,
  layer boundaries.
- Research doctrine: research thesis, research questions, limitations.
- Public technical specifications.
- Validation methodology.
- Evidence map (claim → design → evidence category → status).
- Sanitized benchmark entries and evidence summaries.
- Failure taxonomy.
- Seven architecture decision records (ADR-001 through ADR-007).
- Public/private boundary policy.
- Roadmap.
