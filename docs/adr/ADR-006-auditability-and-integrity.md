# ADR-006 — Auditability and Integrity

## Context

Audit logs in many systems are trusted because of file permissions or
access control alone — if an attacker or a bug can write to the log
storage, the log's trustworthiness is only as strong as that access
control.

## Decision

CORE-AI/7 requires audit records to be tamper-*evident* structurally
(e.g., via hash-chaining), such that tampering is detectable from the log
content itself, independent of file-permission trust.

## Alternatives considered

- **Permission-based trust only.** Rely on filesystem/OS access control to
  protect logs. Rejected as the sole mechanism: this makes log
  trustworthiness a property of host security, not of the architecture,
  and does not survive a compromised host.
- **Full tamper-proofing (e.g., write-once hardware, external notarization).**
  Considered but not required at this research stage: tamper-evidence
  (detectable after the fact) was judged sufficient for the current
  research questions around auditability, at lower operational cost than
  tamper-proofing.

## Tradeoffs

Tamper-evidence detects but does not prevent tampering — an attacker who
can rewrite an entire log chain from scratch is not caught by this
mechanism alone. This is an explicit, stated limitation rather than an
overclaim.

## Consequences

Any component writing audit records must do so through the hash-chained
logging mechanism; ad hoc logging outside that mechanism does not carry
the same integrity guarantee and is not treated as part of the audit
trail.
