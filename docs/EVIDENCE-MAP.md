# Evidence Map

**This is a high-level index.** The source of truth for individual claims
is [evidence/CLAIMS-REGISTER.md](evidence/CLAIMS-REGISTER.md); underlying
evidence is [evidence/EVIDENCE-REGISTRY.md](evidence/EVIDENCE-REGISTRY.md)
and [evidence/BENCHMARK-REGISTRY.md](evidence/BENCHMARK-REGISTRY.md). This
page summarizes those registries against the canonical layer model in
[architecture/CORE-AI-7-SPECIFICATION.md](architecture/CORE-AI-7-SPECIFICATION.md).

## Evidence level scale (E0–E6)

This repository previously used an informal status vocabulary
(`DOCUMENTED`, `IMPLEMENTED — PRIVATE`, `SCENARIO-VALIDATED`, etc.). That
vocabulary has been superseded by the E0–E6 scale used throughout the
claims and evidence registries, to keep one consistent maturity scale
across the repository:

| Level | Name |
|---|---|
| E0 | Conceptual |
| E1 | Designed |
| E2 | Implemented |
| E3 | Internally validated |
| E4 | Publicly reproducible |
| E5 | Independently validated |
| E6 | Production validated |

No claim in this repository is currently above **E3**.

## Claim summary

| Claim ID | Layer | Claim | Status |
|---|---|---|---|
| [C-001](evidence/CLAIMS-REGISTER.md#core-ai-7-c-001) | L1 | No required outbound network dependency for core execution | E3 |
| [C-002](evidence/CLAIMS-REGISTER.md#core-ai-7-c-002) | L1 | Local model inference, no cloud inference path | E3 |
| [C-003](evidence/CLAIMS-REGISTER.md#core-ai-7-c-003) | L2 | Knowledge/data locality — local ingestion and embedding | E3 |
| [C-004](evidence/CLAIMS-REGISTER.md#core-ai-7-c-004) | L2 | Round-trip correct, deterministic tokenization/embedding | E3 |
| [C-005](evidence/CLAIMS-REGISTER.md#core-ai-7-c-005) | L3 | Crash-safe durable memory with defined recovery | E3 (detail private) |
| [C-006](evidence/CLAIMS-REGISTER.md#core-ai-7-c-006) | L3 | Approximate retrieval recall vs. exact ground truth | E3 |
| [C-007](evidence/CLAIMS-REGISTER.md#core-ai-7-c-007) | L3 | Context-assembly provenance recording | E2 |
| [C-008](evidence/CLAIMS-REGISTER.md#core-ai-7-c-008) | L4 | Reasoning treats context as untrusted, no remote model dependency | E2 |
| [C-009](evidence/CLAIMS-REGISTER.md#core-ai-7-c-009) | L4/L5 | Grounded generation, zero hallucination on adversarial probe set | E3 |
| [C-010](evidence/CLAIMS-REGISTER.md#core-ai-7-c-010) | L5 | Workflow recovery — retry/backoff, failure escalation | E2 |
| [C-011](evidence/CLAIMS-REGISTER.md#core-ai-7-c-011) | L6 | Acyclic task graphs, cascade-cancellation containment | E3 |
| [C-012](evidence/CLAIMS-REGISTER.md#core-ai-7-c-012) | L6 | Session isolation and divergence detection | E1 |
| [C-013](evidence/CLAIMS-REGISTER.md#core-ai-7-c-013) | L7 | Governance gate before persistence/surfacing | E3 |
| [C-014](evidence/CLAIMS-REGISTER.md#core-ai-7-c-014) | L7 | Tamper-evident hash-chained audit logging | E3 |
| [C-015](evidence/CLAIMS-REGISTER.md#core-ai-7-c-015) | L7 | Regression gate vs. checked-in baseline | E3 |
| [C-016](evidence/CLAIMS-REGISTER.md#core-ai-7-c-016) | Cross-cutting | Recovery addressed per layer | E2 (varies) |
| — | — | Independent third-party reproduction of any claim above | Not established |
| — | — | Production-scale deployment validation | Not established |

## How to read this table

- Layer letters (L1–L7) follow the canonical specification, not the
  original informal naming — see
  [architecture/ARCHITECTURE-VERSION-MATRIX.md](architecture/ARCHITECTURE-VERSION-MATRIX.md)
  for what changed.
- `IMPLEMENTED — PRIVATE` / `TESTED — PRIVATE` from the prior vocabulary
  map to E2/E3 respectively and are never treated as equivalent to E4
  (publicly reproducible).
- Detail on methodology, limitations, and what each claim does *not*
  establish lives in the claims register, not here — this page is
  intentionally a summary.
