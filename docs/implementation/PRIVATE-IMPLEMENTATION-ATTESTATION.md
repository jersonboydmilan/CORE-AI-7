# Private Implementation Attestation

The public CORE-AI/7 repository is connected to a private implementation
and validation program. This document states what that connection does
and does not mean for the evidence published here.

## What exists privately

The private implementation may contain source code, test suites,
benchmark harnesses, controlled validation environments, deployment
artifacts, and other sensitive operational material. None of this is
published here — see
[../PUBLIC-PRIVATE-BOUNDARY.md](../PUBLIC-PRIVATE-BOUNDARY.md).

## What this does not establish

The existence of a private implementation does not, by itself, make any
public claim more credible than its published evidence supports. Public
claims in this repository are limited strictly to what is documented in
[../evidence/CLAIMS-REGISTER.md](../evidence/CLAIMS-REGISTER.md) and
[../evidence/EVIDENCE-REGISTRY.md](../evidence/EVIDENCE-REGISTRY.md).
Specifically:

- Evidence gathered privately is **not** independently verifiable by a
  reader of this repository.
- A private implementation existing is **not** the same as that
  implementation being publicly reproducible (see
  [../reproducibility/REPRODUCE.md](../reproducibility/REPRODUCE.md)).
- No claim in this repository is asserted at E4 (publicly reproducible),
  E5 (independently validated), or E6 (production validated) on the
  strength of private evidence alone.

## Future publication of build/artifact identity

If and when it is safe to do so without exposing implementation detail or
infrastructure, this repository may in the future publish:

- Release identifiers / version tags for the private reference build.
- Commit hashes corresponding to a specific evaluated build.
- Artifact hashes for evaluated build outputs.
- Signed manifests attesting to a specific build's identity.
- Hashes of sanitized result files, so a reader can verify a published
  summary has not been altered after publication.

**None of these currently exist in this repository.** No hash, signature,
or manifest is published, referenced, or implied anywhere else in this
repository unless it appears in this document with an actual value. This
document will be updated, not fabricated ahead of time, if and when such
artifacts are published.

## How to interpret "private reference build"

Where other documents in this repository refer to a "private reference
build" or "private implementation," they mean: a specific, internally
versioned build of the private implementation that was evaluated to
produce the referenced evidence. No further detail about that build
(location, infrastructure, internal identifiers) is disclosed here.
