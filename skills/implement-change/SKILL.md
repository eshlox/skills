---
name: implement-change
description: Build an approved or clearly-scoped code change as a surgical diff with focused tests, updated docs, and no scope creep. Use this as the coding step once the direction is settled - bug fixes, small features, and well-understood edits - especially in a repo with an AGENTS.md contract. If the change is still ambiguous or material and not yet agreed, use shape-change first. This is the build step, not the design step.
---

# Implement an Approved Change

## Entry conditions

- The goal and acceptance criteria are clear.
- Material choices are approved or already fixed by project policy.
- The expected scope is understood.
- There is no unresolved dependency, schema, API, security, compatibility, architecture, or destructive-operation decision.

If an entry condition fails, stop and use `shape-change`.

## Process

1. Read `AGENTS.md`, `docs/README.md`, the approved task or plan, relevant code, tests, and current Git status.
2. Confirm the narrowest files and behavior that must change.
3. Establish a baseline with the smallest relevant test or reproduction.
4. For a bug fix, add or identify a focused test that fails for the reported behavior when practical. Observe the failure before changing production code.
5. Implement the simplest direct solution using existing patterns, native APIs, and current dependencies.
6. Keep each edit tied to an acceptance criterion or required verification.
7. Stop and ask if implementation exposes a new material choice or requires scope expansion.
8. Run focused checks while iterating. Read failures and fix root causes rather than patching symptoms.
9. Inspect the diff for unrelated changes, speculative abstractions, duplicate logic, cleverness, stale comments, debug output, and avoidable code.
10. Update only the authoritative documentation whose truth changed.
11. Add a changeset when repository policy requires it.
12. Use `review-change`, then `verify-change` before completion.

## Simplicity test

Before keeping a helper, abstraction, option, fallback, or dependency, ask:

- Is it required by a current acceptance criterion or invariant?
- Does it reduce total conceptual complexity now?
- Is there already a suitable project pattern or native API?
- Would deleting it preserve correctness and clarity?

Delete it when it does not earn its cost.

## Boundaries

Do not:

- Add optional features or future-proofing.
- Refactor unrelated code.
- Modernize neighboring code without approval.
- Add a dependency without the dependency evaluation and approval gate.
- Change public behavior to make implementation easier.
- Weaken tests, types, lint rules, security controls, or error handling.
- Claim completion based only on code inspection.
