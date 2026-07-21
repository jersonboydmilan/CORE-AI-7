# Research Thesis

## What is missing from conventional AI system design?

Most AI applications are composed as a thin orchestration layer over a
remote model API, a remote hosted vector database, and a handful of
framework dependencies. Control, inspectability, and availability are
delegated outward at nearly every layer: the model provider controls
inference, the vector-database vendor controls memory, and the framework
controls orchestration. When any of those third parties changes terms,
degrades, or fails, the system built on top inherits the failure with no
local recourse.

CORE-AI/7's thesis is that this is not an incidental property of current
tooling — it is a consequence of treating "intelligence system" as
synonymous with "interface to a model." Sovereignty, inspectability, and
resilience are not properties that can be retrofitted onto a system
assembled this way; they have to be architectural decisions made at every
layer, from raw compute up through governance and audit.

## The central question

> How can intelligence systems be designed as controllable, inspectable,
> resilient, and locally sovereign infrastructure rather than merely as
> model interfaces?

## Research direction

CORE-AI/7 investigates this question by tracing a single path through a
system, end to end:

```
AI MODEL
    ↓
CONTEXT
    ↓
MEMORY
    ↓
RETRIEVAL
    ↓
REASONING
    ↓
AGENTS
    ↓
GOVERNANCE
    ↓
AUDIT
    ↓
RECOVERY
```

At each stage, the research asks what changes when the stage is required to
run under local control and be independently inspectable, and what
architectural property is necessary (not merely convenient) to make that
true. The seven-layer reference architecture in
[../architecture/system-overview.md](../architecture/system-overview.md) is
the current answer; it is treated as a hypothesis under ongoing validation,
not a finished result.

## What this thesis does not claim

This is a research thesis, not a proof. It does not claim that sovereign
architecture is strictly superior to hosted architecture for every use
case, that the current reference implementation fully realizes every
principle it is held to, or that any result described in this repository
has been independently reproduced. See
[limitations.md](limitations.md) and
[../EVIDENCE-MAP.md](../EVIDENCE-MAP.md).
