# ADR-003: Make the human review gate mandatory before implementation
- **Status**: Accepted
- **Date**: 2026-11-08
- **Deciders**: Maintainer
- **Related**: ADR-002
- **Reversibility**: Costly to reverse — removing the gate changes the guarantee users rely on

## Context
AI agents can write a spec and the code for it in one run. Without a stop, contradictions between design, infrastructure, and security are found after code exists, when they are most expensive.

## Decision Drivers
- Spec errors cost the least before implementation starts.
- Agents cannot be the sole approver of their own output.

## Decision
We will run a ten-phase workflow (0–9) in which Phase 3 is a mandatory stop. `spec-driver` never starts implementation until the user explicitly approves, and any later edit to an approved spec goes back through the gate.

## Consequences
### Positive
- The human reviews one complete, consistent artifact.
- Decisions (ADRs and SDRs) are accepted at the same moment as the spec.

### Negative
- Slower for trivial changes; the workflow is for non-trivial features only.

## Alternatives Rejected
### Option: Autonomous run with post-hoc review
Cheaper per run, but defects reach code before anyone with authority has seen the design.

## Confirmation
`scripts/validate.py` checks the phase list matches across the agent, skill, and README. The gate wording is checked in review.
