# ADR-004: Record significant decisions as ADRs and security decisions as SDRs
- **Status**: Accepted
- **Date**: 2026-11-08
- **Deciders**: Maintainer
- **Related**: ADR-002, SDR-001, SDR-002
- **Reversibility**: Reversible — records can be adopted or retired without touching shipped specs

## Context
Arcana described ADRs in the README but nothing produced them: `spec-driver` never asked for one, specs had nowhere to reference them, and accepted security risk lived in free-text notes with no owner or expiry. Spec Kit-style workflows treat research and decisions as first-class outputs of the planning step.

## Decision Drivers
- Specs say what and how; the why and the rejected options need a durable home.
- Security risk acceptance needs a named approver and a review date.

## Decision
We will keep two decision logs, `docs/adr/ADR-NNN-{slug}.md` and `docs/sdr/SDR-NNN-{slug}.md`, from `templates/ADR-template.md` and `templates/SDR-template.md`. Every spec lists its decisions in a `## Decision Records` section. `software-architect` and `platform-architect` own ADRs; `devsecops-architect` owns SDRs. Records start `Proposed` in Phase 2 and become `Accepted` when the human approves the spec in Phase 3. Findings accepted instead of fixed in Phase 6 become SDRs of type Risk Acceptance.

## Consequences
### Positive
- The reasons behind a design survive the spec being superseded.
- Accepted security risk is visible, owned, and expires.

### Negative
- Two more artifacts per significant decision; the thresholds in the README keep them rare.

## Alternatives Rejected
### Option: One combined decision log
Security decisions need a different approver, expiry, and residual-risk fields, and are audited separately.

### Option: Keep decisions inside the spec only
Lost when the spec is superseded, and not discoverable across features.

## Confirmation
`scripts/validate.py` checks both templates, validates every file under `docs/adr/` and `docs/sdr/`, and checks that the owning roles and `spec-driver` embed the templates and reference the records.
