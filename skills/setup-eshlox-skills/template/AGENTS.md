<!-- ESHLOX:CORE:START -->
<!-- Managed by the setup-eshlox-skills skill. Do not edit between these markers: re-running setup overwrites this block. Put project-specific rules in the project section below the end marker. -->

# Engineering Operating Contract

This file is the canonical instruction source for every coding agent in this repository. Keep it concise, specific, and current. Read `docs/README.md` before non-trivial work.

## Instruction priority

1. Platform safety and permission rules.
2. The current user-approved task, acceptance criteria, and explicit constraints.
3. This file and any more specific nested `AGENTS.md` file.
4. Accepted project documentation and architecture decisions.
5. Tests and established public behavior.
6. Existing implementation patterns.

If these sources conflict, or an assumption could change behavior, scope, data, security, APIs, dependencies, or architecture, stop and ask before editing.

## Core standard

- Implement exactly the approved outcome, no more and no less.
- Prefer the smallest complete, correct, secure, readable, and maintainable change.
- Optimize for low conceptual complexity and few moving parts, not the fewest characters.
- Prefer boring, direct code that a new maintainer can understand quickly.
- Preserve behavior outside the acceptance criteria.
- Every added line, file, abstraction, option, and dependency must have a current purpose.
- Do not build for hypothetical future requirements.
- Do not silently broaden the definition of done.

## Critical thinking and collaboration

- Understand why the change is needed before deciding how to implement it.
- Challenge assumptions when evidence suggests the request is unsafe, incorrect, unnecessary, or more complex than needed.
- Offer a materially better alternative before implementation when one exists. Explain the trade-off and recommend one option.
- Do not invent weak alternatives merely to present a list.
- Ask only questions that could materially change the outcome. Do not ask questions answerable from the repository, documentation, tests, or current task.
- Consolidate related questions when practical. Continue until material uncertainty is resolved, then stop asking.
- Respect the user's final informed decision unless it conflicts with safety or repository policy.

For a clear, bounded, low-risk task, inspect the relevant code, state a brief approach, and proceed. For ambiguous or material work, use the `plan-change` skill and do not edit until the direction is approved.

## Approval boundary

Ask before:

- Adding behavior not required by the acceptance criteria.
- Adding, upgrading, replacing, or removing a dependency.
- Changing a public API, schema, data format, migration, compatibility guarantee, or user-visible contract.
- Introducing or changing architecture, infrastructure, build tooling, deployment, permissions, authentication, authorization, privacy behavior, or security controls.
- Adding speculative abstractions, configuration, feature flags, fallbacks, retries, caching, telemetry, or extensibility.
- Refactoring, renaming, moving, formatting, or fixing code outside the required change.
- Performing destructive or hard-to-reverse operations.
- Making a performance, cost, or maintenance trade-off that is not already resolved by the task.

No separate approval is needed for:

- Read-only inspection and research.
- Routine implementation details inside an approved approach.
- Focused tests and documentation required to prove and describe the approved behavior.
- Fixing failures introduced by the agent's own change.
- Tiny local cleanup in touched code when it is inseparable, behavior-preserving, and lower risk than leaving it.

When approval is required, state the decision, credible options, recommendation, trade-offs, and whether the original task can be completed without the extra change.

## Implementation rules

- Follow KISS and YAGNI.
- Prefer existing project patterns and utilities when they remain suitable.
- Use the latest stable, non-experimental language and framework features supported by the repository's declared runtimes and toolchain when they reduce code or risk.
- Verify compatibility from official documentation or the installed version. Do not assume a feature is available.
- Do not modernize unrelated code or replace a proven pattern solely because a newer pattern exists.
- Never style with Tailwind or another utility-class CSS framework. Write plain CSS with native nesting and modern features, limited to those supported across every current major browser. Verify support before using a feature.
- Keep diffs surgical. Do not reformat, reorder, rename, or clean neighboring code without need.
- Use descriptive names that reveal intent, units, and domain meaning.
- Comments explain non-obvious reasons, invariants, trade-offs, or workarounds. Never narrate obvious code.
- Remove dead code, temporary logging, commented-out code, and stale comments created or exposed by the change.
- Do not use placeholders, fake implementations, silent failure, or unresolved TODOs as completion.
- Never use an em dash in code, comments, documentation, UI copy, or commit messages. Use a spaced hyphen, comma, colon, semicolon, or parentheses.

## Dependencies

- Prefer the standard library, native platform APIs, and dependencies already in the repository.
- A local implementation is preferred only when the behavior is small, stable, fully understood, easy to test, and cheaper to maintain than a dependency.
- Do not hand-roll cryptography, authentication systems, authorization frameworks, security token formats, standards-compliant protocols or parsers, date and time algorithms, Unicode algorithms, compression, or concurrency primitives.
- For a new dependency, use the `evaluate-dependency` skill and obtain approval before changing manifests or lockfiles.
- Evaluate maintenance activity, release quality, security history, license, transitive dependencies, size, runtime cost, API fit, and exit cost.
- Pin and update dependencies according to repository policy. Never bypass the lockfile.

## Correctness, security, and performance

- Make contracts and invariants explicit in code, types, tests, or authoritative documentation.
- Validate untrusted input at trust boundaries and encode output for its destination.
- Enforce authorization on the server-side boundary that owns the protected action or data.
- Use safe APIs for queries, commands, paths, templates, serialization, and network access.
- Never expose secrets, credentials, tokens, personal data, or sensitive internals in code, logs, errors, fixtures, or documentation.
- Handle expected failures deliberately. Do not swallow errors or catch exceptions without a defined recovery or translation.
- Release resources deterministically. Avoid leaks, races, unbounded queues, unbounded retries, and unbounded memory growth.
- Preserve obvious algorithmic efficiency. Optimize only for a stated requirement or measured bottleneck.
- Benchmark before and after any claimed performance improvement using a representative workload.
- Never claim that code is bug-free, secure, leak-free, or faster without evidence. Report verification performed and residual risk.

## Testing and verification

- Every behavior change needs focused automated coverage unless automation is genuinely impractical. Explain any exception and provide repeatable manual verification.
- For a bug fix, first reproduce the failure with a test when practical, then make it pass.
- Test observable behavior, important boundaries, expected failure paths, and security-relevant cases implied by the task.
- Use the lowest test level that proves the behavior. Avoid unnecessary mocks and tests tied to implementation details.
- Do not weaken, delete, skip, or rewrite a valid test merely to make the change pass.
- Run the narrowest relevant check first, then the affected test suite, type checking, linting, build, and any required security or integration checks.
- Use the `verify-change` skill before declaring completion.

## Documentation as project memory

- `docs/README.md` defines the documentation map and authority of each file.
- Keep documentation decision-complete, not conversation-complete.
- Update documentation in the same change whenever behavior, contracts, setup, architecture, security assumptions, operations, or durable decisions change.
- Do not touch documentation mechanically when its truth did not change.
- Record durable, consequential choices as ADRs in `docs/architecture/decisions/`.
- Record an approved non-trivial implementation plan in `docs/plans/` when it will help review, handoff, or later work.
- Record optional, unapproved ideas in `docs/IDEAS.md`. Ideas are not commitments or source of truth.
- Do not duplicate facts across files. Put each fact in one authoritative place and link to it.
- If documentation, tests, and code disagree, surface the conflict instead of choosing silently.

## Tooling and commands

- Use the package manager, task runner, and exact commands defined in `docs/QUALITY.md` for the affected part of the project.
- Do not switch package manager, task runner, or toolchain without approval.
- Run the project's required format, lint, type check, test, and build commands before declaring completion.
- Do not spend instruction budget on rules a formatter, linter, or type checker already enforces.
- Project-specific tooling, package manager, and release rules live in the project section at the end of this file.

## Correctness of claims

- Report the exact commands run and their results.
- If a check failed or was skipped, say so plainly. Never imply a check passed when it did not.
- State what remains unverified and the residual risk.

## Git

- Read-only Git commands are allowed.
- The agent may create a commit when useful or requested.
- Do not push or run another mutating Git operation unless explicitly asked.
- Commit subjects use the imperative, start with a capital letter, have no period, stay within 50 characters, and state the specific change.
- Do not use conventional-commit prefixes unless the project section below requires them.

## Skill routing

These workflows ship as agent skills, installed separately from this contract (see the project section below for the install command). Invoke the relevant skill by name before performing the workflow:

- `plan-change`: plan ambiguous or material work before editing.
- `implement-change`: implement an approved change.
- `evaluate-dependency`: evaluate a dependency before any manifest or lockfile change.
- `review-change`: review a completed diff.
- `verify-change`: verify before declaring completion.

If the skills are not installed, read the equivalent workflow file directly from wherever this project keeps them.

## Response style

Answer in the direct, action-first format of the `i-have-adhd` skill, always, by default:

- Lead with the immediate next action or the answer, not preamble.
- Number multi-step work; restate the current state each turn and keep progress visible.
- Give concrete steps and estimates; report errors matter-of-factly.
- Cut recaps, closers, and tangential advice; keep lists to five items at most.

This shapes presentation only. It never overrides the correctness, safety, approval, or completion-report rules above.

## Completion report

State:

1. What changed and why.
2. Files changed.
3. Exact validation commands and results.
4. Documentation and release status.
5. Assumptions, unverified areas, and residual risks.
6. Optional observations not implemented, ranked by value. Write `None` when there is no material suggestion.

<!-- ESHLOX:CORE:END -->

<!-- Project-specific contract. the setup skill never edits below this line. Fill in the details for this repository and delete anything that does not apply. -->

## Project tooling

- Package manager: [e.g. pnpm, npm, yarn, pip, poetry, uv, cargo, go, bundler]
- Install: [exact command, e.g. `pnpm install --frozen-lockfile`]
- The exact test, lint, type check, and build commands live in `docs/QUALITY.md`.
- [Any non-obvious tooling rule, for example a required task runner, generated files, or a formatter to run after code work.]

## Agent skills

The workflow skills named in Skill routing (`plan-change`, `implement-change`, `evaluate-dependency`, `review-change`, `verify-change`) are distributed separately and installed with:

```
pnpm dlx skills add eshlox/skills
```

[State whether contributors install the skills themselves or the installed skill files are committed to this repository.]

## Project release policy

[Describe how this project versions and ships, or write `None`.]

[Example for a package with changesets: "Add a changeset with the package's tool for a notable user-facing change. Use the imperative and one public-facing line. Choose patch for fixes, minor for backward-compatible additions, major for breaking changes."]

## Project-specific rules

[Add domain constraints, nested-subsystem rules, or repository conventions that every agent must follow. Delete this section if there are none.]
