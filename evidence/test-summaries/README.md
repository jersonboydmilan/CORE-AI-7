# Test Summaries

Sanitized summary of automated testing performed against the private
implementation. Detailed test source, fixtures, and CI configuration
remain private.

| Category | Summary |
|---|---|
| Unit-level correctness (primitives, reasoning components) | Passing test suite; gradient/numerical correctness checks included. |
| Systems-level correctness (storage engine) | Passing test suite; crash/recovery simulations included. |
| Concurrency and causality properties | Exercised under the private test suite. |
| Static analysis / lint / type-checking gates | Enforced clean on every change as a merge gate. |

No raw counts, file lists, or CI configuration are published here to avoid
implying a level of public reproducibility that does not exist — see
[../../docs/doctrine/limitations.md](../../docs/doctrine/limitations.md).
Where a specific count is safe to publish, it appears in
[../../benchmarks/README.md](../../benchmarks/README.md) with full
methodology context rather than as an isolated number.
