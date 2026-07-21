# Roadmap

Active, planned, and future research directions for CORE-AI/7. This
roadmap describes research and architecture direction — it is not a
private-implementation release schedule.

## Active research

- Retrieval semantics: moving from lexical/term-overlap retrieval toward
  semantic retrieval, and studying the effect on the context-corruption
  containment strategy in
  [docs/architecture/boundaries.md](../docs/architecture/boundaries.md).
- Recovery under higher-concurrency and higher-fault-rate conditions than
  currently characterized (see
  [docs/doctrine/limitations.md](../docs/doctrine/limitations.md)).

## Planned

- Expanding the validated environment-class matrix beyond the current
  single hardware tier.
- Expanding evaluation corpora and adversarial probe sets for the
  governance/hallucination gate (L7 Governance & Audit).
- Multi-process / multi-reader coordination research for the memory layer
  (L3 Memory & Retrieval), currently single-writer by design.
- Vector quantization and memory-constrained-corpus research for L3.

## Deprioritized

- **Session isolation / divergence detection (L6 Agent Coordination,
  [C-012](../docs/evidence/CLAIMS-REGISTER.md#core-ai-7-c-012)).**
  Currently E1 — designed only, no implementation or validation evidence
  exists. This is explicitly deprioritized relative to the items in
  Active/Planned above: cascade-cancellation containment (C-011, E3) is
  judged the higher-value coordination-layer investment right now, since
  it addresses the context-corruption cascade directly. C-012 will not
  move past E1 until it is scoped as its own work item with a defined
  validation scenario — it is listed here so its status is visible, not
  silently dropped, and so it isn't mistaken for near-term work.

## Future research directions

- Independent reproduction: what a third party would need (without access
  to the private implementation) to independently validate a CORE-AI/7
  claim, and whether a reduced public artifact could support that.
- Production-scale validation, once laboratory-scale validation across the
  current scenario set is judged sufficiently mature.
- Formalizing acceptance criteria for governance gates as the evaluation
  corpus grows, to keep the gate meaningful rather than merely permissive.

## Status discipline

Nothing on this roadmap should be read as validated or shipped until it
appears with an evidence level in
[docs/evidence/CLAIMS-REGISTER.md](../docs/evidence/CLAIMS-REGISTER.md).
