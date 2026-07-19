# skills

My agent skills (`eshlox/skills`): a language and framework agnostic engineering
baseline for coding agents (Claude Code, Codex, OpenCode, Grok), distributed
entirely as agent skills and installable with `pnpm dlx skills add eshlox/skills`.

It has two parts:

- **Workflow skills** - `plan-change`, `implement-change`, `evaluate-dependency`,
  `review-change`, `verify-change`. Bare, descriptive names, loaded on demand
  when their description matches the task.
- **`setup-eshlox-skills`** - a skill that installs and updates the always-on
  operating contract (`AGENTS.md`) and the `docs/` scaffold in a project. It works
  interactively: explore, propose, confirm, then write.

Nothing here assumes a language, framework, or package manager. Per-repo tooling
lives only in the project section of `AGENTS.md` and in `docs/QUALITY.md`.

`FLEET.md` is the curated list of every skill you run (this spine plus borrowed
specialist skills), marked by relationship (own / depend / fork / built-in). It
doubles as the install script and the update loop: run it to install, re-run it
to update.

## Naming and namespacing

Agent skills install into a flat, per-agent directory keyed by a bare `name`;
there is no npm-style `@scope`. So the convention is:

- **Workflow skills use bare descriptive names.** The namespace is the install
  source (`pnpm dlx skills add eshlox/skills`), not the skill name.
- **The setup skill is prefixed**, because `install`/`update`/`setup` are
  high-collision generic verbs. `setup-eshlox-skills` namespaces them so they are
  unmistakably yours and collision-free.

Rename `eshlox` to your own handle or org to make the kit yours: rename the
`skills/setup-eshlox-skills/` directory and update the `name:` in its `SKILL.md`.

## Install into a project

```bash
# 1. Add the skills to your coding agents (use -g for all projects)
pnpm dlx skills add eshlox/skills

# 2. Inside a project, ask the agent:
#    "Use the setup-eshlox-skills skill to install the contract and docs here."
```

The setup skill writes the managed files, seeds the `docs/` templates only where
they are missing, and merges `AGENTS.md`. Then complete the project section of
`AGENTS.md` and the bracketed parts of the `docs/` files, and commit.

## Update

Re-run `pnpm dlx skills add` for the latest skills, then run `setup-eshlox-skills`
again. Install and update are the same idempotent operation:

- Managed files (the `AGENTS.md` core, `.claude/`, `docs/README.md`, meta-docs,
  templates) are overwritten so improvements propagate.
- Seed docs (`docs/PROJECT.md`, `ARCHITECTURE.md`, `QUALITY.md`, `SECURITY.md`,
  `IDEAS.md`, `documentation-style.md`) are created if missing and never
  overwritten.
- `AGENTS.md` is merged: only the block between `ESHLOX:CORE:START` and
  `ESHLOX:CORE:END` is refreshed; the project section below is preserved. A
  hand-written `AGENTS.md` with no markers is never clobbered - the setup skill
  writes `AGENTS.md.eshlox-new` beside it for a manual merge.

## Repository layout

```
skills/                          # repo root (eshlox/skills)
├── skills/                      # the installable skills (pnpm dlx skills add reads here)
│   ├── plan-change/SKILL.md
│   ├── implement-change/SKILL.md
│   ├── evaluate-dependency/SKILL.md
│   ├── review-change/SKILL.md
│   ├── verify-change/SKILL.md
│   └── setup-eshlox-skills/
│       ├── SKILL.md             # interactive explore -> propose -> confirm -> write
│       └── template/            # AGENTS.md, .claude/, docs/ starting files
├── FLEET.md                     # curated install/update list (spine + borrowed)
└── README.md
```

## Why the contract is a skill, not a workflow

The contract is always-on governance and belongs in `AGENTS.md` (memory every
action sees), not in an on-demand skill. So it is not one of the workflow skills;
instead `setup-eshlox-skills` plants and updates it. That setup skill is prose:
it explores the repo, proposes what it will change, confirms with you, then writes
the managed files, seeds `docs/` only where missing, and refreshes only the marked
core block of `AGENTS.md`. The `CORE:START`/`CORE:END` markers keep updates safe -
the skill replaces only that block and leaves your project section untouched.

## Private use, no npm publish

`pnpm dlx skills add` reads GitHub (and other git hosts) directly, so a private repo
is enough. Install globally for every project:

```bash
pnpm dlx skills add -g eshlox/skills
```

If your skills CLI version does not copy bundled files, install with the copy
mode it documents (for example `--copy`) so the `template/` folder lands
alongside the skill.

## How the pieces fit

See `skills/setup-eshlox-skills/template/docs/contributing/AI_WORKFLOW.md` for
the full model: why the contract is short, when a skill loads, how the
documentation authority map works, and how to wire each agent tool.
