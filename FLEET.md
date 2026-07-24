# Fleet: my curated agent skills

The single list of skills I run, where each comes from, and how it updates. This
is both the install script and the "lockfile": run it to install, re-run it to
update. Replace `eshlox/skills` with your actual repo, and confirm each
third-party source and skill name before relying on it (the ecosystem moves fast).

## Relationship legend

- **own** - mine, lives in `eshlox/skills`. No upstream to track.
- **depend** - installed unmodified from someone else's repo. Updates are free: re-run its command and you get their latest.
- **fork** - copied into my repo and edited. Updates are manual: diff upstream since the recorded commit and re-merge. Record the commit or the fork is a dead end.
- **built-in** - already available in my agent. Do not install, do not duplicate; just decide which skill wins each job.

## How to use this file

- **Install / refresh everything:** run the commands in sections 1 and 2.
- **Update:** run them again. Each source pulls its own latest independently, from its own origin.
- **Pin a version:** append a git ref to freeze it (the `skills` CLI accepts git URLs, e.g. a `#<tag-or-commit>` suffix). Do this for any dependency you do not want moving under you.
- **After a big borrowed update:** re-check for trigger overlap with my spine (regenerate trigger evals with the `skill-creator` skill if I want to measure it).
- `-g` installs globally (all projects). Drop it to install into the current project only.

## 1. Spine (own)

```bash
pnpm dlx skills add -g eshlox/skills
```

Installs: `plan-change`, `implement-change`, `review-change`, `verify-change`,
`evaluate-dependency`, `product-review`, `article-editor`, and
`setup-eshlox-skills`. These are absorbed, not borrowed: I own them and never sync
them from anyone.

## 2. Depend: general engineering (borrow globally, cherry-pick)

Broad, cross-stack sources. Install globally (`-g`) so they apply everywhere, but
browse with `--list` first and add only skills that fill a real gap. Skip anything
that overlaps my spine (plan / implement / review / verify / evaluate-dependency)
or the built-ins in section 4.

```bash
# Anthropic's official skills - broad, high quality
pnpm dlx skills add -g anthropics/skills --list        # browse, then add specific ones

# general engineering skills, TypeScript-leaning
pnpm dlx skills add -g mattpocock/skills --list        # e.g. diagnosing-bugs fills my debugging gap

# animation and design-engineering skills (Emil Kowalski)
pnpm dlx skills add -g emilkowalski/skills --list      # e.g. emil-design-eng, apple-design, animation-vocabulary

# direct, action-first response style, always-on via AGENTS.md
pnpm dlx skills add -g ayghri/i-have-adhd

# optional specialist security (confirm each repo's install method)
pnpm dlx skills add -g semgrep/skills
pnpm dlx skills add -g trailofbits/skills
```

| Source | Use for | Note |
| ------ | ------- | ---- |
| `anthropics/skills` | broad general capabilities | cherry-pick; some overlap the built-ins |
| `mattpocock/skills` | debugging, TS/engineering | `diagnosing-bugs` fills my one real gap |
| `emilkowalski/skills` | animation and design-engineering | cherry-pick; upstream documents `npx skills@latest add`, the same CLI |
| `ayghri/i-have-adhd` | direct, action-first response style | adopted as the default response style in the `AGENTS.md` core block, so it applies always, not only when the skill loads |
| `semgrep/skills`, `trailofbits/skills` | specialist security | optional; may install as plugins |

## 3. Depend: stack packs (borrow PER PROJECT, not global)

Language and framework skills belong in the project that uses them, not in my
global spine. Install them inside the relevant repo (no `-g`), and only when I
actually have a project in that stack. My spine stays stack-agnostic; these add
the stack-specific knowledge on top, per project.

```bash
# inside a Flutter / Dart project
pnpm dlx skills add flutter/skills --list

# inside a project that uses Terraform / infrastructure-as-code
pnpm dlx skills add antonbabenko/terraform-skill --list

# inside a project deployed on Railway
pnpm dlx skills add railwayapp/railway-skills --list

# inside a project on Cloudflare (Workers, Pages, edge)
pnpm dlx skills add cloudflare/skills --list

# for any other stack: add its source here and install it inside that project
```

| Stack | Source | When to install |
| ----- | ------ | --------------- |
| Flutter / Dart | `flutter/skills` | inside a Flutter repo |
| Terraform / IaC | `antonbabenko/terraform-skill` | inside a repo with Terraform |
| Railway (deploy) | `railwayapp/railway-skills` | inside a Railway-deployed repo |
| Cloudflare (edge / Workers) | `cloudflare/skills` | inside a Cloudflare repo |
| any other stack | add its source when I start such a project | per project |

Caveat: some packs install as a plugin rather than via `pnpm dlx skills add`. Check
each repo's README and adjust the command.

## 4. Built-in / already available (curate, do not install)

These already exist in my Claude Code environment and overlap my spine. The job
here is picking the winner per task, not installing:

| Job | Built-in | My spine | Who wins |
| --- | -------- | -------- | -------- |
| Review a finished change | `code-review`, `/security-review` | `review-change` | `review-change` for a contract-aligned single pass; `code-review` for a whole-branch/PR standards-plus-spec review |
| Prove it works | `verify` | `verify-change` | `verify-change` for acceptance-criteria evidence and defined gates; `verify` for open-ended end-to-end app driving |
| Test-first coding | `tdd` | `implement-change` | `implement-change` for the general build; `tdd` when I want strict red-green-refactor |
| Quality cleanup | `simplify` | `review-change` | complementary; `simplify` applies fixes, `review-change` only reports |

On a fresh machine, confirm these with `/skills` before assuming they are present;
install via `pnpm dlx skills add` only if missing.

## 5. Fork (only when I had to adapt - manual updates)

Empty by default. Add a row only when I copy a third-party skill into my repo and
edit it, so I can re-sync later:

| Skill | Upstream repo | Forked from commit | Why adapted |
| ----- | ------------- | ------------------ | ----------- |
| (none yet) | | | |

## Update checklist

1. Re-run the global installs (sections 1 and 2). Spine and general dependencies
   each pull their own latest.
2. Per project, re-run its stack packs (section 3) inside that repo.
3. For every fork in section 5, diff upstream since the recorded commit, re-merge
   wanted changes, and update the commit.
4. After a notable borrowed update, re-check for trigger overlap with the spine.
5. Keep sections 2 and 3 small. Every borrowed skill is a maintenance and overlap cost.
