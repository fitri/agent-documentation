# Project Development and Documentation Standard

## Purpose

This file is a reusable bootstrap standard for AI-assisted development.
It applies to projects such as CLI tools, APIs, plugins, automation, and
configuration projects.

An agent given this file must use it to initialize and maintain a small,
consistent project documentation structure. The structure is shared memory
between agents and developers; it is not a replacement for source code,
tests, CLI help, or generated API documentation.

Keep this standard simple. Create the documented files as project knowledge
develops; they may begin empty or contain rough notes.

## Standard source

- Repository: <https://github.com/fitri/agent-documentation>
- Standard file: `DEVELOPMENT-STANDARD.md`

Use a tagged release when updating this standard in another project. Do not
automatically pull an unspecified or moving `latest` version.

Keep the local copy under `docs/dev/` by default. It may be removed only when
`AGENTS.md` records a fetchable, pinned source URL and version/tag for the
authoritative copy. If no pinned source is available, keep the local copy.

## Bootstrap

When initializing a project:

1. Read this file completely.
2. Inspect the repository and existing documentation before editing.
3. Ensure `docs/dev/` exists. If it does not, create it.
4. Place this file at `docs/dev/DEVELOPMENT-STANDARD.md`. If a copy already
   exists in the project root, move it into `docs/dev/`.
5. Create the project-level `AGENTS.md`.
6. Create the remaining required files under `docs/dev/`.
7. Populate `AGENTS.md` and the specific documentation files with the context
   currently known. Rough ideas, research, resources, and unanswered questions
   are valid early content; do not present guesses as settled facts.
8. Tell the user which assumptions or unanswered questions remain.

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
├── AGENTS.md                    (required)
├── README.md                    (optional companion; not part of workflow)
├── CHANGELOG.md                 (conditional; when the ecosystem expects it)
└── docs/
    └── dev/
        ├── DEVELOPMENT-STANDARD.md (required during initialization)
        ├── PLAN.md                  (required)
        ├── ARCHITECTURE.md           (required)
        ├── SPECIFICATIONS.md         (required)
        ├── CONSTRAINTS.md            (required)
        ├── USER.md                   (required)
        ├── TEST.md                  (conditional)
        ├── ADR/                     (conditional)
        ├── TASK.md                  (temporary)
        └── HANDOFF.md               (temporary)
```

The project-level `AGENTS.md` is the agent entry point. The files in
`docs/dev/` contain project-specific knowledge.

## File inventory

| Filename                  | Lifecycle   | Path            | Purpose                            |
|---------------------------|-------------|-----------------|------------------------------------|
| `DEVELOPMENT-STANDARD.md` | Required*   | `docs/dev/`     | Defines this workflow              |
| `AGENTS.md`               | Required    | Project root    | Directs agents through the project |
| `PLAN.md`                 | Required    | `docs/dev/`     | Defines project intent and goals   |
| `ARCHITECTURE.md`         | Required    | `docs/dev/`     | Describes system structure        |
| `SPECIFICATIONS.md`       | Required    | `docs/dev/`     | Defines required behavior         |
| `CONSTRAINTS.md`          | Required    | `docs/dev/`     | Defines non-negotiable boundaries |
| `USER.md`                 | Required    | `docs/dev/`     | Provides a short user guide       |
| `README.md`               | Exception   | Project root    | Presents the project to humans    |
| `CHANGELOG.md`            | Conditional | Project root    | Records changes by release        |
| `TEST.md`                 | Conditional | `docs/dev/`     | Maps behavior to verification     |
| `ADR/*.md`                | Conditional | `docs/dev/ADR/` | Records significant decisions     |
| `TASK.md`                 | Temporary   | `docs/dev/`     | Tracks active implementation work |
| `HANDOFF.md`              | Temporary   | `docs/dev/`     | Transfers incomplete work         |

`*` The standard is required during initialization. A project may keep its
versioned copy for future reference. Removal is allowed only under the
conditions stated in Standard source.

## File responsibilities

### `AGENTS.md`

Explains how an agent should work in this repository. It must include:

- A brief project overview.
- The location and version/tag of this standard.
- The location and purpose of `docs/dev/`.
- The project documentation to consult and a link to this standard's
  precedence rules.
- Baseline verification commands, or a pointer to `TEST.md`.
- Testing and completion expectations.
- Any project-specific agent restrictions.

It should route an agent to project knowledge, not duplicate project
requirements or redefine the standard's precedence. Record only
project-specific deviations from this standard.

### `docs/dev/PLAN.md`

Stores the starting point for the project: why it exists, rough ideas,
goals, scope, priorities, assumptions, research, resources, and the
definition of success. It can begin as a simple overview and become more
precise as the project is understood.

### `docs/dev/ARCHITECTURE.md`

Describes the actual system structure: major components, boundaries, data
flow, integrations, storage, interfaces, and important dependencies. Keep it
aligned with the current implementation.

### `docs/dev/SPECIFICATIONS.md`

Defines the project's actual required, observable behavior. Requirements
should be specific and testable.
Give important requirements stable identifiers, such as `AUTH-001`, so tasks
and tests can refer to them without copying their text.

### `docs/dev/CONSTRAINTS.md`

Defines boundaries that implementation must not violate, including security,
compatibility, technology, performance, resource, and regulatory constraints.

Constraints are hard boundaries. An agent may propose a change, but must not
silently weaken or remove a constraint.

### `docs/dev/USER.md`

Provides the canonical short, example-led guide for practical human usage:
what the project can do, how to install or start it, and common workflows.
Keep explanations short; prefer small practical examples over a complete
manual. Detailed reference belongs in CLI help, API documentation, or other
generated tooling.

## Companion file: `README.md`

`README.md` is bundled with the standard as an optional human-facing project
entry point. It is not part of the development workflow or its source-of-truth
hierarchy. Keep the flow simple and familiar:

1. Project overview.
2. Installation.
3. One small quickstart example.
4. Links to `USER.md` and other useful information.
5. License and standard project metadata.

Do not duplicate the full development documentation or the practical usage
guide in `README.md`.

## Documentation boundaries

Keep each document in its own lane. Documents may link to one another, but
must not become duplicate sources of truth.

- `AGENTS.md` gives agent instructions and routes to project knowledge; it
  does not contain the full project specification or redefine precedence.
- `PLAN.md` explains intent and scope; it does not define implementation
  details.
- `ARCHITECTURE.md` explains structure and boundaries; it does not prescribe
  every required behavior.
- `SPECIFICATIONS.md` defines observable behavior; it does not describe internal
  implementation choices.
- `CONSTRAINTS.md` defines hard limits; it does not become a general task list.
- `USER.md` explains user operation; it does not replace tests, API reference,
  or internal documentation.
- `README.md` presents the project to humans; it does not duplicate the full
  development standard or project knowledge.
- `TEST.md` maps requirements and user workflows to verification; it does not
  replace executable tests.
- `CHANGELOG.md` records user-meaningful changes by release; it does not
  become a commit-by-commit history.
- `ADR/*.md` records significant decisions; it does not document every change
  or rewrite previous decisions.
- `TASK.md` tracks current work; it does not become permanent project history.
- `HANDOFF.md` transfers incomplete work; it does not become a second task
  tracker or source of truth.

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

Create this directory when the project makes its first significant decision
involving project scope, architecture, dependencies, security, data, public
interfaces, or long-term maintenance.

Use one consistent project convention. This standard uses numbered, uppercase,
hyphen-separated names:

```text
docs/dev/ADR/001-USE-SQLITE.md
```

An ADR records the decision, context, alternatives, rationale, and
consequences. Do not require status tags. When a decision changes, add a new
ADR that identifies the previous decision, explains the change, and becomes
the applicable decision. Do not delete or rewrite the historical record. Do
not create ADRs for trivial fixes or private refactors.

### `CHANGELOG.md`

Create this at the first release tag, in the project root unless the
ecosystem requires another location. Group user-meaningful changes by release
version and release tag. Each version records the changes since the previous
version; for example, `1.0.0.0` records the first release and `1.0.0.1`
records changes since `1.0.0.0`. Do not use it as a commit-by-commit diary.

## Temporary files

To reconcile documentation means moving durable information into the permanent
documents and confirming that no permanent document contradicts the
implementation.

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
release tag, confirm that neither `TASK.md` nor `HANDOFF.md` remains.

## Source of truth

Use this order when resolving project conflicts:

1. `CONSTRAINTS.md` as the project's hard boundary.
2. Explicit user instruction that does not conflict with a constraint.
3. `PLAN.md` for project scope, intent, and overview.
4. `SPECIFICATIONS.md` for required, observable behavior within that scope.
5. ADRs for recorded decisions; a newer ADR that explicitly replaces an older
   one takes precedence.
6. `ARCHITECTURE.md` for actual system structure.
7. Existing implementation as evidence of current behavior.

`PLAN.md` controls project direction and intent; it does not override
behavior defined in `SPECIFICATIONS.md`. This ordering resolves intended
behavior. By default, the Markdown documentation is the source of truth for
what the project is intended to be. When determining what currently exists,
inspect the implementation directly. If the implementation and documentation
differ, a human must decide whether to update the implementation to match the
documentation or update the affected documentation to match an intentional
implementation change.

Do not silently choose between conflicting documents. Identify the conflict,
resolve it deliberately, and update the affected source of truth.

When documentation appears stale or conflicts with current decisions, surface
the issue and ask the user whether it should be updated, retained as linked
historical context, or removed. Do not delete or archive documentation solely
because an agent considers it unnecessary.

When a user request or decision is vague enough to affect scope, behavior,
architecture, or constraints, ask focused clarification questions before
implementing. Do not turn an unclear answer into an invented requirement.

If a user instruction changes a hard constraint, surface the conflict and
update `CONSTRAINTS.md` in the same change rather than silently bypassing it.

`USER.md` and `TEST.md` describe behavior defined elsewhere. If they conflict
with `SPECIFICATIONS.md`, correct them to match `SPECIFICATIONS.md`.

`README.md` should remain a concise human-facing entry point and link to
deeper material.

After code changes, use the implementation as the current-state reference
while comparing it with `SPECIFICATIONS.md`, `PLAN.md`, and
`ARCHITECTURE.md`. If they differ, present the difference for human
resolution, then update the chosen side so the implementation and Markdown
agree. The workflow is not required to proceed in a fixed order; a task or
implementation may come first, followed by reconciliation.

## Change workflow

The following is a suggested flow, not a rigid sequence. Start where the
change requires, then reconcile every affected source of truth before
finishing.

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
7. Reconcile `SPECIFICATIONS.md`, `PLAN.md`, and `ARCHITECTURE.md` with the
   implementation when the codebase changed.
8. Update `USER.md` or `README.md` when user-facing operation or the project
   introduction changed.
9. Reconcile documentation and remove `TASK.md`.

### Significant changes

For changes involving project scope, architecture, dependencies, security,
data, public interfaces, or long-term maintenance, also create an ADR and
update the affected permanent documentation before considering the work
complete. These are the same triggers described in the ADR section.

For urgent fixes, restore the required behavior first, verify it, and perform
the documentation reconciliation in the same change whenever possible.

## Completion

Before finishing:

- Verify the implementation against `SPECIFICATIONS.md`.
- Verify no `CONSTRAINTS.md` rule was violated.
- Update `PLAN.md` if project intent changed.
- Update `ARCHITECTURE.md` if structure changed.
- Update `USER.md` if user operation changed.
- Update `README.md` if the project introduction or installation changed.
- Update or create `TEST.md` when verification guidance is needed.
- Create an ADR for significant technical decisions.
- Update `CHANGELOG.md` when it exists and the change is user-meaningful.
- Remove completed `TASK.md` and consumed `HANDOFF.md`.
- State what was verified, which commands were run, and any remaining
  assumptions or open questions.
- Before a release tag, confirm that neither `TASK.md` nor `HANDOFF.md`
  remains.

A change is complete when its implementation and affected permanent
documentation describe the same intended system, with any remaining
assumptions or unresolved decisions identified.
