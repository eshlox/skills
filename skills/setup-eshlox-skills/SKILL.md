---
name: setup-eshlox-skills
description: Install or update the eshlox engineering baseline in a repository - the always-on operating contract (AGENTS.md) and the docs/ scaffold. Use when the user asks to install, set up, add, or update the eshlox kit, the agent kit, the operating contract, or the AGENTS.md baseline in a project.
disable-model-invocation: true
---

# setup-eshlox-skills: install or update the operating baseline

This skill plants and updates two things in the current repository:

- `AGENTS.md` - the always-on engineering operating contract.
- `docs/` - the documentation scaffold (authority map, templates, plans, decisions).

The workflow skills (`shape-change`, `implement-change`, `evaluate-dependency`, `review-change`, `verify-change`) are separate agent skills and are not planted here.

Install and update are the same operation. On a fresh repo it installs; run again later and it refreshes the shared parts while leaving your own edits alone.

The starting files live in `template/`, bundled next to this `SKILL.md`. Treat them as the source of truth for the managed files and as first-draft scaffolding for the seed files. Work interactively: explore, propose, confirm, then write. Never overwrite a file the rules below say to preserve.

## Step 1: Explore

Before writing anything, inspect the repository and note:

- Whether `AGENTS.md` already exists, and if so whether it contains the markers `<!-- ESHLOX:CORE:START -->` and `<!-- ESHLOX:CORE:END -->`.
- Whether `.claude/CLAUDE.md` exists and whether it already imports `AGENTS.md`.
- Which of the `docs/` files already exist.
- Signals that change wording: the package manager and language, whether this is a monorepo, and any existing documentation conventions.

## Step 2: Propose

Summarize what you will do, grouped by the three categories below, and list every file you will write, merge, keep, or skip. If `AGENTS.md` exists without the markers, flag that it will not be overwritten. Ask any question whose answer changes the result. Keep it short.

## Step 3: Confirm

Show the user the plan (and, for `AGENTS.md`, the exact core block you will insert if the file already exists) and wait for approval before writing. Do not write files in this step.

## Step 4: Write

Apply these rules exactly.

**Managed files** - overwrite with the bundled `template/` version so updates propagate:

- `AGENTS.md` (managed block only, see below)
- `.claude/commands/improve-docs.md`
- `docs/README.md`
- `docs/contributing/AI_WORKFLOW.md`
- `docs/contributing/OPEN_SOURCE_SKILLS.md`
- `docs/contributing/AI_TASK_TEMPLATE.md`
- `docs/plans/README.md`
- `docs/plans/template.md`
- `docs/architecture/decisions/README.md`
- `docs/architecture/decisions/0000-template.md`

**Seed files** - create only if missing, never overwrite (they hold project-owned truth):

- `docs/PROJECT.md`
- `docs/ARCHITECTURE.md`
- `docs/QUALITY.md`
- `docs/SECURITY.md`
- `docs/IDEAS.md`
- `docs/contributing/documentation-style.md`

**AGENTS.md** - the special case:

- If it does not exist: write the bundled `template/AGENTS.md` whole.
- If it exists and contains both `ESHLOX:CORE:START` and `ESHLOX:CORE:END`: replace only the text between and including those two markers with the bundled core block. Leave everything before and after the markers byte-for-byte unchanged. That is how the project section below the end marker is preserved.
- If it exists but has no markers: do not overwrite it. Write the bundled contract to `AGENTS.md.eshlox-new` beside it and tell the user to merge by hand.

**.claude/CLAUDE.md** - ensure it imports the contract without destroying existing memory:

- If absent: create it containing the single line `@../AGENTS.md`.
- If present but it does not import `AGENTS.md`: add the import line. Do not remove or rewrite the user's existing content.
- If present and already importing `AGENTS.md`: leave it.

## Step 5: Report and hand off

State what you wrote, merged, kept, and skipped, plus any `AGENTS.md.eshlox-new` file. Then tell the user to:

1. Install the workflow skills: `pnpm dlx skills add eshlox/skills`.
2. Complete the project section of `AGENTS.md` (package manager, install command, the skills install command) and the bracketed parts of `docs/PROJECT.md`, `docs/ARCHITECTURE.md`, `docs/QUALITY.md`, `docs/SECURITY.md`.
3. Delete template sections that do not apply, then commit.
