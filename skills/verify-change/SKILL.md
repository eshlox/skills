---
name: verify-change
description: Before declaring a change complete, prove it - map every acceptance criterion and risk to a concrete test, command, scan, or runtime check, run the repository's required quality gates, and report an evidence table. Use before any "done", "passing", "secure", or "faster" claim, as the final step of the shape / implement / review / verify workflow. This focuses on acceptance-criteria evidence and the repo's defined checks; for open-ended end-to-end exploration of a running app, the verify skill is more specialized.
---

# Verify a Change

## Principle

Evidence before claims. Code that looks correct is not verified.

## Process

1. Read the approved acceptance criteria and verification plan.
2. Inspect Git status and the complete diff. Confirm the expected files changed and no unrelated files changed.
3. Map each acceptance criterion and material risk to a test, command, runtime check, scan, benchmark, or inspection.
4. Run the narrowest relevant checks first.
5. Run all affected commands required by `docs/QUALITY.md` and `AGENTS.md`.
6. Inspect exit codes and meaningful output. Do not treat a command invocation as a pass.
7. For user-visible behavior, perform a repeatable runtime or visual check when tooling permits.
8. For security-sensitive behavior, verify the relevant trust boundary, unauthorized path, malformed input, secret handling, and failure behavior.
9. For performance claims, run a representative before-and-after benchmark and report method, workload, variance, and limitations.
10. Confirm documentation, ADR, plan status, localization output, generated files, and changeset requirements.
11. If a check fails, fix only within the approved scope. Stop and ask when the fix requires a new material decision.
12. Never hide, truncate, or paraphrase away a failure.

## Completion evidence

Report:

| Acceptance criterion or risk | Evidence                                       | Result                 | Limitation      |
| ---------------------------- | ---------------------------------------------- | ---------------------- | --------------- |
| [Criterion]                  | [Command, test, scan, benchmark, or procedure] | Pass, fail, or not run | [Gap or `None`] |

Then report:

- Exact commands run.
- Tests or checks not run and why.
- Files changed.
- Documentation and changeset status.
- Assumptions and residual risks.
- Optional observations not implemented.

## Prohibited claims

Do not state or imply:

- All tests pass, unless all named required tests ran successfully.
- The code is secure, bug-free, leak-free, race-free, or production-ready without scoped evidence.
- Performance improved without measurement.
- Existing behavior is unchanged without relevant regression evidence.
