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

## Architecture

CORE-AI/7 defines seven conceptual layers, from raw compute to governed and
audited intelligence:

```
COMPUTATION
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

See [docs/architecture/system-overview.md](docs/architecture/system-overview.md)
for the full layer breakdown and [docs/architecture/architectural-principles.md](docs/architecture/architectural-principles.md)
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
higher. See [docs/EVIDENCE-MAP.md](docs/EVIDENCE-MAP.md) for the claim →
evidence → status table, and [evidence/](evidence/) for sanitized summaries.

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

## License

Documentation and research artifacts in this repository are released under
[LICENSE](LICENSE). See [SECURITY.md](SECURITY.md) for the vulnerability
reporting policy.

Copyright (c) 2026 Jerson Boyd Milan.
