# ADR-001: Ship every role as a paired Claude Code agent and Copilot skill
- **Status**: Accepted
- **Date**: 2026-11-08
- **Deciders**: Maintainer
- **Related**: none
- **Reversibility**: Costly to reverse — users install both formats and file names are public API

## Context
Arcana targets two hosts: Claude Code (`agents/*.md`) and GitHub Copilot (`copilot/skills/*/SKILL.md`). Each host has its own front-matter and discovery rules, but the role instructions are the same.

## Decision Drivers
- A role must behave the same on both hosts.
- Contributors should not have to remember which half they forgot to update.

## Decision
We will keep one agent file and one skill file for every role, with the same instructions in both, and enforce the pairing and the shared spec sections in `scripts/validate.py` on every pull request.

## Consequences
### Positive
- Behaviour is consistent across hosts.
- CI catches a missing half and missing shared sections before release.

### Negative
- Every instruction change is made twice, and CI does not compare the two bodies line by line.
- Host-specific features (for example subagent spawning) must be phrased so they degrade gracefully on the other host.

## Alternatives Rejected
### Option: Generate one format from the other
Adds a build step and hides the shipped text from reviewers; rejected for a repository whose content is the product.

### Option: Support one host only
Excludes a large part of the audience.

## Confirmation
`scripts/validate.py` fails when an agent or skill has no pair or when a role that embeds a template omits one of its sections. Body drift beyond that is caught in review.
