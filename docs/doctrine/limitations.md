# Limitations

Stated explicitly, because an accurate limitations section increases the
credibility of the research record rather than weakening it.

## Private implementation

The reference implementation of CORE-AI/7 is not published in this
repository. A technical reader can understand the architecture, the
research questions, and the validation methodology here, but cannot build
or run the actual system from this repository alone.

## Limited public reproducibility

Because the implementation is private, claims in this repository that are
backed by evidence are backed by evidence gathered by the authors, under
the methodology in
[../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md).
A reader cannot currently re-run these scenarios themselves.

## No independent reproduction

No third party has reproduced any result described in this repository.
Every evidence entry in [../EVIDENCE-MAP.md](../EVIDENCE-MAP.md) that could
plausibly be read as "independently reproduced" is not — this is stated
explicitly to avoid any ambiguity.

## No production validation claimed

Validation described in this repository is laboratory/scenario validation
under controlled conditions, not production deployment at scale. No claim
of production validation is made anywhere in this repository.

## Hardware and environment scope

Validation performed to date has been on a bounded set of environment
classes and hardware. Behavior outside that envelope (different hardware
tiers, different failure-injection classes, different concurrency levels)
has not been characterized.

## Benchmark scope

Published benchmarks (where sanitized results exist) cover the specific
scenarios documented under [../../benchmarks/](../../benchmarks/) and
[../../evidence/](../../evidence/) — they should not be read as general
claims about performance across all workloads or hardware.

## Research-stage components

Some architectural layers are further along in validation than others.
The evidence map distinguishes designed, implemented-private,
tested-private, and scenario-validated status per claim rather than
applying one maturity level to the whole architecture.

## Summary

The strongest honest claim this repository supports is: a private
implementation exists, is exercised under a documented methodology, and
produces sanitized evidence for a defined subset of claims. Nothing beyond
that should be inferred.
