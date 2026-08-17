Development Markdown Files
Fitri Rahim

​
Abdul Rahim, Muhammad Fitri​
AI Development Documentation Protocol

1. Purpose

This document defines the documentation protocol used by AI coding agents working on this repository.

The purpose is to provide a consistent, model-independent structure for:

Understanding project intent
Understanding system architecture
Defining required behavior
Defining constraints
Breaking requirements into executable tasks
Implementing changes
Verifying functionality
Recording significant technical decisions
Passing work between agents
Allowing agents to understand the system from both developer and user perspectives
This protocol is intentionally lightweight.

The goal is not to create documentation for the sake of documentation.

The goal is to create a reliable external memory and control structure that allows different AI agents and human developers to work on the same project without losing context.



2. Core Principles

2.1 Intent before implementation

Agents must understand why the project exists and what it is intended to achieve before modifying implementation.

The project intent is defined primarily by:

PLAN.md

Agents should not begin significant implementation work without understanding the relevant project plan.



2.2 Separate concerns

Each documentation file has a specific responsibility.

Do not duplicate information unnecessarily between documents.

The intended separation is:



Document

Primary question

AGENTS.md

How should an AI agent work on this repository?

PLAN.md

What are we trying to achieve, and why?

ARCHITECTURE.md

How is the system structured?

SPEC.md

What exact behavior is required?

CONSTRAINTS.md

What must not happen?

DESIGN.md

What should the user interface/experience/design look like?

TASK.md

What concrete work needs to be done now?

TEST.md

How do we prove the required behavior works?

USER.md

How does a user operate the finished system?

ADR/*.md

Why were important technical decisions made?

HANDOFF.md

What does the next agent need to know to continue?



2.3 Documentation has different lifetimes

Not every document should be treated the same way.

Permanent documents

These describe durable project knowledge:

AGENTS.md

PLAN.md

ARCHITECTURE.md

SPEC.md

CONSTRAINTS.md

DESIGN.md

TEST.md

USER.md

ADR/*

Temporary working documents

These represent current execution state:

TASK.md

HANDOFF.md

TASK.md should not become a permanent historical backlog unless the project explicitly chooses to use it that way.

When there is no pending implementation task, TASK.md should be removed.

HANDOFF.md should be removed once the handoff has been successfully completed and its information has been incorporated into the appropriate permanent documentation.



3. Documentation Hierarchy

The conceptual dependency is:

                         AGENTS.md

                       Agent protocol

                             │

                             ↓

                          PLAN.md

                     Project intent

                     WHY + WHAT

                             │

            ┌────────────────┼────────────────┐

            ↓                ↓                ↓

     ARCHITECTURE.md      SPEC.md       CONSTRAINTS.md

          HOW            MUST DO          MUST NOT

            │                │                │

            └────────────────┼────────────────┘

                             ↓

                        DESIGN.md

                    when applicable

                             │

                             ↓

                         TASK.md

                    actionable work

                             │

                             ↓

                     IMPLEMENTATION

                             │

                             ↓

                          TEST.md

                      verification

                             │

                             ↓

                         ADR/*

                    decision history

USER.md exists as a separate perspective:

USER.md

   │

   └── How a human uses the resulting system

HANDOFF.md exists as temporary cross-agent state:

Agent A

   │

   ↓

HANDOFF.md

   │

   ↓

Agent B

   │

   ↓

HANDOFF.md removed



4. AGENTS.md

Purpose

AGENTS.md is the operating manual for AI coding agents.

It must explain how agents are expected to work within the repository.

It should contain:

Documentation structure
Purpose of each documentation file
Agent workflow
Rules for modifying documentation
Testing expectations
Decision-making process
Rules for handling uncertainty
Rules for task completion
Rules for handoffs
It should not become a duplicate of:

PLAN.md
ARCHITECTURE.md
SPEC.md
CONSTRAINTS.md
It should describe the protocol, not the project implementation.

Important distinction

AGENTS.md answers:

“How should I work?”

It does not answer:

“How is this application implemented?”



5. PLAN.md

Purpose

PLAN.md is the highest-level project planning document.

It defines:

Project purpose
Problem being solved
Desired outcome
Major objectives
Project scope
Major milestones
High-level priorities
Important assumptions
Major strategic direction
It should provide an agent with an overview of the entire project.

An agent reading only PLAN.md should be able to understand:

What are we building, why are we building it, and what does success look like?



PLAN.md is not an implementation document

Do not fill PLAN.md with:

Individual code changes
Detailed function implementations
Temporary debugging information
Every completed task
Low-level implementation details
Those belong elsewhere.



When PLAN.md must be updated

Changes must flow back to PLAN.md when implementation reveals a change to:

Project scope
Project goals
Major requirements
Major architectural direction
Major user experience direction
Fundamental assumptions
Definition of success
Not every code change requires a plan update.

For example:

Changing a variable name

does not require updating PLAN.md.

But:

Replacing a local database with a distributed database

may require a plan update if it changes the project’s strategic direction.



6. ARCHITECTURE.md

Purpose

ARCHITECTURE.md describes the overall technical structure of the project.

It should explain:

Major components
Component responsibilities
Data flow
Control flow
System boundaries
External integrations
Storage
APIs
Communication mechanisms
Important dependencies
Major architectural patterns
It answers:

“How is this system organized?”

It should remain understandable at the system level.

Detailed implementation belongs in source code and appropriate design documentation.



7. SPEC.md

Purpose

SPEC.md defines what the system must do.

Specifications should describe observable or enforceable behavior.

Examples:

A user can create an account.



An authenticated user can create a project.



The API must return HTTP 401 for unauthenticated requests.



A failed payment must not create an active subscription.

Specifications should avoid unnecessarily prescribing implementation.

Prefer:

The system must retain user preferences.

over:

Create a PostgreSQL table called user_preferences.

The latter is an architectural/implementation concern.



8. CONSTRAINTS.md

Purpose

CONSTRAINTS.md defines boundaries that implementation must respect.

Examples:

Technology restrictions
Security requirements
Performance requirements
Compatibility requirements
Regulatory requirements
Resource limits
API compatibility
Backward compatibility
Explicitly forbidden approaches
Examples:

Do not expose internal database IDs through public APIs.



Do not introduce a new runtime dependency without justification.



The system must remain compatible with Python 3.12.



User data must not be stored in client-side local storage.

Constraints are especially important for AI agents because agents may otherwise optimize toward a locally attractive solution that violates a project-level requirement.



9. DESIGN.md

Purpose

DESIGN.md describes design specifications that are not purely architectural or functional.

Examples include:

UI/UX
User flows
Navigation
Interaction behavior
Visual hierarchy
Layout requirements
Accessibility requirements
Responsive behavior
Design-system requirements
This file is optional.

It should exist when the project has meaningful design requirements.



10. TASK.md

Purpose

TASK.md converts project requirements and architecture into concrete executable work.

It is the bridge between:

What we want

and:

What the agent should implement now

A task should normally be:

Concrete
Testable
Scoped
Implementable
Traceable back to the relevant specification or architecture
Example:

## Task



Implement user session creation.



### Requirements



- Accept valid credentials.

- Reject invalid credentials.

- Return a session token.

- Persist the session.

- Add automated tests.



### Related documentation



- SPEC.md: Authentication

- ARCHITECTURE.md: Authentication Service

- CONSTRAINTS.md: Security



TASK.md lifecycle

TASK.md represents pending work.

When all pending work has been completed and verified:

TASK.md

should be deleted.

Do not leave:

TASK.md



Status: COMPLETE

as permanent documentation unless there is an explicit reason to preserve it.

Historical information belongs in:

ADR/

CHANGELOG.md

or other appropriate permanent documentation.



11. TEST.md

Purpose

TEST.md defines how the system’s required behavior is verified.

It should describe:

Functional verification
Acceptance criteria
Important edge cases
Integration requirements
Regression requirements
Performance requirements where relevant
Security verification where relevant
TEST.md describes what must be proven.

Actual automated tests should normally live in the project’s test infrastructure:

tests/

The relationship is:

SPEC.md

    ↓

TEST.md

    ↓

tests/

A specification without a meaningful verification strategy should be treated as incomplete when practical.



12. USER.md

Purpose

USER.md describes the project from the perspective of someone who uses the finished system.

It is intentionally different from technical documentation.

It should explain:

What the system does for the user
How to start using it
Common workflows
User-facing commands
User-facing configuration
Expected behavior
Common usage patterns
It should avoid explaining internal implementation unless that information is necessary for a user.

The distinction is:

AGENTS.md

How an AI developer works on it



USER.md

How a human user works with it



ARCHITECTURE.md

How the system is built



SPEC.md

What the system must do

This separation is intentional.



13. ADR Directory

Purpose

ADR/ contains Architecture Decision Records.

Each ADR records a significant technical decision and the reasoning behind it.

Example:

adr/

├── 001-use-postgresql.md

├── 002-use-redis.md

└── 003-event-driven-processing.md

A decision should generally become an ADR when it has meaningful consequences for:

Architecture
Technology selection
Data model
Security
Scalability
API compatibility
Major dependencies
Significant trade-offs
Long-term maintenance


ADRs are historical records

Once accepted, an ADR should normally remain immutable.

If a previous decision changes, create a new ADR.

Example:

001-use-redis.md

Later:

005-replace-redis-with-valkey.md

Do not rewrite ADR 001 merely to make historical decisions appear as though they never happened.

The ADR system should answer:

“Why is the system like this?”

and:

“What did we previously decide, and why?”



14. HANDOFF.md

Purpose

HANDOFF.md is temporary cross-agent communication.

It should be created when one agent cannot complete the work and another agent must continue.

It may contain:

Current state
What was completed
What remains
Important discoveries
Failed approaches
Relevant files
Tests already performed
Known problems
Recommended next action
Example:

## Completed



Implemented authentication endpoint.



## Remaining



Session expiration handling is incomplete.



## Important discovery



The existing middleware already validates JWT signatures.



Do not create a second authentication middleware.



## Tests



Authentication unit tests pass.



## Next action



Implement session expiration and add integration coverage.



HANDOFF.md lifecycle

After the next agent has successfully consumed the handoff:

Relevant information should be incorporated into permanent documentation if necessary.
TASK.md should reflect the remaining work.
HANDOFF.md should be deleted.
The repository should not accumulate stale handoff documents.



15. Decision-Making Process

This is the most important part of the protocol.

Agents should not treat all documentation as equal.

When deciding whether to make a change, use the following process.

Step 1 — Understand the project

Read:

AGENTS.md

PLAN.md

Understand the project objective before deciding how to implement something.



Step 2 — Determine whether the request changes project intent

Ask:

Does this change alter the project’s purpose, scope, major objective, or definition of success?

If yes:

Update PLAN.md

before proceeding.



Step 3 — Determine architectural impact

Ask:

Does this change alter system structure, components, data flow, interfaces, dependencies, or major technology choices?

If yes:

Review/update ARCHITECTURE.md



Step 4 — Determine behavioral requirements

Ask:

What exact behavior is required?

Update or derive the relevant requirements in:

SPEC.md



Step 5 — Determine boundaries

Ask:

What must not happen?

Document important boundaries in:

CONSTRAINTS.md



Step 6 — Determine design impact

Ask:

Does this change affect UI, UX, interaction, visual behavior, or user workflow?

If yes:

Review/update DESIGN.md



Step 7 — Break the work into tasks

Only after the intended behavior and architecture are understood should the work be converted into:

TASK.md

Tasks should be small enough to implement and verify.



Step 8 — Implement

The agent implements the task.

The implementation must conform to:

PLAN.md

ARCHITECTURE.md

SPEC.md

CONSTRAINTS.md

DESIGN.md

where applicable.



Step 9 — Verify

Run the relevant tests and verification procedures defined by:

TEST.md

Do not mark work complete merely because the code compiles or appears correct.



Step 10 — Determine whether a decision occurred

After implementation, ask:

Did we make a significant technical decision that future developers or agents need to understand?

If yes:

Create a new ADR.

Do not create ADRs for trivial implementation details.



Step 11 — Reconcile documentation

After implementation, compare the resulting system against the documentation.

Ask:

Does PLAN.md still describe the intended project?



Does ARCHITECTURE.md still describe the actual architecture?



Does SPEC.md still describe required behavior?



Does CONSTRAINTS.md still describe applicable restrictions?



Does DESIGN.md still describe the intended experience?



Does TEST.md still describe how correctness is verified?

Update documentation where reality has changed.



Step 12 — Close the task

When all work is implemented and verified:

Remove TASK.md

unless additional pending work remains.



16. Decision Flow

The complete decision process can be summarized as:

                    New requirement/change

                             │

                             ↓

                    Does intent change?

                       /            \

                     YES            NO

                      │              │

                      ↓              │

                 Update PLAN         │

                      │              │

                      └──────┬───────┘

                             ↓

                    Does architecture change?

                       /            \

                     YES            NO

                      │              │

                      ↓              │

              Update ARCHITECTURE    │

                      │              │

                      └──────┬───────┘

                             ↓

                    Define behavior

                             │

                             ↓

                         Update SPEC

                             │

                             ↓

                    Define boundaries

                             │

                             ↓

                    Update CONSTRAINTS

                             │

                             ↓

                     Design if needed

                             │

                             ↓

                       Create TASK

                             │

                             ↓

                       Implement

                             │

                             ↓

                          TEST

                             │

                             ↓

                  Significant decision?

                       /            \

                     YES            NO

                      │              │

                      ↓              │

                  Create ADR        │

                      │              │

                      └──────┬───────┘

                             ↓

                   Reconcile documentation

                             │

                             ↓

                     Complete TASK

                             │

                             ↓

                      Delete TASK.md



17. Source of Truth Rules

When documentation conflicts, use the following principle:

Project intent

PLAN.md

System structure

ARCHITECTURE.md

Required behavior

SPEC.md

Explicit boundaries

CONSTRAINTS.md

Design requirements

DESIGN.md

Current execution state

TASK.md

Verification requirements

TEST.md

Historical decisions

ADR/*

User operation

USER.md

Agent operating procedure

AGENTS.md

Temporary cross-agent state

HANDOFF.md

If two documents conflict, the agent must not silently choose one.

The conflict should be identified and resolved deliberately.



18. Handling Ambiguity

AI agents frequently encounter incomplete or conflicting requirements.

The agent should not immediately guess when the ambiguity could materially affect the project.

Use this priority:

Explicit user instruction
Current project intent in PLAN.md
Explicit requirements in SPEC.md
Explicit constraints in CONSTRAINTS.md
Current architecture in ARCHITECTURE.md
Existing implementation
Existing ADR decisions
Reasonable engineering judgment
If ambiguity remains significant, stop and ask for clarification.

Do not invent a major product or architectural decision merely to make progress.

For minor, reversible implementation details, reasonable engineering judgment may be used.



19. Existing Code vs Documentation

Existing code is evidence of the current implementation.

It is not automatically proof that the implementation represents the intended design.

When code conflicts with documentation:

Do not blindly rewrite the documentation to match the code.

Do not blindly rewrite the code to match the documentation.

Determine whether:

The code is wrong.
The documentation is outdated.
The project intentionally changed but documentation was not updated.
There is an unresolved design decision.
For significant conflicts, resolve the underlying decision first.



20. Preventing Documentation Drift

Documentation should be updated as part of implementation when the implementation changes documented behavior or structure.

Avoid the pattern:

Implement first

"Document later"

because “later” frequently never happens.

Instead:

Plan

→ Specify

→ Architect

→ Task

→ Implement

→ Test

→ Reconcile documentation

→ Record significant decisions

Documentation is part of the implementation lifecycle.



21. Minimal Repository Structure

A small project does not need every document.

The recommended starting point is:

AGENTS.md

PLAN.md

ARCHITECTURE.md

SPEC.md

CONSTRAINTS.md

TASK.md

TEST.md

Add only when needed:

DESIGN.md

USER.md

HANDOFF.md

and:

adr/

when meaningful architectural decisions begin accumulating.

Do not create empty documentation files merely because the protocol defines them.



22. Recommended Mature Repository Structure

A mature project may eventually contain:

.

├── AGENTS.md

├── PLAN.md

├── ARCHITECTURE.md

├── SPEC.md

├── CONSTRAINTS.md

├── DESIGN.md

├── TEST.md

├── USER.md

│

├── TASK.md

├── HANDOFF.md

│

├── adr/

│   ├── 001-*.md

│   ├── 002-*.md

│   └── 003-*.md

│

├── src/

├── tests/

└── ...

TASK.md and HANDOFF.md may legitimately be absent.

Their absence can itself mean:

No active task.

No pending handoff.



23. Important Anti-Patterns

23.1 Documentation duplication

Do not copy the same requirement into five documents.

Each piece of information should have a natural home.



23.2 Giant AGENTS.md

Do not turn AGENTS.md into a complete technical manual.

It should tell the agent where information lives and how to work, not contain the entire project knowledge base.



23.3 Permanent TASK.md

Do not allow TASK.md to become an undocumented changelog.

Completed work should disappear from the active task document.

Historical information belongs elsewhere.



23.4 Stale HANDOFF.md

Never leave a stale handoff that may cause a future agent to follow obsolete instructions.

Consume it, incorporate useful information, and delete it.



23.5 ADR for every change

Do not create an ADR for:

Rename variable

Fix typo

Add missing null check

Refactor private function

Create ADRs for decisions whose reasoning matters to future maintainers.



23.6 Implementation leaking into specifications

Avoid turning:

SPEC.md

into a description of the source code.

Specifications should primarily describe required behavior.



23.7 Architecture becoming implementation documentation

ARCHITECTURE.md should explain system structure, not document every function and class.



24. Multi-Agent Compatibility

This protocol is intentionally independent of any specific AI model.

An agent may be:

Codex
Claude Code
Gemini
GitHub Copilot
OpenCode
A custom MCP agent
A human developer
The repository itself provides the shared context.

The agents do not need to share the same model, memory system, or orchestration framework.

They only need to understand this protocol.

The repository therefore becomes a shared external memory layer.



25. Agent Session Protocol

At the beginning of a session, an agent should:

1. Read AGENTS.md.

2. Read PLAN.md.

3. Inspect relevant ARCHITECTURE.md sections.

4. Inspect relevant SPEC.md sections.

5. Inspect relevant CONSTRAINTS.md sections.

6. Check whether TASK.md exists.

7. Check whether HANDOFF.md exists.

8. Inspect relevant ADRs.

9. Inspect the actual implementation.

10. Determine the current state before making changes.

The agent should not assume that the previous agent’s implementation is correct.

It should verify the current state.



26. End-of-Session Protocol

Before ending work, an agent should:

1. Run relevant tests.

2. Verify implementation against SPEC.md.

3. Verify constraints were not violated.

4. Verify architecture documentation if architecture changed.

5. Update PLAN.md if project intent changed.

6. Create an ADR if a significant decision was made.

7. Update TASK.md if work remains.

8. Delete TASK.md if no pending work remains.

9. Create HANDOFF.md only if another agent must continue.

10. Remove stale HANDOFF.md information after successful handoff.



27. The Fundamental Model

The entire protocol can be remembered as:

PLAN

  ↓

Why are we doing this?

What are we trying to achieve?



ARCHITECTURE

  ↓

How is the system structured?



SPEC

  ↓

What must it do?



CONSTRAINTS

  ↓

What must it not do?



DESIGN

  ↓

How should it look and behave for users?



TASK

  ↓

What do we implement now?



IMPLEMENTATION

  ↓

Build it.



TEST

  ↓

How do we prove it works?



ADR

  ↓

Why did we make important technical decisions?



USER

  ↓

How does someone use the finished system?



HANDOFF

  ↓

What does the next agent need to continue?



28. Final Principle

The documentation system should behave like a living engineering model of the project.

It should not be treated as paperwork.

The desired lifecycle is:

Intent

  ↓

Plan

  ↓

Architecture + Specification + Constraints

  ↓

Design

  ↓

Tasks

  ↓

Implementation

  ↓

Verification

  ↓

Decision history

  ↓

Updated project knowledge

The most important rule is:

When implementation changes the understanding of the project, update the appropriate source of truth.

Do not allow the code and documentation to silently diverge.

The objective is that a completely new AI agent, with no conversational history, can enter the repository and reconstruct:

Why the project exists.
What the project is supposed to do.
How the project is structured.
What constraints apply.
What the current work is.
How correctness is verified.
Why important technical decisions were made.
How a user interacts with the system.
What another agent was doing if work was handed over.


29. Decision Record — Project Documentation Standard

Date: 2026-08-17

The protocol was refined into a single reusable bootstrap file named:

DEVELOPMENT-STANDARD.md

The standard is intended to be shared across multiple projects through a
versioned GitHub repository. Projects should use a released, pinned version
rather than automatically pulling the latest version.

The standard file may be copied into a project after an agent receives its
versioned GitHub URL. The agent then reads it, creates the project-level
AGENTS.md, and scaffolds the project development documentation.

The agreed project structure is:

project/
├── AGENTS.md
└── docs/
    └── dev/
        ├── PLAN.md
        ├── ARCHITECTURE.md
        ├── SPEC.md
        ├── CONSTRAINTS.md
        ├── USER.md
        ├── CHANGELOG.md   (created at the first release)
        ├── TASK.md        (temporary, only while work is active)
        ├── HANDOFF.md     (temporary, only during an incomplete handoff)
        ├── TEST.md        (conditional)
        └── ADR/           (conditional)

AGENTS.md belongs at the project root because agent tools commonly discover it
there. It provides the project overview, points to this standard, and directs
agents to docs/dev/.

The docs/dev/ files are the project-specific sources of truth. The standard
defines how those files are created and maintained; it must not be duplicated
inside each project document.

TASK.md and HANDOFF.md must be removed after their information has been
implemented, verified, and reconciled into the permanent documentation.

CHANGELOG.md is not an initial file. It is created at the first GitHub release
and records user-meaningful changes grouped by release tag and version.

TEST.md and ADR/ are created only when the project has meaningful verification
requirements or a significant technical decision, respectively.

The standard deliberately avoids mandatory runbooks, metadata systems,
validators, CI tooling, or additional documentation categories. The workflow
must reduce maintenance burden rather than become a second project to manage.
If these nine questions can be answered from the repository, the repository has sufficient external context to support reliable multi-agent development.