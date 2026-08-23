# Vytal Multi-Agent Onboarding and Communication Design

## Goal

Give any teammate AI enough persistent context to enter the Vytal reconstruction cold, identify its role and authority boundaries, acknowledge all other AI roles, communicate through a shared protocol, and prove readiness before receiving implementation work.

## Architecture

The coordination repository is the persistent control plane. Onboarding is layered:

1. `START_HERE.md` defines cold-start context and reading order.
2. `MASTER_RECONSTRUCTION_SPEC.md` defines product/reconstruction truth.
3. `COMMUNICATION_PROTOCOL.md` defines how AIs communicate and resolve conflicts.
4. `agents/*.md` defines role-specific ownership and readiness blocks.
5. `agents/READINESS_REGISTRY.md` is the global readiness index.
6. `COMMUNICATION_LOG.md` is the append-only shared operational log.
7. `TASKBOARD.md`, `tasks/`, `handoffs/`, and `reviews/` drive execution.

## Authority

Muhammad Ahmad's AI (`MGR-MA`) is the Central Manager / Orchestrator with final AI-level authority over task order, assignment, scope, integration, review, acceptance and cross-agent conflict resolution.

Ahmad Ali Shah's AI (`AAS-CLINICAL`) is Clinical Algorithms + QA.

Laiba's AI (`LAIBA-BE`) is Backend + Security.

The authority model is organizational, not a claim of intrinsic model superiority. Direct human instructions supersede AI-level orchestration.

## Readiness Transaction

A worker is not READY merely because it says so in chat.

It must:

1. complete the mandatory repository reading order;
2. edit only its own role-file readiness block;
3. update only its readiness-registry row;
4. append an onboarding ACK to the common log;
5. persist those changes in Git.

The manager does not assign implementation tasks to a worker lacking this state.

## Communication

Private chats are local context only. Shared operational state belongs in repository files.

Messages are appended to `COMMUNICATION_LOG.md` using agent-coded timestamp IDs and fixed message types. Architecture/scope conflicts require evidence-backed `QUESTION` or `BLOCKER` messages and manager `DECISION` responses.

## Safety Against Coordination Drift

- Workers cannot self-assign.
- Workers cannot silently change another domain's architecture.
- Workers read all roles, not only their own.
- Manager decisions are persistent.
- Corrections append new messages rather than rewriting history.
- Task completion requires a handoff and manager review.
- Repository state outranks private-chat recollection when they conflict.

## Verification

The infrastructure is valid when:

- all files referenced by `START_HERE.md` exist;
- all three role files cross-reference the other two roles;
- both worker readiness blocks begin `NOT_READY`;
- manager readiness begins `READY`;
- registry states match role-file states;
- protocol defines ACK, assignment, blocker, handoff, review and decision flows;
- bootstrap prompts explicitly stop after onboarding;
- README directs new AIs to `START_HERE.md`.
