---
name: product-review
description: >
  Full-repository product and UX review skill. Reviews an entire codebase and its
  user-facing surfaces (web, mobile, API, docs, onboarding, settings) and produces an
  evidence-backed verdict on what is strong, what is weak, what should be removed,
  merged, simplified, added, or standardised - plus a prioritised plan. Use this skill
  whenever the user asks to review, audit, critique, or evaluate a repository, app,
  API, feature set, product flow, UX, information architecture, navigation, settings,
  onboarding, or documentation; asks "what should I cut / simplify / focus on";
  asks whether a product is too complex or missing something; or asks to compare
  their product against best-in-class standards (Linear, Stripe, Apple, Vercel,
  GitHub, Figma). Trigger even if the user only says "look at my repo and tell me
  what you think" or "make this product better". This is a product/UX review, not a
  code-style lint and not a visual-design pass.
---

# Product Review

Review an entire repository the way a great product organisation would: find what earns
user trust, expose what erodes it, and produce the smallest coherent set of changes that
makes the product shine. The output is judgement backed by evidence - never taste,
never a wall of nitpicks, never a magic score.

**Scope**: features, flows, user jobs, information architecture, navigation, options,
settings, states, onboarding, API contracts, docs, and product focus.
**Out of scope**: code formatting, micro visual aesthetics (pixel colours, font pairing),
and refactors with no user-visible or contract-visible effect - unless the user asks.

---

## 1. Operating principles (non-negotiable)

1. **Evidence, not taste.** Every judgement cites a file, screen, route, spec, doc,
   standard, or precedent. Never write "this feels wrong" without showing where and why.
2. **Separate facts from decisions.** State what you observed (fact), then the verdict
   (decision), explicitly. Mark assumptions as assumptions.
3. **Shipped code is evidence, not automatic precedent.** Existing patterns may be the
   bug. Ask "does this serve the user job?" before "is this consistent?".
4. **Smallest coherent intervention.** Prefer the minimal change that resolves the issue
   over redesigns. Removal beats addition. Simplification beats configuration.
5. **Preserve what works.** Every review must name strengths worth protecting. A review
   that only criticises destroys trust and loses the product's identity.
6. **No mode drift.** An audit never silently becomes a redesign. A UX pass never
   mutates architecture. Resolve the mode first (Section 2) and stay in it.
7. **No composite scores.** Never output "72/100". Use per-dimension judgements with
   severity + confidence, each traceable to evidence.
8. **No compliance theatre.** Accessibility, consistency, and API governance matter
   because they serve users - flag real user impact, not checkbox violations.
9. **Declare coverage gaps.** End every review by listing what you did NOT examine
   (surfaces, states, files, flows) so the user knows the limits of the verdict.

## 2. Resolve the mode first

Before touching files, classify the request into exactly one primary mode:

| Mode | User intent | Output |
|---|---|---|
| **Audit** | "Review this / what's good & bad" | Full structured report (Section 6) |
| **Explain** | "Why is X a problem?" | Deep dive on one finding with evidence |
| **Compare** | "Is this consistent / how do others do it?" | Pattern comparison across repo or vs. gold standards |
| **Plan** | "What should I do about it?" | Prioritised action plan (Section 7) |
| **Enforce** | "Make this a rule / prevent regressions" | Repository-native standard (Section 8) |

If ambiguous, default to **Audit** and say so. Never mix modes silently.

## 3. Repository reconnaissance (before any judgement)

Build layered context. Do not review from a single file or a diff.

1. **Repo-wide layer**: README, AGENTS.md / CLAUDE.md, CONTRIBUTING, architecture docs,
   package manifests, monorepo layout. Extract: what the product claims to be, who it's
   for, and the stated principles. Nearby explicit guidance (AGENTS.md, path-level docs)
   outranks inferred convention.
2. **Surface inventory**: enumerate every user-facing surface - web routes/pages, mobile
   screens, API endpoints/spec, CLI commands, settings screens, onboarding flows,
   emails/notifications, docs site, error pages. List them explicitly in the report.
3. **Path-specific layer**: per-directory conventions (design system, API module, mobile
   app) - these vary and must be reviewed against their own local rules.
4. **The user job**: state in one sentence, per surface, the job the user hires it for.
   If you cannot state the job, that is itself a top finding.
5. **Rendered evidence when available**: URLs, screenshots, preview deployments, Figma
   links. Many real problems (empty states, dead zones, confusing navigation) are only
   visible rendered. If none is available, say so in coverage gaps and review flows from
   routes, components, and copy strings instead.

## 4. What to review (the seven dimensions)

Review each dimension only where it applies; skip and note irrelevant ones.

### 4.1 User job clarity
- Can a new user tell in 10 seconds what this product does and what to do first?
- Does every top-level surface map to a real user job, or to internal org structure?
- Is there one primary action per screen, or competing calls to action?

### 4.2 Information architecture & navigation
- Count top-level navigation items. More than ~5 is a finding; justify each.
- Flag: redundant "Home" tabs, duplicate paths to the same content, unclear labels,
  features reachable only through hidden menus, orphan pages.
- Grouping should follow user mental models, not team boundaries.

### 4.3 Feature scope (the core of this skill)
For every feature, ask in order:
1. What user job does it serve? (If none stateable → **Remove** candidate.)
2. Is another feature already serving that job? (→ **Merge/Remove**.)
3. Is it used through 3+ options/toggles when one strong default would do? (→ **Simplify**.)
4. Is it half-built or inconsistent with the rest? (→ **Fix or Remove**, never leave half.)
5. Is a critical job unserved? (→ **Add** - the rarest verdict; require strong evidence.)

Bias: a great product is defined by what it refuses to include. Removal and
simplification findings should usually outnumber additions.

### 4.4 Flows & states
Every important flow must handle: **loading, empty, error, permission-denied, billing/
limit-reached, and destructive confirmation**. The happy path is where products look
fine; the edge states are where trust is won or lost. For each key flow, trace it
end-to-end and report which states exist, which are missing, and which are inconsistent.
Destructive actions require: clear labelling, confirmation proportional to severity,
and undo where feasible.

### 4.5 Settings & options discipline
- Every setting is a decision the team refused to make. Flag settings that exist to
  avoid choosing a good default.
- Flag: duplicated settings, settings with no discoverable effect, dangerous settings
  ungated, settings screens with no grouping or search past ~10 items.
- Prefer: strong defaults, progressive disclosure (simple by default, deep on demand).

### 4.6 API & contract quality (when an API exists)
- Separate **contract critique** (naming, resource modelling, error model, status
  semantics, payload shape, versioning, examples) from **implementation critique**.
- Ingest OpenAPI/spec files if present; inconsistency between spec, implementation,
  and docs is a high-severity finding.
- Judge against: predictable resource naming, consistent error envelope, pagination
  and idempotency where relevant, examples for every endpoint. The bar is Stripe-level
  clarity: a developer should succeed from the docs alone.

### 4.7 Docs, onboarding & first-run
- README: can a stranger install, run, and understand the product from it alone?
- Onboarding: what happens on first launch with zero data? Empty states should teach.
- Docs are a surface, not an afterthought - quickstart, reference, and conceptual
  guides each judged on whether the user succeeds without support.

## 5. Verdict taxonomy & finding format

Every finding gets exactly one verdict:

**PRESERVE** · **REMOVE** · **MERGE** · **SIMPLIFY** · **FIX** · **ADD** · **STANDARDISE**

And every finding answers five questions, in this order:

1. **Observed** - what exists, factually, with location (file/route/screen/endpoint).
2. **Why it matters** - the user or business impact, tied to the user job.
3. **Evidence** - code excerpt, route list, screenshot, spec line, copy string.
4. **Standard / precedent** - the principle applied (e.g. "one primary action per
   screen", "empty states must teach", "consistent error envelope") and, where useful,
   the exemplar (Linear's focused nav, Stripe's error model, Apple's tab guidance).
5. **Smallest next action** - one concrete step, not a redesign essay.

Plus two tags:
- **Severity**: `critical` (blocks/breaks the user job) · `major` (erodes trust or adds
  real friction) · `minor` (polish).
- **Confidence**: `high` (direct evidence) · `medium` (strong inference) ·
  `low` (assumption - state what would confirm it).

Low-confidence critical findings are questions, not verdicts - phrase them as such.

## 6. Fixed report structure (Audit mode)

Always output the same structure, in this order. Prose over bullet-spam; findings are
short and dense. Target: the whole report readable in under 10 minutes.

```
# Product Review: <name>

## Verdict in three sentences
<The honest headline: what this product is, its biggest strength,
 its biggest risk, and the single highest-leverage change.>

## Surfaces reviewed
<Explicit inventory + what was NOT reviewed (coverage gaps).>

## What is strong - preserve this
<3-7 findings. Specific, evidenced. These define the product's identity.>

## What to remove
## What to merge or simplify
## What to fix
## What to add (only if strongly evidenced)
## What to standardise
<Each finding in the 5-question format, severity + confidence tagged.
 Empty sections are stated as empty - that is information too.>

## The plan
<Section 7 format.>

## Coverage gaps & assumptions
<What wasn't examined; assumptions that, if wrong, change verdicts.>
```

## 7. The plan (Plan mode or report tail)

Convert findings into a prioritised sequence, not a backlog dump:

1. **Now (this week)** - critical fixes + free wins (pure removals). Max 5 items.
2. **Next (this cycle)** - simplifications and merges that reshape the product. Max 5.
3. **Later** - additions and standardisation. Everything else is explicitly **dropped,
   not deferred** - say which findings you are choosing not to act on and why.

Each item: verdict, one-line action, affected surface, expected user-visible effect,
and rough size (S/M/L). Sequence by leverage: remove before simplify, simplify before
fix, fix before add. Fixed time, variable scope: if an item grows, cut its scope, not
the deadline.

## 8. Enforce mode - make wisdom repository-native

One-off advice decays; standards compound. When the user accepts a finding as a rule:

- Write it into the repository where agents and humans will find it: root `AGENTS.md`
  (or CLAUDE.md) for repo-wide rules, path-level `AGENTS.md` for surface-specific rules.
  Nearby explicit guidance beats hidden cleverness - prefer a plain, readable docs
  index over elaborate machinery.
- Record **accepted decisions with their reasoning** ("we removed X because…"), not just
  the rule - future reviewers need the why.
- Capture **exemplars**: point to the best existing screen/endpoint/flow as the
  canonical pattern ("do it like `settings/billing`").
- Keep a visible **coverage gaps** section: what the standards do not yet cover.
- Where the platform supports it, convert findings into typed issues with owner,
  severity, and the smallest-next-action as the issue body.

## 9. The quality bar (gold standards to judge against)

Distilled from the products and thinkers that define the bar. Use these as named
standards in findings:

- **Focus (Linear)**: a small number of opinionated views beats infinite configurability;
  the backlog is curated, not hoarded; saying no is a feature.
- **Developer clarity (Stripe)**: docs and API teach by example; errors tell you what to
  do next; a stranger succeeds without support.
- **Simplicity through removal (Apple)**: extra tabs add complexity; remove redundant
  navigation; structure follows content hierarchy, not org chart.
- **Whole-context judgement (Sourcegraph/Cursor/GitHub)**: never judge from a diff or a
  single file; understand the pattern across the repository first.
- **Rendered truth (Vercel/Figma)**: review the running product and its states, not just
  the source; decisions and their reasoning live next to the code.
- **Don't make me think (Krug)**: if a user must reason about navigation or labels, the
  design failed - obviousness is the bar.
- **Heuristic language (Nielsen/NN-g)**: visibility of status, user control, consistency,
  error prevention, recognition over recall, minimalist design - use these terms so
  findings are precise and teachable.
- **Problem first (Cagan/Olsen)**: every feature must trace to a valuable, usable,
  feasible solution to a real user problem; otherwise it's scope, not product.
- **Shaped work (Singer)**: recommendations come shaped - bounded, risk-targeted,
  fixed-appetite - never as open-ended "improve everything" mandates.
- **Practical craft (Wathan/Schoger)**: hierarchy, spacing, and de-emphasis solve most
  "cluttered" complaints without adding anything.

## 10. Anti-patterns - what this review must never do

- **The everything-report**: 90 undifferentiated comments. Cap at ~25 findings; fold the
  rest into standards or drop them. Signal over completeness.
- **The magic score**: any single number summarising product quality.
- **Uncited opinion**: any verdict without file/screen/spec evidence.
- **Redesign creep**: proposing a new product instead of reviewing this one.
- **Lint wall**: elevating convention violations above user-job failures.
- **Addition bias**: recommending new features as the default fix. The default fix is
  removal or a better default.
- **Backend noise in UX review**: internal-only changes with no user- or
  contract-visible effect are out of scope unless asked.
- **False confidence**: presenting assumptions as findings. Tag confidence honestly;
  turn low-confidence criticals into questions for the user.
- **Ignoring strengths**: a review with an empty PRESERVE section is a broken review.

## 11. Quick-run checklist

1. Resolve mode (Section 2). State it.
2. Reconnaissance: repo-wide → surfaces inventory → path rules → user job per surface.
3. Review applicable dimensions (Section 4); trace 2-3 critical flows end-to-end
   including edge states.
4. Draft findings in the 5-question format; assign verdict, severity, confidence.
5. Cut to the strongest ~25; ensure PRESERVE is populated; ensure removals ≥ additions
   unless evidence demands otherwise.
6. Emit the fixed report (Section 6) with the plan (Section 7) and coverage gaps.
7. Offer Enforce mode: "want any of these as repository standards?"
