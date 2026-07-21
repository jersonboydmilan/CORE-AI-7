# Evidence Registry

Every evidence artifact backing a claim in
[CLAIMS-REGISTER.md](CLAIMS-REGISTER.md). Performance-bearing entries also
appear, with full methodology context, in
[BENCHMARK-REGISTRY.md](BENCHMARK-REGISTRY.md).

---

## CORE-AI-7-E-001

**Claim supported.** [CORE-AI-7-C-002](CLAIMS-REGISTER.md#core-ai-7-c-002).
**Method.** Local compute-substrate comparison: dense matrix-multiplication
throughput and numerical-parity check across candidate local execution
paths, plus functional check that the local inference backend runs as an
in-process/local-subprocess call with no network socket opened.
**Environment.** Commodity multi-core CPU workstation, single process, no
GPU. See [BENCHMARK-REGISTRY.md#core-ai-7-bm-001](BENCHMARK-REGISTRY.md#core-ai-7-bm-001)
for full detail.
**Result.** Native local-compute path measured functionally correct
(numerical parity within a fixed tolerance vs. a reference substrate) and
substantially faster than a naive interpreted baseline; see benchmark
entry for the full comparison table.
**Interpretation.** Demonstrates a working local compute substrate exists
and is measured, not merely designed.
**Limitations.** Single hardware class; no GPU or distributed regime
tested.
**Evidence status.** E3.

## CORE-AI-7-E-002

**Claim supported.** [CORE-AI-7-C-006](CLAIMS-REGISTER.md#core-ai-7-c-006).
**Method.** Recall@10 and per-query latency of the approximate
nearest-neighbor index vs. exact brute-force search, swept across
search-effort settings, with an in-suite regression floor on minimum
recall.
**Environment.** Commodity multi-core CPU workstation. See
[BENCHMARK-REGISTRY.md#core-ai-7-bm-002](BENCHMARK-REGISTRY.md#core-ai-7-bm-002).
**Result.** Recall approached exact-search parity at higher search
effort; sub-millisecond per-query latency at the tested corpus scale.
**Interpretation.** Retrieval integrity (accuracy vs. exact ground truth)
is measured, not assumed, at the tested scale.
**Limitations.** Single corpus scale/dimensionality; no high
delete-fraction/compaction stress test included.
**Evidence status.** E3.

## CORE-AI-7-E-003

**Claim supported.** [CORE-AI-7-C-009](CLAIMS-REGISTER.md#core-ai-7-c-009),
[CORE-AI-7-C-003](CLAIMS-REGISTER.md#core-ai-7-c-003).
**Method.** End-to-end retrieval and answer-quality evaluation over a
fixed local document corpus, including an adversarial hallucination probe
set with no supported answer in the corpus, run fully offline.
**Environment.** Commodity CPU workstation, no network access during the
run. See [BENCHMARK-REGISTRY.md#core-ai-7-bm-003](BENCHMARK-REGISTRY.md#core-ai-7-bm-003).
**Result.** Retrieval hit rate and rank quality at or above the gate
floor; zero pipeline failures; zero hallucinated answers on the
adversarial set; low measured stage latency (extractive backend, not a
live large local model, in the loop).
**Interpretation.** The offline pipeline is functionally correct and
measurably grounded on the tested corpus and probe set.
**Limitations.** Small fixed corpus and question set; results with a live
local large-model backend are not covered.
**Evidence status.** E3.

## CORE-AI-7-E-004

**Claim supported.** [CORE-AI-7-C-005](CLAIMS-REGISTER.md#core-ai-7-c-005).
**Method.** Fault-injection scenario validation of the durable-storage
write-ahead-log recovery path: interrupted-write and corruption recovery
under the full validation chain in
[../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md).
**Environment.** Commodity CPU workstation, local disk.
**Result.** `VALIDATION PERFORMED — DETAILED RESULTS PRIVATE`. Fault
technique and pass/fail counts are withheld pending public-safety review.
**Interpretation.** Confirms the scenario was run through the full chain
(scenario → build → workload → measurement → failure → recovery →
integrity verification → result), without disclosing implementation
detail that could expose the fault-injection mechanism.
**Limitations.** Not independently reviewable in detail from this
repository alone.
**Evidence status.** E3.

## CORE-AI-7-E-005

**Claim supported.** [CORE-AI-7-C-015](CLAIMS-REGISTER.md#core-ai-7-c-015).
**Method.** Automated regression gate run against a checked-in quality
baseline on each reference build, covering retrieval, generation-quality,
and failure-count checks.
**Environment.** Same as [E-003](#core-ai-7-e-003).
**Result.** All checks passed against the checked-in baseline for the
reference build evaluated.
**Interpretation.** The private implementation has a working,
automatically-enforced quality floor, not just a one-time measurement.
**Limitations.** Baseline and thresholds are privately defined; not
independently set or reviewed.
**Evidence status.** E3.

## CORE-AI-7-E-006

**Claim supported.** [CORE-AI-7-C-001](CLAIMS-REGISTER.md#core-ai-7-c-001),
[CORE-AI-7-C-004](CLAIMS-REGISTER.md#core-ai-7-c-004).
**Method.** (a) Dependency-surface audit of the private implementation's
package manifest against the "no required outbound network dependency"
policy. (b) Internal unit-test suite covering tokenizer/embedding
round-trip correctness and gradient/numerical correctness of reasoning
primitives, checked against numerical differentiation.
**Environment.** Private CI / local test run.
**Result.** Dependency manifest contained no networked-service client
dependency at audit time; unit-test suite passed.
**Interpretation.** Both the sovereignty policy and basic representation
correctness are enforced by an automated, repeatable check rather than
manual review alone.
**Limitations.** Point-in-time audit; not continuously and publicly
monitored. Unit-test evidence is internal only.
**Evidence status.** E3.

## CORE-AI-7-E-007

**Claim supported.** [CORE-AI-7-C-011](CLAIMS-REGISTER.md#core-ai-7-c-011).
**Method.** Scenario test suite: multi-agent task graph with an injected
task failure, verifying that cancellation cascades only to the failed
task's dependents and reaches a fixpoint, rather than affecting unrelated
tasks.
**Environment.** Private CI / local test run.
**Result.** Cascade cancellation contained to dependents in the tested
scenarios; unrelated tasks completed normally.
**Interpretation.** Failure containment at the coordination layer is
exercised, not just claimed by design.
**Limitations.** Tested at small/moderate graph scale; large-graph and
adversarial-agent scenarios not covered.
**Evidence status.** E3.

## CORE-AI-7-E-008

**Claim supported.** [CORE-AI-7-C-013](CLAIMS-REGISTER.md#core-ai-7-c-013).
**Method.** Adversarial evaluation set specifically constructed to probe
for hallucination and ungrounded output, run through the governance
evaluation gate before results are accepted.
**Environment.** Same as [E-003](#core-ai-7-e-003).
**Result.** Zero hallucinated answers on the tested adversarial set for
the reference build evaluated (see [E-003](#core-ai-7-e-003) for the
combined pipeline result).
**Interpretation.** The governance gate is exercised against a specific
adversarial probe set, not evaluated only on well-formed happy-path
inputs.
**Limitations.** Adversarial set size and construction are private; not
independently reviewed or expanded by a third party.
**Evidence status.** E3.
