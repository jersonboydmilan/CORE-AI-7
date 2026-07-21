# Public / Private Boundary

This document makes the publication strategy of CORE-AI/7 explicit.

## Public

This repository (`core-ai-7`) contains:

- Architecture — layer definitions, trust and failure boundaries,
  conceptual data/control flow.
- Research thesis and research questions.
- Validation methodology — how scenarios are defined and reproduced at the
  laboratory level.
- Sanitized evidence — evidence summaries that do not expose private
  implementation, infrastructure, or sensitive configuration.
- Failure taxonomy — categories of failure and recovery investigated.
- Architecture Decision Records — why key design decisions were made.
- Limitations — what has not been proven, and what remains private.
- Roadmap — active, planned, and future research directions.

## Private

A separate, private implementation repository contains:

- Actual source code (tensor engine, storage engine, agent runtime,
  evaluation harness).
- Private runtime and build configuration.
- Private infrastructure and deployment configuration.
- Internal test harnesses and sensitive benchmark harnesses.
- Proprietary implementation details, internal class structures, and
  internal API contracts.
- Operational systems and private datasets.

## Why the boundary exists

The public repository is a technical research and evidence layer, not a
source-code mirror. It is designed to let a serious technical reader
understand what CORE-AI/7 is, what it investigates, how it is validated,
and what evidence exists — without exposing implementation details that
have no public-safety justification for release.

## Handling uncertainty

Where it is unclear whether a specific artifact is safe to publish, the
default is **not to publish it** and to flag it for human review rather
than exposing it or silently omitting context about its existence.
