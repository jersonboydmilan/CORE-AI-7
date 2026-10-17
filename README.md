# CORE-AI/7

Sovereign intelligence architecture, research, and validation framework.

**Author:** Jerson Boyd Milan
**Website:** [www.jersonboydmilan.com](https://www.jersonboydmilan.com)

---

## Overview

CORE-AI/7 is an independent research and engineering program investigating
sovereign intelligence architecture through first-principles system design,
controlled scenario-replicated validation, and explicit failure analysis.

This repository is the **public research record** for CORE-AI/7. It is not
the private implementation repository, and it does not contain source code.
It contains the architectural thesis, the seven-layer reference design, the
research questions the program investigates, the methodology used to
validate the private implementation, sanitized evidence, failure taxonomy,
architecture decision records, known limitations, and the research roadmap.

## Research Traceability

This repository records the relationship between:

```
RESEARCH THESIS → ARCHITECTURE → IMPLEMENTATION REQUIREMENTS →
PRIVATE IMPLEMENTATION → CONTROLLED VALIDATION → EVIDENCE →
LIMITATIONS → FUTURE REPRODUCTION
```

Every public claim carries a stable ID and an evidence level (E0–E6); no
claim is published above the level its evidence actually supports.

| Document | Purpose |
|---|---|
| [docs/architecture/CORE-AI-7-SPECIFICATION.md](docs/architecture/CORE-AI-7-SPECIFICATION.md) | Canonical seven-layer architecture |
| [docs/implementation/RESEARCH-TO-IMPLEMENTATION-MAP.md](docs/implementation/RESEARCH-TO-IMPLEMENTATION-MAP.md) | Requirement → capability → validation → evidence |
| [docs/evidence/CLAIMS-REGISTER.md](docs/evidence/CLAIMS-REGISTER.md) | Every public claim, rated E0–E6 |
| [docs/evidence/EVIDENCE-REGISTRY.md](docs/evidence/EVIDENCE-REGISTRY.md) | Evidence artifacts behind each claim |
| [docs/evidence/BENCHMARK-REGISTRY.md](docs/evidence/BENCHMARK-REGISTRY.md) | Performance results with full methodology context |
| [docs/reproducibility/REPRODUCE.md](docs/reproducibility/REPRODUCE.md) | What is and isn't reproducible today |
| [docs/failures/FAILURE-CASE-INDEX.md](docs/failures/FAILURE-CASE-INDEX.md) | Specific investigated failure cases |
| [docs/implementation/PRIVATE-IMPLEMENTATION-ATTESTATION.md](docs/implementation/PRIVATE-IMPLEMENTATION-ATTESTATION.md) | What the private implementation's existence does and does not establish |

**The implementation repository is private.** Independent reproduction of
any claim in this repository has not yet been established — see
[docs/reproducibility/REPRODUCE.md](docs/reproducibility/REPRODUCE.md).

## The Problem

Modern AI applications are typically assembled from opaque, remotely-hosted
dependencies: a training framework here, a hosted vector database there, an
inference API somewhere else. Each dependency is a point where control,
inspectability, and availability are handed to a third party. CORE-AI/7
investigates what changes — architecturally — when a system is required to
run under local control, with every layer reviewable and every failure mode
explicit, instead of assuming a network is always present and always
trustworthy.

## Core Thesis

Intelligence systems should be designed as controllable, inspectable,
resilient, and locally sovereign infrastructure — not merely as thin
interfaces over a remote model API. Sovereignty, in this sense, is an
architectural property that must be designed in at every layer:

```
AI MODEL
    ↓
CONTEXT
    ↓
MEMORY
    ↓
RETRIEVAL
    ↓
REASONING
    ↓
AGENTS
    ↓
GOVERNANCE
    ↓
AUDIT
    ↓
RECOVERY
```

This pipeline is the research narrative — *why* each concern matters. The
canonical, versioned architecture that governs implementation and evidence
mapping is the seven-layer model below; see
[docs/architecture/CORE-AI-7-SPECIFICATION.md](docs/architecture/CORE-AI-7-SPECIFICATION.md#relationship-to-the-research-thesis)
for how the two relate.

## Architecture

CORE-AI/7 defines seven layers, from local compute to governed and audited
intelligence, plus recovery as a cross-cutting property of every layer
rather than an eighth layer:

```
L1  COMPUTE & RUNTIME
    ↓
L2  KNOWLEDGE & DATA
    ↓
L3  MEMORY & RETRIEVAL
    ↓
L4  REASONING
    ↓
L5  ORCHESTRATION
    ↓
L6  AGENT COORDINATION
    ↓
L7  GOVERNANCE & AUDIT
```

Canonical definition, full scope per layer, and the recovery model:
[docs/architecture/CORE-AI-7-SPECIFICATION.md](docs/architecture/CORE-AI-7-SPECIFICATION.md).
See also [docs/architecture/system-overview.md](docs/architecture/system-overview.md)
and [docs/architecture/architectural-principles.md](docs/architecture/architectural-principles.md)
for the design principles behind it.

## Research Areas

- Sovereignty as an architectural property
- System and decision inspectability
- Memory integrity under adversarial and corrupted input
- Retrieval trust and context-corruption resistance
- Failure detection, isolation, and recovery
- Governance and policy enforcement as a runtime concern
- Auditability and tamper-evidence
- Reproducibility of controlled validation scenarios

Full research doctrine: [docs/doctrine/research-thesis.md](docs/doctrine/research-thesis.md)
and [docs/doctrine/research-questions.md](docs/doctrine/research-questions.md).

## Validation Approach

Relevant builds of the private implementation are evaluated through
controlled laboratory environments designed to replicate a target scenario,
under a defined build, a defined workload, explicit measurement, and (where
applicable) an injected failure condition followed by recovery and integrity
verification. Full methodology:
[docs/validation/VALIDATION-METHODOLOGY.md](docs/validation/VALIDATION-METHODOLOGY.md).

## Evidence

Evidence is published at the strongest level actually supported — never
higher. See [docs/evidence/CLAIMS-REGISTER.md](docs/evidence/CLAIMS-REGISTER.md)
for every claim rated E0–E6, [docs/evidence/EVIDENCE-REGISTRY.md](docs/evidence/EVIDENCE-REGISTRY.md)
and [docs/evidence/BENCHMARK-REGISTRY.md](docs/evidence/BENCHMARK-REGISTRY.md)
for the artifacts behind them, [docs/EVIDENCE-MAP.md](docs/EVIDENCE-MAP.md)
for a one-page summary, and [evidence/](evidence/) for sanitized summaries.

## Current Status

At-a-glance maturity model: [docs/RESEARCH-STATUS.md](docs/RESEARCH-STATUS.md).

| Area | Public Status | Evidence |
|---|---|---|
| Architecture | Documented | Public specification |
| Core implementation | Private | Private repository |
| Automated testing | Performed privately | Sanitized summary |
| Failure testing | Performed | Public methodology |
| Benchmarking | Performed | Sanitized summary |
| Scenario validation | Performed where documented | Validation methodology |
| Independent reproduction | Not yet claimed | Not established |
| Production validation | Not claimed | Not established |

## Limitations

The private implementation is not publicly reproducible from this
repository, and no independent third party has yet reproduced any reported
result. See [docs/doctrine/limitations.md](docs/doctrine/limitations.md)
for the full accounting.

## Roadmap

Active and planned research directions: [roadmap/README.md](roadmap/README.md).
Evolution of the research program itself (distinct from document changes):
[RESEARCH-CHANGELOG.md](RESEARCH-CHANGELOG.md).

## Public / Private Boundary

This repository intentionally excludes source code, infrastructure, and
sensitive testing material. See
[docs/PUBLIC-PRIVATE-BOUNDARY.md](docs/PUBLIC-PRIVATE-BOUNDARY.md) for the
explicit publication policy.

## Research Position

CORE-AI/7 is an independent sovereign intelligence architecture research
program whose architectural thesis is connected to a private
implementation, controlled scenario-replicated validation, and explicit
evidence. This repository exposes the research and evidence necessary for
technical understanding without exposing the private implementation or
sensitive infrastructure.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=jersonboydmilan/CORE-AI-7&type=Date)](https://star-history.com/#jersonboydmilan/CORE-AI-7&Date)

## License

Documentation and research artifacts in this repository are released under
[LICENSE](LICENSE). See [SECURITY.md](SECURITY.md) for the vulnerability
reporting policy.

Copyright (c) 2026 Jerson Boyd Milan.
