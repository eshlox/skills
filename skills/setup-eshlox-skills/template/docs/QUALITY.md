# Quality and Definition of Done

Status: Draft
Last reviewed: [YYYY-MM-DD]
Owner: [person or role]

Every command below must be real and verified against the project's CI configuration and package scripts. Do not invent commands or claim checks ran when they did not.

## Required commands

| Purpose    | Command   | When required |
| ---------- | --------- | ------------- |
| Install    | [command] | Clean setup or lockfile verification |
| Focused test | [command with a name or path filter] | Every changed behavior |
| Affected test suite | [command] | Before completion |
| Type check | [command] | Type changes |
| Lint       | [command] | Before completion |
| Format check | [command] | Before completion |
| Build      | [command] | Build-affecting changes |
| Security scan | [command] | Dependency, input, auth, data, or high-risk changes |
| [Other project-specific gate] | [command] | [When] |

[Add notes here for anything that changes how a command behaves: the cheapest gate to run while implementing, checks that need a prior build, environment setup, or browser install.]

## Test strategy

- Test observable contracts, not private implementation shape.
- Use the lowest test level that proves the behavior.
- Add a failing regression test before a bug fix when practical.
- Cover important boundary values, expected failures, and security-relevant cases implied by the requirement.
- Avoid mocks when a stable real boundary or small fake provides stronger evidence.
- Keep tests deterministic, isolated, readable, and fast enough for their intended gate.
- Do not use coverage percentage as a substitute for meaningful assertions.

## Review standard

A change is ready only when:

- It satisfies every acceptance criterion.
- The diff contains no unrelated behavior, refactor, dependency, formatting, or generated-file churn.
- Names and structure reveal intent without unnecessary comments.
- Error handling and cleanup are deliberate.
- Trust-boundary changes have security review and tests.
- Performance claims have representative measurements.
- Required documentation and release notes are current.
- Exact validation evidence is reported.

## Verification order

1. Reproduce the original failure or establish a clean focused baseline.
2. Run the narrowest relevant test while implementing.
3. Run the affected suite for each touched part of the project.
4. Run type checking, linting, format check, and the build.
5. Run contract, integration, security, or other checks when the change reaches those concerns.
6. Perform repeatable runtime or visual verification for user-visible behavior.
7. Inspect the final diff and working tree.

## Evidence format

Report:

| Check | Result | Evidence or limitation |
| ----- | ------ | ---------------------- |
| [Command or manual check] | Pass, fail, or not run | [Exit result, key output, reason, or artifact] |

Do not write `all tests pass` without naming the commands that ran.

## Release policy

[Describe how this project versions and ships, or write `None`. Cover the versioning tool, who may publish, and any release gate.]
