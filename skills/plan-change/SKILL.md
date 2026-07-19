---
name: plan-change
description: Plan and get sign-off on a non-trivial or ambiguous code change BEFORE editing anything - restate the goal, compare credible options, recommend one, and define acceptance criteria. Use whenever a request touches new features, public APIs, schemas, dependencies, architecture, security, performance, or migrations, or when requirements are uncertain, even if the user only says "add X" or "change Y" without asking for a plan. Stop at the agreed plan and do not write production code. Skip only for tiny, self-contained, low-risk edits, which go straight to implement-change.
---

# Plan a Change

## Purpose

Reach an informed, approved implementation direction before code changes consume time or create anchoring.

## Rules

- Remain read-only until the material direction is approved.
- Read `AGENTS.md`, `docs/README.md`, relevant authoritative docs, code, tests, and history.
- Do not ask a question the repository can answer.
- Challenge assumptions with evidence, not reflexive disagreement.
- Compare alternatives only when they are genuinely credible and materially different.
- Prefer the smallest proven solution that meets the current requirements.
- Do not create code, dependencies, schemas, migrations, or configuration during planning.

## Process

1. Restate the goal, user value, and observable success.
2. Inspect the current behavior and relevant project patterns.
3. Identify missing information that could change behavior, scope, APIs, data, security, compatibility, architecture, dependency choice, performance, cost, or operations.
4. Ask focused questions. Attach a recommended default or current hypothesis when it helps the user decide.
5. Define acceptance criteria, important failure cases, constraints, invariants, and explicit non-goals.
6. Identify assumptions and mark each as verified, user-approved, or unresolved.
7. Produce up to three credible options for each material decision. If only one option is credible, say why instead of inventing alternatives.
8. Compare options by:
   - Requirement fit.
   - Conceptual and operational simplicity.
   - Correctness and security risk.
   - Compatibility and migration impact.
   - Performance evidence or likely complexity.
   - Maintenance and dependency cost.
   - Reversibility and exit cost.
9. Recommend one option and explain why the others lose.
10. State the smallest expected file and behavior scope.
11. Present a decision gate and wait for explicit approval.

## Output

Use this structure:

```text
Goal
Current behavior and evidence
Material questions
Acceptance criteria
Out of scope
Options and trade-offs
Recommendation
Expected scope
Risks and verification
Decision needed
```

After approval, write a plan under `docs/plans/` only when the work is non-trivial enough to benefit from a durable handoff. Then use `implement-change`.
