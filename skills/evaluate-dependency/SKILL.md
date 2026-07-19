---
name: evaluate-dependency
description: Decide the right way to get a capability before changing any dependency - weigh native or standard-library APIs, a small local implementation, an existing dependency, and a new maintained library, then recommend one with its security and maintenance trade-offs. Trigger this whenever adding, replacing, upgrading, or removing a dependency is even being considered, including casual "just install X" or "add a package for Y" requests, and always before editing a manifest or lockfile.
---

# Evaluate a Dependency

## Rule

Do not change a manifest, lockfile, import, or installation state during evaluation. Obtain explicit approval for the selected dependency action.

## Process

1. Define the exact capability needed and the required edge cases.
2. Confirm whether the need is real and inside the approved task.
3. Check, in order:
   - Standard library or native platform API.
   - Existing project utility or dependency.
   - Small local implementation.
   - New external library.
4. Reject a local implementation for cryptography, authentication protocols, authorization frameworks, security tokens, standards-compliant parsers or protocols, date and time algorithms, Unicode algorithms, compression, concurrency primitives, or another domain where subtle correctness and security dominate line count.
5. Evaluate each credible option by:
   - Correctness and specification coverage.
   - Security history and attack surface.
   - Maintenance activity, release discipline, and bus factor.
   - License and policy compatibility.
   - Transitive dependency count and install scripts.
   - Package size, runtime cost, memory cost, and platform compatibility.
   - Type quality, API ergonomics, and testability.
   - Ecosystem use and migration history.
   - Lock-in, removal cost, and replacement options.
   - Total maintenance cost for this repository.
6. Verify current facts from official documentation, the package registry, source repository, changelog, and advisory sources when network access is available.
7. Recommend the option with the lowest total risk and complexity, not automatically the option with the least code or highest popularity.
8. State the exact package version or local scope, expected lockfile impact, and verification plan.
9. Ask for approval before implementation.

## Local implementation threshold

Prefer a local implementation only when all are true:

- The behavior is short and fully specified.
- Edge cases are few and understood.
- The code is not security-sensitive.
- The implementation can be exhaustively or strongly tested.
- Maintenance cost is lower than dependency and supply-chain cost.
- No standards compliance burden is being underestimated.

## Output

```text
Capability required
Options considered
Comparison table
Security and supply-chain notes
Recommendation
Exact change proposed
Verification
Approval needed
```
