# Validation Methodology

This document describes how relevant builds of the private CORE-AI/7
implementation are evaluated. It is written at a public-safe abstraction
level: it names the validation chain and the categories of information
each stage produces, without disclosing private laboratory infrastructure,
hostnames, paths, scripts, or proprietary benchmark harnesses.

## Validation chain

```
TARGET SCENARIO
        ↓
CONTROLLED LABORATORY ENVIRONMENT
        ↓
DEFINED BUILD
        ↓
DEFINED WORKLOAD
        ↓
MEASUREMENT
        ↓
FAILURE CONDITION
        ↓
RECOVERY
        ↓
INTEGRITY VERIFICATION
        ↓
RESULT
```

Relevant builds are evaluated through controlled laboratory environments
designed to replicate the target scenario for that build. A scenario is not
considered validated until it has passed through the full chain — a
measurement without a defined build and workload, or a recovery claim
without an integrity check, is not published as validated.

## Stage definitions

**Target scenario.** A specific, named situation under test — e.g., a
storage-layer crash mid-write, a retrieval-quality evaluation over a fixed
corpus, a multi-agent task graph with an injected agent failure. Scenarios
are chosen to exercise a specific architectural claim from
[../EVIDENCE-MAP.md](../EVIDENCE-MAP.md).

**Controlled laboratory environment.** A defined, isolated environment
class (not a specific host or path) — e.g., "commodity CPU workstation,
single-process, local disk." Environment identity beyond its class is
private.

**Defined build.** Validation is always tied to a specific build identity
of the private implementation, not to "the system" in the abstract. Builds
are versioned; a validation result is only comparable across the same
build class.

**Defined workload.** The input scale, shape, and pattern used — e.g.,
corpus size, vector count, concurrency level, request rate — stated as a
class, not necessarily as private raw data.

**Measurement.** What is recorded: latency, recall, throughput, failure
count, hallucination rate, or similar, depending on the scenario.

**Failure condition.** Where applicable, an explicit fault is injected —
process kill mid-write, corrupted input, dependency unavailability — rather
than only observing steady-state behavior.

**Recovery.** The system's recovery procedure is exercised, not assumed;
recovery is a measured stage, not a claim taken on faith.

**Integrity verification.** After recovery, state is checked for
correctness (e.g., no partial writes, no silently corrupted index, audit
chain intact) before a result is accepted.

**Result.** The scenario's outcome, classified by the acceptance criteria
defined for it ahead of time.

## What is documented, where safe

For each validated scenario, the following categories are documented
publicly where doing so does not expose sensitive infrastructure:

- Scenario definition
- Environment class
- Build identity (version, not host)
- Workload class
- Measurement categories
- Failure categories exercised
- Recovery categories exercised
- Repetition (number of runs)
- Acceptance criteria
- Limitations specific to that scenario

## What is not disclosed

Private laboratory infrastructure, internal hostnames, machine-specific
paths, proprietary benchmark or test harness source, and confidential
configuration are never included in public validation records, even in
sanitized form. Where a result cannot be described without exposing one of
these, only the fact that validation was performed is published — see
the status classification `VALIDATION PERFORMED — DETAILED RESULTS
PRIVATE` in [../../benchmarks/README.md](../../benchmarks/README.md).

## Limitations of this methodology

- Validation is performed by the authors, not by an independent third
  party. No result in this repository should be read as independently
  reproduced.
- Validation covers a defined set of scenarios and environment classes,
  not an exhaustive fault-injection or workload space.
- A sanitized result is a summary of a private measurement, not a
  publicly re-runnable artifact.
