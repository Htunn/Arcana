# ADR-002: Keep one single-file spec with stable IDs per feature
- **Status**: Accepted
- **Date**: 2026-11-08
- **Deciders**: Maintainer
- **Related**: ADR-003
- **Reversibility**: Costly to reverse — IDs are cited by tasks, tests, and deviations

## Context
Spec-driven toolkits such as GitHub Spec Kit split work into a specification, a plan, research notes, contracts, and a task list. Arcana has several authoring roles that each own a section, and a human who approves the whole thing once.

## Decision Drivers
- One approval target for the human gate.
- Every criterion must be traceable to its tasks, tests, and deviations.
- Business sections must stay free of implementation detail.

## Decision
We will keep a single `specs/SPEC-NNN-{slug}.md` per feature, divided into role-owned sections, with stable `G-`, `NG-`, `US-`, `AC-`, and `OQ-` IDs. Derived artifacts (`-tasks`, `-test-plan`, `-review`, `-deviations`) live beside it and cite those IDs. The Technical Design section carries the plan content: research and assumptions, data model, contracts, and sequence diagrams.

## Consequences
### Positive
- One file to review and approve; one place for traceability.
- Parallel architects edit disjoint sections.

### Negative
- Long specs for large features; split the feature instead of the file.
- Plan content cannot be reviewed separately from requirements.

## Alternatives Rejected
### Option: Separate spec, plan, research, and contracts files
Closer to Spec Kit, but multiplies approval targets and weakens the single human gate.

## Confirmation
`scripts/validate.py` checks that the roles embedding the template contain every section of `templates/SPEC-template.md`.
