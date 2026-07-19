# Architecture Decision Records

Use an ADR for a durable, consequential choice whose context and trade-offs will help future maintainers. Examples include architecture boundaries, data models, public contracts, major dependencies, security models, compatibility policy, and operational strategy.

Do not create an ADR for routine implementation details, easily reversible local choices, style already enforced by tools, or a decision fully obvious from code and tests.

## Naming

Use sequential names:

```text
0001-short-decision-title.md
0002-another-decision.md
```

## Status

- Proposed: under discussion and not approved.
- Accepted: current decision.
- Rejected: considered but not selected.
- Superseded: replaced by a later ADR. Link both directions.
- Deprecated: no longer recommended but still relevant to existing code.

## Process

1. Describe the context and decision drivers.
2. Compare only credible options.
3. State the decision clearly.
4. Record positive, negative, and neutral consequences.
5. Link the task, plan, code, tests, and superseding ADRs.
6. Keep the ADR unchanged as a historical record. Supersede it instead of rewriting history, except for typo or link fixes.

Copy `0000-template.md` and replace every bracketed field.
