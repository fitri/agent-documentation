# Project Development and Documentation Standard

## Purpose

This file is a reusable bootstrap standard for AI-assisted development.
It applies to projects such as CLI tools, APIs, plugins, automation, and
configuration projects.

An agent given this file must use it to initialize and maintain a small,
consistent project documentation structure. The structure is shared memory
between agents and developers; it is not a replacement for source code,
tests, CLI help, or generated API documentation.

Keep this standard simple. Create only the files required by the project.
Do not create empty files merely to match the structure.

## Standard source

- Repository: <https://github.com/fitri/agent-documentation>
- Standard file: `DEVELOPMENT-STANDARD.md`

Use a tagged release when updating this standard in another project. Do not
automatically pull an unspecified or moving `latest` version.

## Bootstrap

When initializing a project:

1. Read this file completely.
2. Inspect the repository and existing documentation before editing.
3. Create the project-level `AGENTS.md`.
4. Create the mandatory files under `docs/dev/`.
5. Populate them with the project's actual context. Do not invent missing
   requirements or architecture.
6. Tell the user which assumptions or unanswered questions remain.

If this file was downloaded from a versioned standard repository, record the
source URL and version in `AGENTS.md`. Do not silently replace a project with
the latest standard version.

## Required structure

```text
project/
├── AGENTS.md
└── docs/
    └── dev/
        ├── PLAN.md
        ├── ARCHITECTURE.md
        ├── SPEC.md
        ├── CONSTRAINTS.md
        └── USER.md
```

The project-level `AGENTS.md` is the agent entry point. The files in
`docs/dev/` contain project-specific knowledge.

## File inventory

| Filename                  | Mandatory | Conditional | Temporary | Path                       | Purpose                            |
|---------------------------|-----------|-------------|-----------|----------------------------|------------------------------------|
| `DEVELOPMENT-STANDARD.md` | Yes*      | No          | No        | Project root or `standard/` | Defines this workflow              |
| `AGENTS.md`               | Yes       | No          | No        | Project root               | Directs agents through the project |
| `PLAN.md`                 | Yes       | No          | No        | `docs/dev/`                | Defines project intent and goals   |
| `ARCHITECTURE.md`         | Yes       | No          | No        | `docs/dev/`                | Describes system structure        |
| `SPEC.md`                 | Yes       | No          | No        | `docs/dev/`                | Defines required behavior         |
| `CONSTRAINTS.md`          | Yes       | No          | No        | `docs/dev/`                | Defines non-negotiable boundaries |
| `USER.md`                 | Yes       | No          | No        | `docs/dev/`                | Provides a short user guide       |
| `CHANGELOG.md`            | No        | Yes         | No        | `docs/dev/`                | Records changes by release        |
| `TEST.md`                 | No        | Yes         | No        | `docs/dev/`                | Defines verification procedures   |
| `ADR/*.md`                | No        | Yes         | No        | `docs/dev/ADR/`            | Records significant decisions     |
| `TASK.md`                 | No        | No          | Yes       | `docs/dev/`                | Tracks active implementation work |
| `HANDOFF.md`              | No        | No          | Yes       | `docs/dev/`                | Transfers incomplete work         |

`*` The standard is required during initialization. A project may keep its
versioned copy for future reference or remove it after the workflow is
established, provided `AGENTS.md` records where the authoritative standard
comes from.

## File responsibilities

### `AGENTS.md`

Explains how an agent should work in this repository. It must include:

- A brief project overview.
- The location of this standard.
- The location and purpose of `docs/dev/`.
- The required reading order.
- Testing and completion expectations.
- Any project-specific agent restrictions.

It should route an agent to project knowledge, not duplicate all project
requirements.

### `docs/dev/PLAN.md`

Defines why the project exists, its goals, scope, priorities, assumptions,
and definition of success.

### `docs/dev/ARCHITECTURE.md`

Describes the system at a structural level: major components, boundaries,
data flow, integrations, storage, interfaces, and important dependencies.

### `docs/dev/SPEC.md`

Defines observable behavior. Requirements should be specific and testable.
Give important requirements stable identifiers, such as `AUTH-001`, so tasks
and tests can refer to them without copying their text.

### `docs/dev/CONSTRAINTS.md`

Defines boundaries that implementation must not violate, including security,
compatibility, technology, performance, resource, and regulatory constraints.

Constraints are hard boundaries. An agent may propose a change, but must not
silently weaken or remove a constraint.

### `docs/dev/USER.md`

Provides a short practical guide for a user: what the project can do, how to
run it, and a few useful first actions. It is not a complete manual. Detailed
reference belongs in CLI help, API documentation, or other generated tooling.

## Documentation boundaries

Keep each document in its own lane. Documents may link to one another, but
must not become duplicate sources of truth.

- `AGENTS.md` gives agent instructions; it does not contain the full project
  specification.
- `PLAN.md` explains intent and scope; it does not define implementation
  details.
- `ARCHITECTURE.md` explains structure and boundaries; it does not prescribe
  every required behavior.
- `SPEC.md` defines observable behavior; it does not describe internal
  implementation choices.
- `CONSTRAINTS.md` defines hard limits; it does not become a general task list.
- `USER.md` explains user operation; it does not replace tests, API reference,
  or internal documentation.
- `TASK.md` tracks current work; it does not become permanent project history.
- `HANDOFF.md` transfers incomplete work; it does not become a second task
  tracker or source of truth.
- `TEST.md` maps behavior to verification; it does not replace executable
  tests.

Avoid oversized `AGENTS.md`, repeated requirements, permanent temporary files,
ADRs for trivial changes, and copying implementation details into
specifications. When information belongs elsewhere, link to that document
instead of duplicating it.

## Conditional files

Create these only when they provide real value:

### `docs/dev/TEST.md`

Create this when agents need a dedicated verification map for the project.
`TEST.md` is for agents to know what to run and what to verify after changes
or when verification is requested. It may cover functional behavior, behavior
described in `USER.md`, acceptance criteria from `SPEC.md`, and selected tests
implemented under directories such as `tests/`.

It should state:

- What behavior or requirement must be proven.
- Which command, test file, suite, or manual procedure to run.
- The expected result and relevant environment.
- Links between requirements, user workflows, and executable tests.

`TEST.md` describes the verification strategy and commands; the executable
tests remain in the project's normal test infrastructure.

### `docs/dev/ADR/`

Create this directory when the project makes its first significant technical
decision involving architecture, dependencies, security, data, public
interfaces, or long-term maintenance.

Use numbered, uppercase, hyphen-separated names:

```text
docs/dev/ADR/001-USE-SQLITE.md
```

An ADR records the decision, context, alternatives, rationale, consequences,
and status. Do not create ADRs for trivial fixes or private refactors.

### `docs/dev/CHANGELOG.md`

Create this at the first release tag. Group user-meaningful changes by the
released version and GitHub tag. Do not use it as a commit-by-commit diary.

## Temporary files

### `docs/dev/TASK.md`

Create this only when there is active implementation work. It should state
the objective, requirements, affected files, verification, and remaining
work. Delete it after the work is implemented, verified, and reconciled.

### `docs/dev/HANDOFF.md`

Create this only when incomplete work must be continued by another agent.
Record completed work, discoveries, remaining work, tests, and the next action.
The receiving agent must validate it against current project documentation.
After the handoff is consumed and its durable information is reconciled,
delete it.

Temporary files must never become a second source of truth or a permanent
status history.

## Source of truth

Use this order when resolving project conflicts:

1. Explicit user instruction.
2. `CONSTRAINTS.md` as a hard veto.
3. `PLAN.md` for project intent.
4. `SPEC.md` for required behavior.
5. `ARCHITECTURE.md` for system structure.
6. Accepted ADRs for recorded decisions.
7. Existing implementation as evidence of current behavior.

Do not silently choose between conflicting documents. Identify the conflict,
resolve it deliberately, and update the affected source of truth.

## Change workflow

### Trivial changes

For typos, renames, and private refactors, make the change and run the
smallest relevant checks. Update documentation only when its meaning changes.

### Standard changes

For behavior or user-facing changes:

1. Read the relevant project documentation.
2. Define or update requirements in `SPEC.md`.
3. Check `CONSTRAINTS.md` and `ARCHITECTURE.md`.
4. Create or update `TASK.md`.
5. Implement the change.
6. Run relevant tests and checks.
7. Update `USER.md` when user behavior changes.
8. Reconcile documentation and remove `TASK.md`.

### Significant changes

For changes to project scope, architecture, security, dependencies, data
models, or public interfaces, also create an ADR and update the affected
permanent documentation before considering the work complete.

For urgent fixes, restore the required behavior first, verify it, and perform
the documentation reconciliation in the same change whenever possible.

## Completion

Before finishing:

- Verify the implementation against `SPEC.md`.
- Verify no `CONSTRAINTS.md` rule was violated.
- Update `PLAN.md` if project intent changed.
- Update `ARCHITECTURE.md` if structure changed.
- Update `USER.md` if user operation changed.
- Update or create `TEST.md` when verification guidance is needed.
- Create an ADR for significant technical decisions.
- Remove completed `TASK.md` and consumed `HANDOFF.md`.

The project is complete only when its code and permanent documentation
describe the same intended system.
