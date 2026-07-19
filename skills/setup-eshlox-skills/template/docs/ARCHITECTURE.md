# Architecture

Status: Draft
Last reviewed: [YYYY-MM-DD]
Owner: [person or role]

## System context

[What the system is, who calls it, what it calls, and where its boundary sits. Name external systems that are not in this repository.]

## Design principles

- [A durable principle that shapes the design, with the reason it holds.]

## Components

| Component | Responsibility | Owns | Must not own | Location |
| --------- | -------------- | ---- | ------------ | -------- |
| [Name]    | [What it does] | [Concerns it owns] | [Concerns it must not own] | [Path] |

## Data flow

[The main paths through the system, numbered. Describe how a request or action moves from entry to effect, and which component owns each step.]

## Interfaces and contracts

| Interface | Producer | Consumer | Contract source | Compatibility policy |
| --------- | -------- | -------- | --------------- | -------------------- |
| [Name]    | [Component] | [Component] | [File or spec] | [Semver, internal, generated, ...] |

## Data ownership and lifecycle

- [Where each important kind of data originates, who owns it, and how long it lives.]

## Trust boundaries

[Summarize only as far as architecture needs. Keep the full model in `SECURITY.md`.]

- [Boundary: untrusted input, who validates it, and the resulting effect.]

## Dependency boundaries

Allowed direction:

- [Which component may depend on which, from the actual graph.]

Forbidden coupling:

- [Dependencies that must never exist, and where that is enforced.]

## Performance and scale constraints

[Real gates and budgets, if any: bundle size, latency, throughput, memory. Point to the check that enforces them.]

## Deployment and operations

[How the system is built and deployed, the environments it runs in, and any operational rule an agent must not violate.]

## Known limitations

- [A current limitation a maintainer should know about.]

## Architecture decisions

- `architecture/decisions/<nnnn>-<title>.md` - [one-line summary]
