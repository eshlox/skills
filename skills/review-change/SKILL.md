---
name: review-change
description: Review a finished change by hand against the approved task and this repository's operating contract - scope creep, correctness, security, simplicity, tests, docs, dependencies, and unsupported performance claims. Report findings only and do not edit unless asked. Use as the review step of the shape / implement / review / verify workflow, especially in repos with an AGENTS.md contract. For a heavier multi-agent standards-and-spec review of a whole branch or PR, use the separate code-review skill instead.
---

# Review a Change

## Default mode

Review only. Do not edit files, install packages, or broaden the task unless explicitly asked after findings are presented.

## Preparation

Read:

- `AGENTS.md` and applicable nested rules.
- The task contract, approved plan, and related ADRs.
- Relevant project documentation.
- The complete diff, changed tests, and affected interfaces.

Do not review against imagined requirements.

## Review order

1. Scope compliance
   - Every change is required by the approved outcome or verification.
   - No unrelated cleanup, feature, dependency, configuration, or behavior slipped in.
2. Correctness
   - Acceptance criteria and invariants hold.
   - Boundary values, state transitions, failure paths, ordering, concurrency, and cleanup are correct where relevant.
3. Security and privacy
   - Trust boundaries, validation, encoding, authorization, secrets, logging, injection, path handling, resource limits, and dependency risk are handled.
4. Simplicity
   - No avoidable abstraction, indirection, option, fallback, duplication, or cleverness.
   - Names and structure make the change easy to understand.
   - Deleting code or using an existing native or project pattern would not improve it.
5. Tests
   - Tests prove observable behavior and important failures.
   - Assertions are meaningful and deterministic.
   - Mocks do not hide the behavior being claimed.
6. Documentation and release
   - Changed truths, ADRs, plans, and changesets are current and non-duplicative.
7. Dependencies and performance
   - Dependency choices are approved and justified.
   - Performance claims have representative measurements.

## Findings

Report only actionable findings. Avoid personal style preferences and generic best-practice advice.

Classify:

- Critical: exploitable, destructive, data-loss, or fundamentally wrong behavior.
- High: likely production defect, material security issue, broken contract, or major scope violation.
- Medium: credible edge-case defect, maintainability cost, weak verification, or documentation mismatch.
- Low: small clarity or robustness issue worth fixing in this diff.

For each finding include:

```text
Severity and title
Location
Evidence
Impact
Smallest correction
```

End with:

- Acceptance criteria coverage.
- Unnecessary code or scope creep to remove.
- Test and verification gaps.
- Residual risk.
- `No material findings` when appropriate.
