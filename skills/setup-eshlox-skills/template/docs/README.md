# Project Documentation Map

Status: Active documentation index

This directory is the durable project memory. Chat history, agent memory, plans, and code comments are not substitutes for authoritative documentation.

## Authority map

| File                      | Authoritative for                                                                      | Update when                                                          |
| ------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `PROJECT.md`              | Purpose, users, scope, behavior, domain terms, invariants, supported environments      | Product scope or externally observable behavior changes              |
| `ARCHITECTURE.md`         | System boundaries, components, data flow, interfaces, ownership, technical constraints | Architecture or a durable technical boundary changes                 |
| `QUALITY.md`              | Exact commands, test strategy, quality gates, performance evidence, release definition | Tooling, required checks, or release policy changes                  |
| `SECURITY.md`             | Assets, trust boundaries, threat model, abuse cases, controls, verification            | Security assumptions, data handling, permissions, or controls change |
| `architecture/decisions/` | Accepted, rejected, or superseded durable decisions and consequences                   | A consequential choice is made or replaced                           |
| `plans/`                  | Approved implementation plans and execution status                                     | Non-trivial work is approved, materially revised, or completed       |
| `IDEAS.md`                | Optional improvements not approved for implementation                                  | A useful out-of-scope idea is discovered or its status changes       |

## Source-of-truth rules

- Keep each fact in one authoritative file and link to it elsewhere.
- Current accepted documents describe intent and constraints.
- Tests provide executable evidence of supported behavior.
- Code provides implementation truth.
- When these disagree, treat it as a defect to resolve, not permission to guess.
- Plans explain an intended route, but completed plans do not override current project documentation, tests, or code.
- Ideas are hypotheses, not requirements or commitments.
- Comments explain local reasons and invariants only. Do not use comments as project documentation.

## Documentation quality

- Write for a capable maintainer who has no chat context.
- State decisions, constraints, interfaces, invariants, and reasons that are not obvious from code.
- Link to exact files, tests, ADRs, or external standards when useful.
- Use concrete dates in ISO format for time-sensitive facts.
- Mark draft, accepted, superseded, and deprecated material explicitly.
- Delete or supersede stale content instead of appending contradictory notes.
- Do not document implementation detail that names, types, structure, and tests already express clearly.

## Change checklist

For every completed change, decide explicitly whether it changed:

- Product behavior or scope.
- Architecture or data flow.
- Security assumptions or controls.
- Build, test, release, or operational commands.
- A durable decision.
- An approved plan's status.
- An optional idea worth preserving.

Update only the affected authoritative files.
