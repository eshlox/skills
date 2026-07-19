# AI Coding Workflow

This repository uses one shared operating contract for coding agents such as Claude Code, Codex, OpenCode, and Grok. The permanent rule file stays concise. Detailed procedures load only when the task needs them. Durable project knowledge lives under `docs/`.

The baseline is distributed as agent skills, installed with `pnpm dlx skills add`, and has two parts matched to two different needs:

- The always-on contract and the documentation scaffold are planted into the repository by the `setup-eshlox-skills` skill, because they must live in the repo and be versioned with the code. That skill works interactively: it inspects the repo, proposes the changes, and confirms with you before writing.
- The task workflows are ordinary agent skills, loaded on demand when their description matches the task rather than sitting in context all the time.

## Why this structure

- `AGENTS.md` is the canonical cross-agent contract. Its top block is managed by the setup-eshlox-skills skill. Its project section is owned by this repository.
- `.claude/CLAUDE.md` imports the canonical contract for Claude Code without duplicating it.
- The workflow skills (`shape-change`, `implement-change`, `evaluate-dependency`, `review-change`, `verify-change`) are installed separately as agent skills and discovered by each agent natively.
- `docs/` separates current project truth, decisions, plans, and unapproved ideas.
- `AI_TASK_TEMPLATE.md` gives each task an explicit goal, context, constraints, scope, and definition of done.

A prose rule is guidance, not a guarantee. Put non-negotiable controls in permissions, hooks, CI, linters, type checking, tests, dependency policies, secret scanning, and branch protection.

## Install and update

Add the skills to your coding agents once:

```bash
pnpm dlx skills add eshlox/skills
```

Then, inside a project, ask the agent to run the setup skill:

```text
Use the setup-eshlox-skills skill to install the operating contract and docs in this repo.
```

That skill inspects the repo, proposes what it will add, and after you confirm writes the managed contract, creates the `docs/` templates only where they are missing, and refreshes the managed block of `AGENTS.md` while preserving your project section. Install and update are the same operation, so running the skill again later pulls contract and doc-scaffold improvements without overwriting documentation you have filled in.

To update everything: re-run `pnpm dlx skills add` for the latest skills, then run `setup-eshlox-skills` again for the latest contract and docs.

After the first run, complete the project section of `AGENTS.md` and the bracketed sections of `docs/PROJECT.md`, `docs/ARCHITECTURE.md`, `docs/QUALITY.md`, and `docs/SECURITY.md`. Delete template sections that are not relevant. Commit the result so every agent and teammate receives the same rules.

## Tool setup

### Claude Code

Claude Code loads `.claude/CLAUDE.md`, which imports `AGENTS.md`. `pnpm dlx skills add` installs the workflow skills where Claude Code discovers them, so you can invoke one by name, for example:

```text
Use the shape-change skill for this task.
```

### Codex

Codex loads `AGENTS.md`. `pnpm dlx skills add` installs the skills into Codex's skill directory, so invoke one by name, for example `$shape-change`, or name the workflow in the prompt when the interface does not expose skill invocation.

### OpenCode

OpenCode loads `AGENTS.md` instead of `CLAUDE.md` when both exist, and discovers installed skills automatically. Use its plan agent for read-only shaping and its build agent only after the material decisions are approved.

### Grok

Grok loads root `AGENTS.md`. Install the skills with `pnpm dlx skills add`, or point Grok at the skill directory it was installed into via the `[skills] paths` list in the user Grok configuration.

## Daily flow

### Small, clear change

Use `AI_TASK_TEMPLATE.md`, but keep the task compact. Include the exact behavior and the check that proves completion.

```text
Fix the logged-out edge case in the session module.
Done when the existing failure is reproduced by a focused test, the test passes after the fix, and unrelated authentication behavior is unchanged.
Do not refactor the session module or add dependencies.
```

The agent should inspect, state a brief approach, implement, review the diff, update changed documentation, and verify.

### Non-trivial or ambiguous change

Start with:

```text
Use the shape-change skill.
Do not edit code yet. Interview me about material uncertainty, challenge weak assumptions, compare credible solutions, recommend the simplest proven option, and wait for approval.
```

After approval:

```text
Write the approved plan to docs/plans/ using the template, then use the implement-change skill. Stop and ask if implementation reveals a new material decision.
```

### Review and completion

Use a fresh agent session when the risk or size justifies it. A reviewer that did not write the code is less anchored to the implementation.

```text
Read the approved task or plan and use the review-change skill.
Review only. Find scope creep, correctness defects, security issues, unnecessary complexity, weak tests, stale documentation, and unsupported performance claims.
```

Then run:

```text
Use the verify-change skill and map every acceptance criterion to evidence.
```

## Approval policy

Do not require confirmation for every line, helper, test, or documentation edit. That creates ceremony and trains the agent to treat ordinary engineering decisions as user decisions.

Require approval for material scope, behavior, APIs, data, dependencies, architecture, security, compatibility, operations, destructive actions, and meaningful trade-offs. Let the agent decide routine details inside the approved direction by following existing project patterns.

## Documentation policy

The goal is one reliable source for every durable fact, not one giant file and not a transcript of every discussion. `docs/README.md` is the authority map. Update documentation in the same change only when its truth changes. Avoid restating code that is already clear from names, types, tests, and structure.

## Hard controls worth adding

Adapt these to the repository instead of relying on agent prose:

- Ask or deny permission for package installation, Git push, destructive shell commands, migrations, production access, and secret access.
- Require lockfile consistency and an approved package manager in CI.
- Require focused tests, type checking, linting, build checks, dependency scanning, and secret scanning before merge.
- Use branch protection and required review for high-risk paths.
- Use formatters and linters for mechanical style. Do not spend instruction tokens on rules a tool can enforce.
- Add path-scoped rules only for genuine subsystem differences.

## Maintaining the rules

Add a permanent rule when an agent repeats the same mistake, a review exposes missing repository knowledge, or every future contributor needs the fact. Do not add one-off corrections, temporary task detail, or information inferable from the repository.

Repository-specific rules belong in the project section of `AGENTS.md`, not in the managed block, so re-running `setup-eshlox-skills` does not overwrite them. Propose a change to the managed block upstream in eshlox/skills when it would help every project.

## Source material

This system synthesizes current official guidance and maintained open-source workflows:

- Anthropic Claude Code memory and best practices: https://code.claude.com/docs/en/memory and https://code.claude.com/docs/en/best-practices
- OpenAI Codex best practices and skills: https://developers.openai.com/codex/learn/best-practices and https://developers.openai.com/codex/build-skills
- OpenCode rules and skills: https://opencode.ai/docs/rules/ and https://opencode.ai/docs/skills/
- Grok project rules and skills: https://docs.x.ai/build/features/project-rules and https://docs.x.ai/build/features/skills-plugins-marketplaces
- Agent Skills open format: https://agentskills.io
- AGENTS.md open format: https://agents.md
- Superpowers: https://github.com/obra/superpowers
- GitHub Spec Kit: https://github.com/github/spec-kit
- Addy Osmani's agent skills: https://github.com/addyosmani/agent-skills
- HumanLayer advanced context engineering: https://www.humanlayer.dev/blog/advanced-context-engineering-for-coding-agents
- MADR decision records: https://adr.github.io/madr/
- Diataxis documentation framework: https://diataxis.fr/
