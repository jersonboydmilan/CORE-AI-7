# Benchmark Registry

No benchmark in this registry is published without full context. A number
alone (e.g. "0.065 ms/query") is never treated as evidence — only a number
with its documented workload, hardware, dataset, and measurement procedure
is. Underlying evidence entries: [EVIDENCE-REGISTRY.md](EVIDENCE-REGISTRY.md).

**Reproduction status legend:** Indicative (informal, not gated) · Internal
(private CI, not independently observed) · Controlled (ran through the
full [validation methodology](../validation/VALIDATION-METHODOLOGY.md)
chain) · Reproducible (public materials sufficient for an external party
to re-run) · Independently reproduced (a third party has re-run it and
confirmed the result). All entries below are **Controlled**; none are
**Reproducible** or **Independently reproduced**.

---

## CORE-AI-7-BM-001 — Local compute substrate comparison

- **System/component.** L1 Compute & Runtime — dense matrix-multiplication
  throughput across candidate local execution substrates.
- **Hardware.** Single commodity multi-core CPU workstation (no GPU).
- **Software/build context.** Reference build; correctness gated by a
  numerical-parity check (fixed tolerance) before timing.
- **Workload.** Square dense matrices at representative training-scale
  dimensions.
- **Dataset characteristics.** Synthetic numerical arrays, not
  domain data.
- **Metric.** Throughput, relative multiplier vs. a naive interpreted
  baseline; numerical parity vs. a reference substrate.
- **Result.** The in-tree native compute path measured roughly four
  orders of magnitude faster than a naive interpreted baseline; a
  general-purpose vendored numerical library remained faster still for
  this workload class — documented as an expected tradeoff (the native
  path exists for auditability, not to outperform a mature vendored
  library).
- **Methodology.** Repeated timed runs after the parity gate; see
  [../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md).
- **Reproduction status.** Controlled.
- **Limitations.** Single hardware class; no GPU/distributed regime; no
  large-matrix regime beyond the tested dimensions.

## CORE-AI-7-BM-002 — Approximate nearest-neighbor retrieval

- **System/component.** L3 Memory & Retrieval — approximate
  nearest-neighbor index vs. exact brute-force search.
- **Hardware.** Single commodity multi-core CPU workstation.
- **Software/build context.** Reference build.
- **Workload.** Moderate-scale vector corpus, low-dimensional embeddings,
  fixed query set, swept across multiple search-effort settings.
- **Dataset characteristics.** Synthetic vector corpus at a fixed scale.
- **Metric.** Recall@10 vs. exact ground truth; per-query latency.
- **Result.** Recall approached exact-search parity at higher search
  effort; sub-millisecond per-query latency across the tested effort
  sweep at the tested corpus scale. An in-suite regression gate enforces
  a minimum recall floor on every run.
- **Methodology.** Exact brute-force search as ground truth; recall and
  latency measured at each search-effort setting.
- **Reproduction status.** Controlled.
- **Limitations.** Single corpus scale and dimensionality; no
  high-delete-fraction/compaction stress test; no multi-process
  concurrent-access test.

## CORE-AI-7-BM-003 — Offline retrieval-augmented generation pipeline

- **System/component.** L4/L5 — retrieval-augmented generation pipeline,
  end to end.
- **Hardware.** Single commodity CPU workstation, fully offline (no
  network access during the run).
- **Software/build context.** Reference build; extractive backend (not a
  live large local model) in the loop for this measurement.
- **Workload.** Small fixed local document corpus; fixed question set
  including adversarial questions with no supported answer in the corpus.
- **Dataset characteristics.** Small, fixed, checked-in evaluation
  dataset — not production-scale.
- **Metric.** Retrieval hit rate and rank quality; answer accuracy;
  pipeline failure count; hallucination rate on the adversarial subset;
  per-stage latency.
- **Result.** Retrieval hit rate and rank quality at or above the gate's
  floor; zero pipeline failures; zero hallucinated answers on the
  adversarial set; per-query latency well under the gate's ceiling
  (excluding live large-model inference, not in the loop for this run).
- **Methodology.** Deterministic evaluation harness against the
  checked-in dataset; regression gate compares results to baseline on
  every build — see
  [CORE-AI-7-E-005](EVIDENCE-REGISTRY.md#core-ai-7-e-005) for the gate
  itself.
- **Reproduction status.** Controlled.
- **Limitations.** Small fixed corpus; no live large-model backend in the
  loop; not production-scale.

## CORE-AI-7-BM-004 — Durable storage crash recovery

- **System/component.** L3 Memory & Retrieval — write-ahead-log durability
  and crash recovery.
- **Hardware.** Single commodity CPU workstation, local disk.
- **Software/build context.** Reference build.
- **Workload.** Interrupted-write and corruption fault injection during
  mutation.
- **Dataset characteristics.** Not disclosed.
- **Metric.** Not disclosed in detail.
- **Result.** `VALIDATION PERFORMED — DETAILED RESULTS PRIVATE`.
- **Methodology.** Ran through the full validation chain in
  [../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md);
  fault-injection technique withheld pending public-safety review.
- **Reproduction status.** Controlled (detail private).
- **Limitations.** Not independently reviewable in detail from this
  repository.
