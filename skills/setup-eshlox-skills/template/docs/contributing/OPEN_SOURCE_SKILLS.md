# Open-Source Skills and Workflows

Use third-party skills selectively. More skills do not automatically produce better code. Overlapping skills can conflict, over-trigger, consume context, and add supply-chain risk. Review the source, license, scripts, hooks, network access, and permissions before installation. Pin a reviewed revision when reproducibility matters.

## Recommended stack

### 1. Superpowers

Repository: https://github.com/obra/superpowers

Best pieces to consider:

- `systematic-debugging` for root-cause work instead of guessing.
- `verification-before-completion` for evidence before success claims.
- `requesting-code-review` and `receiving-code-review` for structured feedback.
- `using-git-worktrees` for isolated parallel work.
- `test-driven-development` when strict test-first development fits the task.

Superpowers also provides brainstorming, detailed planning, subagent execution, and branch-finishing workflows. It is intentionally opinionated and can be heavier than necessary for small tasks. Do not combine its full workflow with another full workflow unless you define which one owns each phase.

Recommended use: install it when you want strong process enforcement. Otherwise borrow only the debugging, review, and verification skills.

### 2. GitHub Spec Kit

Repository: https://github.com/github/spec-kit

Best pieces to consider:

- Constitution for project principles.
- Specification focused on what and why.
- Clarification before planning.
- Technical plan.
- Actionable tasks.
- Consistency analysis before implementation.

Recommended use: large features, new products, cross-team work, migrations, or requirements that need a durable spec. It is usually too much process for a small bug fix or local refactor.

### 3. Addy Osmani's Agent Skills

Repository: https://github.com/addyosmani/agent-skills

Strong selective skills:

- `interview-me` for finding the real requirement before coding.
- `code-simplification` for reducing comprehension cost while preserving behavior.
- `incremental-implementation` for small vertical slices.
- `test-driven-development` for behavior-first implementation.
- `code-review-and-quality` for structured review.
- `security-and-hardening` for trust boundaries, input, authentication, authorization, data, and dependency risk.
- `performance-optimization` for measure-first performance work.
- `documentation-and-adrs` for decisions and durable context.

Recommended use: copy or install only the skills that fill a gap. The custom skills in this package already cover shaping, implementation, dependency evaluation, review, and verification, so installing overlapping versions may create competing instructions.

### 4. Semgrep Skills

Repository: https://github.com/semgrep/skills

Recommended use: focused static security analysis, writing or applying Semgrep rules, and repeatable security checks. Treat scanner output as evidence to triage, not automatic proof that code is safe or vulnerable.

### 5. Trail of Bits Skills

Repository: https://github.com/trailofbits/skills

Recommended use: specialist security review, differential review, cryptography, smart contracts, fuzzing, and high-risk code. These are most valuable when the task actually involves those domains.

### 6. OWASP Secure Agent Playbook and Agentic Skills Top 10

Projects:

- https://github.com/OWASP/secure-agent-playbook
- https://github.com/OWASP/www-project-agentic-skills-top-10

Recommended use: structured OWASP-grounded security reviews, dependency and secret checks, API and web security procedures, and security review of agent skills themselves. Review every skill and script before enabling it, especially skills that can execute commands or retrieve remote content.

### 7. MADR and Diataxis

Projects:

- https://adr.github.io/madr/
- https://diataxis.fr/

These are documentation methods, not coding-agent skill packs.

Use MADR for concise architecture decision records. Use Diataxis when public or internal documentation grows large enough to need a clear separation between tutorials, how-to guides, reference, and explanation.

## Principles incorporated without requiring installation

This package already incorporates several widely repeated high-value ideas:

- Explore and understand before coding.
- Define the goal, context, constraints, and completion evidence.
- Use a human approval gate for material decisions, not routine details.
- Keep permanent instructions short and move procedures to on-demand skills.
- Prefer surgical diffs and boring implementations.
- Measure simplicity by comprehension, not character count.
- Use tests and runtime evidence instead of confidence statements.
- Use a fresh context for independent review when risk justifies it.
- Record durable decisions, not every conversation.

## Selection rule

Before installing a skill pack, answer:

1. Which recurring failure does it solve?
2. Does an existing project skill already solve it?
3. What files, scripts, hooks, tools, and network actions does it introduce?
4. Who maintains it, how active is it, and what revision will be pinned?
5. How will its behavior be tested on this repository?
6. How will it be removed if it adds noise or conflicts?

Do not install a pack merely because it is popular or comprehensive.
