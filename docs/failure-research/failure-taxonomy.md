# Failure Taxonomy

CORE-AI/7 treats failure as a designed-for condition, not an unmodeled
exception. Each category below is investigated using the conceptual model:

```
FAILURE
    ↓
DETECTION
    ↓
ISOLATION
    ↓
RECOVERY
    ↓
VERIFICATION
```

## Interrupted operations

A write or mutation is stopped mid-flight (process kill, power loss). The
research question is whether the system can distinguish "nothing happened"
from "something happened but wasn't acknowledged" from "something happened
and was acknowledged" — and recover to exactly the last acknowledged state.

## Corrupted state

Persisted state is damaged (bitrot, torn write, malformed record). The
research question is detection: can corruption be identified structurally
(checksums, structural invariants) rather than assumed absent.

## Process failure

A component (an agent, a worker) fails outright. The research question is
containment: does the failure stay local to that component's dependents,
or does it silently propagate.

## Stale runtime state

In-memory state diverges from persisted state (e.g., after a partial
restart). The research question is whether staleness is detectable before
it is acted on.

## Dependency failure

A local dependency (e.g., the local inference backend process) becomes
unavailable. The research question is degraded-mode behavior: does the
system fail the specific operation that needed the dependency, or fail
globally.

## Service interruption

Distinguished from dependency failure in scope — an interruption affecting
multiple components at once. The research question is ordering: which
components must recover before others can safely resume.

## Recovery after restart

The system is restarted after any of the above. The research question is
whether recovery is a defined, idempotent procedure or an ad hoc one.

## Integrity verification

After recovery, is state checked against structural invariants before the
system is considered "back," or is recovery assumed successful once the
process starts.

## Cascading failure

The failure mode specific to agentic systems: a low-quality or corrupted
item enters an agent's context, produces corrupted output, which is written
back to memory, retrieved again with higher apparent authority, and
amplified across agents until the memory substrate is untrustworthy.
CORE-AI/7's architectural response is discussed layer-by-layer in
[../architecture/boundaries.md](../architecture/boundaries.md) — the
short version is that write-back to memory is gated by governance (L7),
provenance is recorded at the point of context assembly (L3), and agents
exchange typed messages rather than shared mutable state (L6), so no
single hop in the cascade is unmonitored.

## Degraded operation

Where full recovery is not immediately possible, does the system have a
defined degraded mode (reduced capability, explicit user-visible state)
rather than an undefined one.

---

Evidence for how thoroughly each category has been exercised against the
private implementation is tracked in
[../EVIDENCE-MAP.md](../EVIDENCE-MAP.md). This document describes the
research categories, not the private implementation's mechanisms.
