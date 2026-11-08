# SDR-002: Treat agent and skill files as executable instructions
- **Status**: Accepted
- **Date**: 2026-11-08
- **Type**: Control
- **Deciders**: Maintainer (security approver)
- **Related**: ADR-001
- **Review by**: n/a

## Context
Files under `agents/` and `copilot/skills/` are loaded by AI hosts as instructions, and the install scripts copy them into user configuration. A malicious change is a prompt-injection or supply-chain vector. `SECURITY.md` already puts these files in scope; this record fixes the controls.

## Threats and Assets
| Threat (STRIDE) | Asset | Spec threat-model row or finding ID |
|-----------------|-------|-------------------------------------|
| Tampering | Agent and skill instructions | n/a (tooling) |
| Information Disclosure | User secrets reachable by the host agent | n/a (tooling) |
| Elevation of Privilege | Local user account running install scripts | n/a (tooling) |

## Decision
We will review diffs to agents, skills, and install scripts like executable code. Instructions must not fetch and run remote code, disable safety checks, hide actions from the user, or exfiltrate data. Install scripts keep `set -euo pipefail`, quoted expansions, and ShellCheck in CI.

## Security Controls
| Control | Standard mapping | How it is verified |
|---------|------------------|--------------------|
| Code review of instruction diffs | OpenSSF Scorecard: Code-Review | Pull request review |
| ShellCheck on `*.sh` | CWE-78 hygiene | `.github/workflows/shellcheck.yml` |
| Dependabot on GitHub Actions | OpenSSF Scorecard: Dependency-Update-Tool | `.github/dependabot.yml` |

## Residual Risk
- **Likelihood / Impact**: Low / High
- **Rating**: Medium
- **Accepted by**: Maintainer — a subtly worded instruction can pass human review
- **Compensating controls**: Private vulnerability reporting per `SECURITY.md`.

## Consequences
Contributors cannot add convenience instructions that run unreviewed remote content.

## Alternatives Rejected
### Option: Automated scanning of instruction text only
No reliable scanner exists for natural-language prompt injection; it may supplement review but cannot replace it.

## Verification
Pull request review; ShellCheck workflow; `SECURITY.md` reporting channel.
