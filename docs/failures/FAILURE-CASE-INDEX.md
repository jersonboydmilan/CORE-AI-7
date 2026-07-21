# Failure Case Index

Specific investigated failure cases, distinct from the general categories
in [../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md).
Each case follows: failure → observation → root cause → architectural
response → controlled validation → evidence → remaining limitations. No
sensitive operational detail (fault-injection technique, infrastructure,
timing) is published where it would expose the private implementation
beyond what is already disclosed in the evidence registry.

---

## CORE-AI-7-FC-001 — Interrupted write during durable-storage mutation

**Affected layer.** L3 — Memory & Retrieval.
**Initial condition.** A mutation (insert/update/delete) is in flight
against the durable storage engine.
**Observed failure.** Process termination mid-write, before the mutation
is acknowledged as durable.
**Impact.** Risk of a torn or partially-applied record on disk if not
handled.
**Root cause.** Structural — any storage engine without an explicit
durability boundary is exposed to this class; not a defect discovered in
a specific incident.
**Architectural response.** Acknowledge a mutation as durable only after
it is fsynced; recovery on restart accepts exactly the clean, committed
prefix of records and truncates any torn tail.
**Controlled validation.** Fault-injection scenario run through the full
validation chain; see
[../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-004](../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-004).
**Evidence level.** E3. Detailed results private.
**Remaining uncertainty.** Fault classes outside the tested injection set
are not characterized; behavior under concurrent multi-writer access is
out of scope (single-writer by design).

## CORE-AI-7-FC-002 — Single agent failure in a multi-agent task graph

**Affected layer.** L6 — Agent Coordination.
**Initial condition.** A multi-agent task graph is executing with tasks
depending on one another.
**Observed failure.** One task raises an unrecoverable error.
**Impact.** Without containment, failure could propagate to unrelated
tasks or leave the graph in an inconsistent state.
**Root cause.** Structural — any dependency-graph scheduler needs an
explicit containment policy or failure propagates by default through
shared execution state.
**Architectural response.** Acyclic-by-construction task submission
(a task may only depend on already-submitted tasks) plus cascade
cancellation: failure cancels only the failed task's dependents, to a
fixpoint, leaving independent branches of the graph to complete.
**Controlled validation.** Scenario test suite with an injected task
failure; see
[../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-007](../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-007).
**Evidence level.** E3.
**Remaining uncertainty.** Tested at small/moderate graph scale only;
behavior under adversarial or Byzantine agent behavior (an agent that
fails in a misleading rather than an honest way) is not characterized.

## CORE-AI-7-FC-003 — Ungrounded generation on an unanswerable question

**Affected layer.** L4/L7 — Reasoning; Governance & Audit.
**Initial condition.** A question is posed for which the local corpus
contains no supporting answer.
**Observed failure.** Risk of the reasoning stage generating a plausible
but ungrounded (hallucinated) answer instead of declining to answer.
**Impact.** A hallucinated answer presented with the same apparent
authority as a grounded one is the entry point for the context-corruption
cascade described in
[../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md).
**Root cause.** Structural — retrieval-augmented generation has no
inherent mechanism to distinguish "no evidence found" from "evidence
found but weak" unless explicitly evaluated.
**Architectural response.** A dedicated adversarial evaluation set
(questions with no supported answer in the corpus) is run through the
governance gate before results are accepted as grounded.
**Controlled validation.** Adversarial hallucination-rate evaluation; see
[../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-008](../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-008).
**Evidence level.** E3.
**Remaining uncertainty.** Adversarial set size and construction are
private and self-defined; behavior with a live large local model (rather
than the extractive backend used for this measurement) is not yet
covered.

## CORE-AI-7-FC-004 — Retrieval-recall degradation under heavy deletion

**Affected layer.** L3 — Memory & Retrieval.
**Initial condition.** A large fraction of a vector index's entries are
deleted between compaction cycles.
**Observed failure.** This is a known, deliberate architectural tradeoff
identified during design, not an incident discovered in production — the
approximate retrieval index used has no cheap in-place delete/unlink
operation.
**Impact.** Tombstone-filtered search recall can degrade as the deleted
fraction grows, until the next compaction rebuilds a clean index.
**Root cause.** Structural, by design choice: tombstone deletes were
chosen over unlink-based deletes because the underlying index structure
has no cheap unlink; see
[../doctrine/limitations.md](../doctrine/limitations.md).
**Architectural response.** Tombstone deletes with periodic compaction;
the tradeoff is stated explicitly rather than hidden.
**Controlled validation.** Not separately benchmarked at high
delete-fraction; recall is measured at zero-deletion baseline only (see
[../evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-002](../evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-002)).
**Evidence level.** E1 — designed and acknowledged; not scenario-validated
under a high delete-fraction workload.
**Remaining uncertainty.** The actual recall-degradation curve as a
function of delete fraction has not been measured and is not claimed
here.
