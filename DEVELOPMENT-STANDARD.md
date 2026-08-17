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

In an existing project, preserve accurate documentation and edit it
surgically. Map existing documents into the appropriate lanes and link to
them instead of duplicating them. Extend an existing `AGENTS.md` rather than
replacing it.

If this file was downloaded from a versioned standard repository, record the
source URL and version in `AGENTS.md`. Do not silently replace a project with
the latest standard version.

## Required structure

```text
project/
├── AGENTS.md
├── CHANGELOG.md                 (conditional; when the ecosystem expects it)
└── docs/
    └── dev/
        ├── PLAN.md
        ├── ARCHITECTURE.md
        ├── SPECIFICATIONS.md
        ├── CONSTRAINTS.md
        └── USER.md
```

The project-level `AGENTS.md` is the agent entry point. The files in
`docs/dev/` contain project-specific knowledge.

## File inventory

| Filename                  | Lifecycle   | Path           | Purpose                            |
|---------------------------|-------------|----------------|------------------------------------|
| `DEVELOPMENT-STANDARD.md` | Required*   | Project root   | Defines this workflow              |
| `AGENTS.md`               | Required    | Project root   | Directs agents through the project |
| `PLAN.md`                 | Required    | `docs/dev/`    | Defines project intent and goals   |
| `ARCHITECTURE.md`         | Required    | `docs/dev/`    | Describes system structure        |
| `SPECIFICATIONS.md`       | Required    | `docs/dev/`    | Defines required behavior         |
| `CONSTRAINTS.md`          | Required    | `docs/dev/`    | Defines non-negotiable boundaries |
| `USER.md`                 | Required    | `docs/dev/`    | Provides a short user guide       |
| `CHANGELOG.md`            | Conditional | Project root   | Records changes by release        |
| `TEST.md`                 | Conditional | `docs/dev/`    | Maps behavior to verification     |
| `ADR/*.md`                | Conditional | `docs/dev/ADR/` | Records significant decisions     |
| `TASK.md`                 | Temporary   | `docs/dev/`    | Tracks active implementation work |
| `HANDOFF.md`              | Temporary   | `docs/dev/`    | Transfers incomplete work         |

`*` The standard is required during initialization. A project may keep its
versioned copy for future reference or remove it after the workflow is
established, provided `AGENTS.md` records where the authoritative standard
comes from.

Required files must contain real project information, but may be brief. If a
required file has no meaningful content for a project, explain why in
`AGENTS.md` rather than leaving it empty.

## File responsibilities

### `AGENTS.md`

Explains how an agent should work in this repository. It must include:

- A brief project overview.
- The location and version/tag of this standard.
- The location and purpose of `docs/dev/`.
- The required reading order.
- Baseline verification commands, or a pointer to `TEST.md`.
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

### `docs/dev/SPECIFICATIONS.md`

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
- `SPECIFICATIONS.md` defines observable behavior; it does not describe internal
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
specifications. Never place credentials, tokens, or personal data in project
documentation; describe where they are configured instead. When information
belongs elsewhere, link to that document instead of duplicating it.

## Conditional files

Create these only when they provide real value:

### `docs/dev/TEST.md`

Create this when verification requires more than one obvious command, manual
procedures, special environments, or a non-obvious mapping between
requirements and tests.
`TEST.md` is for agents to know what to run and what to verify after changes
or when verification is requested. It may cover functional behavior, behavior
described in `USER.md`, acceptance criteria from `SPECIFICATIONS.md`, and selected tests
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

Use one consistent project convention. This standard uses numbered, uppercase,
hyphen-separated names:

```text
docs/dev/ADR/001-USE-SQLITE.md
```

An ADR records the decision, context, alternatives, rationale, consequences,
and status. Do not create ADRs for trivial fixes or private refactors.

### `CHANGELOG.md`

Create this at the first release tag, in the project root unless the
ecosystem requires another location. Group user-meaningful changes by the
released version and release tag. Do not use it as a commit-by-commit diary.

## Temporary files

### `docs/dev/TASK.md`

Create this only when work spans multiple steps, changes, sessions, or agents.
It should state the objective, requirements, affected files, verification, and
remaining work. Delete it after the work is implemented, verified, and
reconciled.

### `docs/dev/HANDOFF.md`

Create this only when the user specifically requests a handoff for incomplete
work to be continued by another agent.
Record completed work, discoveries, remaining work, tests, and the next action.
The receiving agent must validate it against current project documentation.
After the handoff is consumed and its durable information is reconciled,
delete it.

Temporary files may be committed while work is active, but must never become
a second source of truth or a permanent status history. Before creating a
release tag, confirm that no temporary files are included.

To reconcile documentation means moving durable information into the permanent
documents and confirming that no permanent document contradicts the
implementation.

## Source of truth

Use this order when resolving project conflicts:

1. Explicit user instruction.
2. `CONSTRAINTS.md` as a hard veto.
3. `PLAN.md` for project intent.
4. `SPECIFICATIONS.md` for required behavior.
5. Accepted ADRs for recorded decisions.
6. `ARCHITECTURE.md` for system structure.
7. Existing implementation as evidence of current behavior.

Do not silently choose between conflicting documents. Identify the conflict,
resolve it deliberately, and update the affected source of truth.

If a user instruction changes a hard constraint, surface the conflict and
update `CONSTRAINTS.md` in the same change rather than silently weakening it.

`USER.md` and `TEST.md` describe behavior defined elsewhere. If they conflict
with `SPECIFICATIONS.md`, correct them to match `SPECIFICATIONS.md`.

After code changes, use the implementation as the current-state reference
while reconciling `PLAN.md` and `ARCHITECTURE.md`. Update those documents when
project intent or system structure changed so the code and permanent
documentation describe the same system.

## Change workflow

### Trivial changes

For typos, renames, and private refactors, make the change and run the
smallest relevant checks. Update documentation only when its meaning changes.

### Standard changes

For behavior or user-facing changes:

1. Read the relevant project documentation.
2. Define or update requirements in `SPECIFICATIONS.md`.
3. Check `CONSTRAINTS.md` and `ARCHITECTURE.md`.
4. Create or update `TASK.md` when the work spans multiple steps, changes,
   sessions, or agents.
5. Implement the change.
6. Run relevant tests and checks.
7. Reconcile `PLAN.md` and `ARCHITECTURE.md` with the implementation when the
   codebase changed.
8. Update `USER.md` when user behavior changes.
9. Reconcile documentation and remove `TASK.md`.

### Significant changes

For changes to project scope, architecture, security, dependencies, data
models, or public interfaces, also create an ADR and update the affected
permanent documentation before considering the work complete.

For urgent fixes, restore the required behavior first, verify it, and perform
the documentation reconciliation in the same change whenever possible.

## Completion

Before finishing:

- Verify the implementation against `SPECIFICATIONS.md`.
- Verify no `CONSTRAINTS.md` rule was violated.
- Update `PLAN.md` if project intent changed.
- Update `ARCHITECTURE.md` if structure changed.
- Update `USER.md` if user operation changed.
- Update or create `TEST.md` when verification guidance is needed.
- Create an ADR for significant technical decisions.
- Remove completed `TASK.md` and consumed `HANDOFF.md`.
- State what was verified, which commands were run, and any remaining
  assumptions or open questions.
- Before a release tag, confirm that temporary files are not included.

The project is complete only when its code and permanent documentation
describe the same intended system.
