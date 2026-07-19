# Implementation Plans

Plans capture an approved route for non-trivial work. They help review, handoff, fresh-session implementation, and recovery after context loss.

A plan is not the source of truth for current behavior after implementation. Current project documentation, ADRs, tests, and code take precedence.

## Use a plan when

- The change spans multiple components or files.
- The implementation order matters.
- The task includes migration, compatibility, security, rollout, or data risk.
- Another person or fresh agent session may implement or review it.
- Material alternatives were compared and approved.

Skip a plan for a clear change whose complete diff can be described in one sentence.

## Naming

```text
YYYY-MM-DD-short-task-name.md
```

## Lifecycle

- Draft: being shaped, not approved for implementation.
- Approved: direction accepted and ready to implement.
- In progress: implementation started.
- Blocked: a new material decision is required.
- Completed: implemented and verified.
- Abandoned: intentionally stopped, with reason.

Use `template.md`. Keep file paths, acceptance criteria, and verification concrete. Update status and material deviations. Do not turn the plan into a chronological work log.
