# Research-to-Implementation Map

Connects CORE-AI/7 principle → architectural requirement → implementation
capability → private implementation location (neutral reference only) →
validation method → public evidence → evidence status. Full claim detail:
[../evidence/CLAIMS-REGISTER.md](../evidence/CLAIMS-REGISTER.md).

| ID | Layer | Architectural Requirement | Implementation Capability | Validation Method | Public Evidence | Status |
|---|---|---|---|---|---|---|
| M-01 | L1 | Local compute sovereignty — no required outbound network dependency for core execution | Private implementation; local execution substrate + local inference backend | Dependency-surface audit | [Claim C-001](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-001) | E3 — internally validated |
| M-02 | L1 | Local model execution | Private reference build; local inference runtime | Controlled laboratory environment, benchmark | [Claim C-002](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-002), [BM-001](../evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-001) | E3 |
| M-03 | L2 | Knowledge/data locality — local ingestion, chunking, embedding generation | Private reference build; local ingestion pipeline | Sanitized validation summary | [Claim C-003](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-003) | E3 |
| M-04 | L2 | Representation correctness — deterministic, round-trip tokenization/embedding | Private reference build; unit-tested representation module | Internal unit-test suite | [Claim C-004](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-004) | E3 |
| M-05 | L3 | Memory durability — crash-safe persistence with defined recovery | Private reference build; durable storage engine | Controlled laboratory environment, fault injection | [Claim C-005](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-005), [BM-004](../evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-004) | E3 (detail private) |
| M-06 | L3 | Retrieval integrity — measured accuracy vs. exact ground truth | Private reference build; approximate retrieval index | Controlled laboratory environment, benchmark | [Claim C-006](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-006), [BM-002](../evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-002) | E3 |
| M-07 | L3 | Context provenance at assembly time | Private reference build; context-assembly component | Design specification | [Claim C-007](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-007) | E2 — implemented, not separately validated |
| M-08 | L4 | Reasoning isolation — context treated as untrusted input, no remote model dependency | Private reference build; local reasoning/inference interface | Design specification | [Claim C-008](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-008) | E2 |
| M-09 | L4/L5 | Grounded generation, low hallucination rate on adversarial probes | Private reference build; RAG pipeline | Controlled laboratory environment, adversarial evaluation | [Claim C-009](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-009), [BM-003](../evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-003) | E3 |
| M-10 | L5 | Workflow recovery — retry/backoff and failure escalation | Private reference build; orchestration layer | Design specification | [Claim C-010](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-010) | E2 |
| M-11 | L6 | Agent coordination — acyclic task graphs, cascade-cancellation failure containment | Private reference build; scheduler/coordination component | Controlled laboratory environment, scenario test | [Claim C-011](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-011), [E-007](../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-007) | E3 |
| M-12 | L6 | Session isolation and divergence detection between agents | Not yet documented | Not yet documented | [Claim C-012](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-012) | E1 — designed only |
| M-13 | L7 | Governance enforcement — output gated before persistence/surfacing | Private reference build; evaluation gate | Controlled laboratory environment, adversarial evaluation | [Claim C-013](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-013), [E-008](../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-008) | E3 |
| M-14 | L7 | Auditability — tamper-evident, hash-chained decision/mutation logging | Private reference build; audit logging component | Structural verification test | [Claim C-014](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-014) | E3 |
| M-15 | Cross-cutting | Recovery — per-layer recovery behavior, not a single bolted-on subsystem | Private reference build; per-layer recovery mechanisms | Varies by layer — see [CORE-AI-7-SPECIFICATION.md#recovery-model](../architecture/CORE-AI-7-SPECIFICATION.md#recovery-model) | [Claim C-016](../evidence/CLAIMS-REGISTER.md#core-ai-7-c-016) | E2 (varies by layer, E3 for L3/L6) |

## Reading this table

- "Private implementation location" is intentionally neutral — no file
  paths, module names, or repository URLs are given. See
  [PRIVATE-IMPLEMENTATION-ATTESTATION.md](PRIVATE-IMPLEMENTATION-ATTESTATION.md).
- Status uses the same E0–E6 scale as
  [../evidence/CLAIMS-REGISTER.md](../evidence/CLAIMS-REGISTER.md). No row
  above E3.
- A row with "Not yet documented" is an honest gap, not a placeholder for
  a claim that will be upgraded without new evidence.
