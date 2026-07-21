# Reproducibility

An honest statement of what can and cannot currently be reproduced from
this repository.

## Currently reproducible

- **Architecture documentation** — the canonical specification
  ([../architecture/CORE-AI-7-SPECIFICATION.md](../architecture/CORE-AI-7-SPECIFICATION.md))
  and supporting documents describe the architecture completely enough
  for a reader to understand and critique the design.
- **Research methodology** — the doctrine and research-question documents
  ([../doctrine/](../doctrine/)) are fully public and open to critique or
  extension by any reader.
- **Threat/failure model** — the failure taxonomy
  ([../failure-research/failure-taxonomy.md](../failure-research/failure-taxonomy.md))
  and failure case index
  ([../failures/FAILURE-CASE-INDEX.md](../failures/FAILURE-CASE-INDEX.md))
  are public conceptual models, reproducible as analysis (a reader can
  apply the same taxonomy to a different system).
- **Public evidence interpretation** — the claims, evidence, and
  benchmark registries state exactly what was measured and how; a reader
  can evaluate whether the stated methodology supports the stated
  conclusion, even without re-running it.
- **Validation methodology** — the abstract validation chain in
  [../validation/VALIDATION-METHODOLOGY.md](../validation/VALIDATION-METHODOLOGY.md)
  is public and could be applied by a third party to their own
  implementation of a similar system.

## Not currently reproducible

- **The complete private implementation** — no source code is published
  in this repository.
- **Private deployment environments** — laboratory environment identity
  beyond its stated class (e.g., "commodity CPU workstation") is not
  published.
- **Private operational infrastructure** — build systems, CI
  configuration, and infrastructure are private.
- **Sensitive testing environments** — fault-injection technique for
  storage-recovery validation is withheld pending public-safety review
  (see [../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-004](../evidence/EVIDENCE-REGISTRY.md#core-ai-7-e-004)).
- **Unpublished validation material** — any scenario not listed in the
  claims/evidence/benchmark registries has not been run, or has not been
  published, and should not be assumed to exist.

## Independent reproduction status

**Independent reproduction has not yet been established for any claim in
this repository.** No third party has re-run a CORE-AI/7 scenario and
confirmed its result. This is stated explicitly and applies uniformly
unless a specific future evidence entry documents otherwise.

## Future reproduction path

For an independent researcher to reproduce a CORE-AI/7 result in the
future, the following would need to exist and be published, none of which
exist today:

1. A public, runnable reference implementation (or a reduced public
   artifact sufficient to exercise the specific claim) — see
   [../implementation/PRIVATE-IMPLEMENTATION-ATTESTATION.md](../implementation/PRIVATE-IMPLEMENTATION-ATTESTATION.md)
   for the conditions under which build/artifact identifiers might be
   published.
2. A publicly documented workload/dataset matching the one referenced in
   the relevant benchmark-registry entry (synthetic data can be
   regenerated from a documented procedure; the current entries do not
   yet specify one precisely enough for exact reproduction).
3. A defined, public environment class specification precise enough that
   a third party's result would be comparable, not merely similar.
4. A named independent party willing to run the reproduction and publish
   their own result, positively or negatively.

Until all four exist for a given claim, that claim remains at E3
(internally validated) at most.
