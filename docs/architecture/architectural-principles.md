# Architectural Principles

Each principle below is a design commitment. The **Evidence class** line
states, honestly, whether the principle is currently a design intent or has
supporting empirical evidence — see
[../EVIDENCE-MAP.md](../EVIDENCE-MAP.md) for the full claim table.

## Sovereignty as an architectural property

Local control over compute, memory, and inference is treated as a system
requirement, not a deployment option.
**Evidence class:** design principle, implemented — private.

## Local control

No layer should require an outbound network dependency to perform its core
function.
**Evidence class:** design principle, implemented — private; sanitized
validation methodology public.

## Inspectability

Important system behavior — decisions, memory mutations, tool invocations —
should be observable, not opaque.
**Evidence class:** design principle, implemented — private.

## Explicit system boundaries

Every layer transition is a named trust and failure boundary (see
[boundaries.md](boundaries.md)), not an implicit one.
**Evidence class:** design principle, documented.

## Failure-aware design

The system defines expected behavior under failure, rather than treating
failure as an unmodeled exception.
**Evidence class:** design principle; validated under controlled scenarios
— see [../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md)
and [../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md).

## Recoverability

Persistent state carries explicit recovery expectations after interruption
or corruption, rather than requiring manual reconstruction.
**Evidence class:** design principle; scenario-validated — private detail,
sanitized summary in [../../evidence/](../../evidence/).

## Auditability

Decisions and memory mutations should be attributable after the fact.
**Evidence class:** design principle, implemented — private.

## Integrity

The system should be able to detect invalid or corrupted state rather than
silently operating on it.
**Evidence class:** design principle, implemented — private.

## Reproducibility

Validation scenarios should be defined precisely enough to be re-run, by
the same team, against the same build class, and to produce comparable
results.
**Evidence class:** design principle, methodology public — see
[../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md).
Independent (third-party) reproduction is not yet established.

## Governance as an executable system concern

Policy enforcement is a runtime layer (L7), not documentation or a
downstream review process.
**Evidence class:** design principle, implemented — private.

---

None of the above should be read as an empirically validated result unless
its evidence class says so, and none currently carries a
"production validated" or "independently reproduced" status. See
[../EVIDENCE-MAP.md](../EVIDENCE-MAP.md).
