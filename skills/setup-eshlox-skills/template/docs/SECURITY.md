# Security Model

Status: Draft
Last reviewed: [YYYY-MM-DD]
Owner: [person or role]

This document records project-specific security facts. Do not place secrets, credentials, exploit payloads for live systems, or sensitive operational detail here.

Scope: [state what this document covers and what external system, if any, actually enforces authorization.]

## Assets

| Asset   | Sensitivity | Owner | Required protection |
| ------- | ----------- | ----- | ------------------- |
| [Asset] | [Public, Internal, Confidential, Restricted] | [Owner] | [What must be protected and how] |

## Trust boundaries

| Boundary | Untrusted input | Validation and authorization owner | Output or side effect |
| -------- | --------------- | ---------------------------------- | --------------------- |
| [Boundary] | [Input] | [Where it is validated] | [Effect] |

[Describe the validation contract: where input is checked, whether it is allow-listed, what error is produced, and that it fails before any state changes.]

## Authentication and authorization

- [Where credentials live, or that this component holds none.]
- [Which system makes each authorization decision. Nothing client-side may be treated as an access control.]

## Data handling

- [How sensitive data and PII are minimized, redacted, or kept out of logs and errors.]

## Secrets and configuration

- [Rule that no secret belongs in the repository, and how configuration separates non-secret endpoints from real secrets.]
- [Any credential committed on purpose, with the reason it is safe.]

## Abuse cases

| Abuse case | Impact | Prevention | Detection | Recovery |
| ---------- | ------ | ---------- | --------- | -------- |
| [Case]     | [Impact] | [Control] | [Signal] | [Response] |

## Dependency and supply-chain policy

- Prefer native APIs and existing reviewed dependencies.
- Require approval and documented evaluation before adding or replacing a dependency. Use the `evaluate-dependency` skill.
- Commit the lockfile and verify integrity in CI.
- Review install scripts, transitive dependencies, maintainership, release provenance, advisories, and license.
- Never execute unreviewed third-party agent skills, hooks, or scripts with broad repository or network permissions.

## Secure implementation baseline

- Validate external input at the boundary that understands its contract.
- Encode output for the destination context.
- Use parameterized queries and safe process APIs.
- Enforce authorization server-side for every protected action and object.
- Avoid sensitive data in logs and error responses.
- Use established libraries for cryptography, authentication protocols, token formats, and security-sensitive parsers.
- Bound resource use, retries, uploads, queues, recursion, and concurrency.
- Fail closed when authorization or security state is uncertain.

## Verification

| Control or threat | Automated check | Manual review | Frequency |
| ----------------- | --------------- | ------------- | --------- |
| [Control]         | [Test or scan]  | [Review]      | [Cadence] |

## Known risks and accepted exceptions

| Risk   | Impact | Mitigation | Owner | Review date | Decision |
| ------ | ------ | ---------- | ----- | ----------- | -------- |
| [Risk] | [Impact] | [Mitigation] | [Owner] | [YYYY-MM-DD] | [Open or Accepted with reason] |

## Incident and disclosure process

[How to report a suspected vulnerability, and where the private incident runbook lives. Do not duplicate the runbook here.]
