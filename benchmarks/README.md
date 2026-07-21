# Benchmarks

**Canonical registry:** [docs/evidence/BENCHMARK-REGISTRY.md](../docs/evidence/BENCHMARK-REGISTRY.md)
carries the same entries with stable benchmark IDs (BM-001–BM-004) and is
the version to cite. This page is the narrative/human-readable form.

Every public benchmark entry follows this template:

```text
Scenario
Build Identifier
Environment Class
Workload Class
Metric
Measurement Method
Number of Runs
Result
Limitations
```

No result is published without this context, and no isolated number is
published without a methodology behind it — see
[../docs/validation/VALIDATION-METHODOLOGY.md](../docs/validation/VALIDATION-METHODOLOGY.md).
No result is fabricated; where a result is not safe for public release in
detail, the entry states only:

```text
VALIDATION PERFORMED — DETAILED RESULTS PRIVATE
```

## Sanitized results

### Local compute substrate comparison (L1) — [BM-001](../docs/evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-001)

- **Scenario:** dense matrix multiplication throughput across candidate
  local compute substrates.
- **Build identifier:** v1.0.x reference build.
- **Environment class:** commodity multi-core CPU workstation, single
  process, no GPU.
- **Workload class:** square dense matrices, representative training-scale
  dimensions.
- **Metric:** throughput (relative multiplier vs. a naive interpreted
  baseline) and correctness (numerical parity vs. a reference substrate,
  fixed tolerance).
- **Measurement method:** repeated timed runs after a numerical-parity
  gate; see methodology doc for repetition and acceptance criteria.
- **Result:** the in-tree native compute path measured roughly four orders
  of magnitude faster than a naive interpreted baseline, while a
  general-purpose vendored numerical library remained the faster option
  for this workload class — a documented, expected tradeoff (the native
  path exists for auditability, not to outperform a mature vendored
  library).
- **Limitations:** single hardware class tested; large-matrix, GPU, and
  distributed regimes not covered.

### Approximate nearest-neighbor retrieval (L3) — [BM-002](../docs/evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-002)

- **Scenario:** recall and latency of the from-scratch approximate
  retrieval index vs. exact brute-force search, at fixed corpus size.
- **Build identifier:** v1.0.x reference build.
- **Environment class:** commodity multi-core CPU workstation.
- **Workload class:** moderate-scale vector corpus, low-dimensional
  embeddings, fixed query set.
- **Metric:** recall@10 vs. exact ground truth, and per-query latency, at
  multiple search-effort settings.
- **Measurement method:** exact brute-force search as ground truth;
  recall/latency measured across a sweep of search-effort parameters; an
  in-suite regression gate enforces a minimum recall floor.
- **Result:** recall approached exact-search parity at higher search
  effort, with a measured latency/recall tradeoff across the effort sweep;
  the index sustained sub-millisecond query latency at the tested corpus
  scale.
- **Limitations:** single corpus scale and dimensionality tested; recall
  behavior under index compaction and high delete fraction is an
  acknowledged architectural tradeoff, not yet scenario-validated or
  benchmarked — see
  [docs/failures/FAILURE-CASE-INDEX.md#core-ai-7-fc-004](../docs/failures/FAILURE-CASE-INDEX.md#core-ai-7-fc-004).

### Offline retrieval-augmented generation pipeline (L4/L5) — [BM-003](../docs/evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-003)

- **Scenario:** end-to-end retrieval and answer-quality evaluation over a
  fixed local document corpus, including an adversarial hallucination
  probe set.
- **Build identifier:** v1.0.x reference build.
- **Environment class:** commodity CPU workstation, fully offline, no
  network access during the run.
- **Workload class:** small fixed corpus, fixed question set, including
  adversarial questions with no supported answer in the corpus.
- **Metric:** retrieval hit rate and rank quality, answer accuracy,
  failure count, hallucination rate on the adversarial set, and stage
  latency.
- **Measurement method:** deterministic evaluation harness run against a
  checked-in dataset; a regression gate compares results to a baseline on
  every build.
- **Result:** retrieval hit rate and rank quality were at or above the
  gate's floor, zero pipeline failures, zero hallucinated answers on the
  adversarial set, and per-query latency well under the gate's ceiling
  (excluding live large-model inference, which was not in the loop for
  this run).
- **Limitations:** small fixed corpus; a production-scale corpus and a
  live local inference backend in the loop are not covered by this run.

### Durable storage crash recovery (L3) — [BM-004](../docs/evidence/BENCHMARK-REGISTRY.md#core-ai-7-bm-004)

- **Scenario:** interrupted-write and corruption recovery under the
  write-ahead-log durability mechanism.
- **Build identifier:** v1.0.x reference build.
- **Environment class:** commodity CPU workstation, local disk.
- **Result:** `VALIDATION PERFORMED — DETAILED RESULTS PRIVATE`.
- **Limitations:** fault-injection technique and detailed pass/fail
  counts are withheld pending public-safety review; methodology category
  is documented in
  [../docs/validation/VALIDATION-METHODOLOGY.md](../docs/validation/VALIDATION-METHODOLOGY.md)
  and [../docs/failure-research/failure-taxonomy.md](../docs/failure-research/failure-taxonomy.md).

## Methodology and raw materials

- [methodology/](methodology/) — scenario definitions referenced above.
- [results/](results/) — reserved for future sanitized result artifacts.
