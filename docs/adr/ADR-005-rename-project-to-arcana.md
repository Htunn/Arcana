# ADR-005: Rename the project from CoreSpec to Arcana
- **Status**: Accepted
- **Date**: 2026-11-09
- **Deciders**: Maintainer
- **Related**: none
- **Reversibility**: Costly to reverse — the plugin ID, marketplace name, and repository URL are public identifiers that users have installed or allow-listed

## Context
"CoreSpec" is generic and reads as tied to a single spec format. The project is a full role-based workflow with a human gate and decision records. The maintainer chose a shorter, more distinctive name.

## Decision Drivers
- A modern, memorable name that does not use "Kit" (GitHub Spec Kit) or the generic "Core".
- Avoiding third-party trademarks, which ruled out names taken from fiction franchises.

## Decision
We will rename the project to Arcana. The Claude Code plugin ID and marketplace become `arcana` (`arcana@arcana`), the repository becomes `Htunn/Arcana`, and all docs, scripts, agent and skill text, and enterprise settings use the new name. Historical CHANGELOG entries keep the old name. The rename ships as a breaking change.

## Consequences
### Positive
- A shorter, distinctive name that describes the project better.

### Negative
- Users who installed `corespec@corespec` or allow-listed the `corespec` marketplace must switch to `arcana@arcana`.
- Links to the old repository work only through GitHub's redirect after the repository is renamed. "Arcana" is a common word, so searches for it are noisy.

## Alternatives Rejected
### Option: Speclane
Free on npm and descriptive, but less distinctive.

### Option: Names from the Harry Potter franchise
Carry trademark risk.

### Option: Keep CoreSpec
Generic, and ties the name to the spec file rather than the workflow.

## Confirmation
`grep -ri corespec` finds matches only in historical CHANGELOG entries and this record. The release notes name the migration step.
