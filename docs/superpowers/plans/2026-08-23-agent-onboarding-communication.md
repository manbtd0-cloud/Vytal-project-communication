# Vytal Agent Onboarding and Communication Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add persistent cold-start onboarding, role hierarchy, readiness acknowledgments, and a shared communication protocol for all Vytal team AIs.

**Architecture:** The communication repository remains the control plane. Shared rules live in `START_HERE.md` and `COMMUNICATION_PROTOCOL.md`; each AI has a role/readiness file; global readiness lives in `agents/READINESS_REGISTRY.md`; operational messages are appended to `COMMUNICATION_LOG.md`.

**Tech Stack:** Markdown + Git/GitHub coordination repository.

**Spec:** `docs/superpowers/specs/2026-08-23-agent-onboarding-communication-design.md`

## Global Constraints

- `MGR-MA` is the Central Manager / Orchestrator.
- `AAS-CLINICAL` is Clinical Algorithms + QA.
- `LAIBA-BE` is Backend + Security.
- Workers read all role files before readiness.
- Workers do not self-assign tasks.
- Private chats do not count as shared persistent communication.
- Worker readiness requires role-block update, registry update and common-log ACK.
- Direct human instructions override AI-level orchestration.

---

### Task 1: Add cold-start and communication infrastructure

**Files:**
- Create: `START_HERE.md`
- Create: `COMMUNICATION_PROTOCOL.md`
- Create: `COMMUNICATION_LOG.md`
- Create: `agents/MANAGER_MUHAMMAD_AHMAD.md`
- Create: `agents/AHMAD_ALI_SHAH.md`
- Create: `agents/LAIBA.md`
- Create: `agents/READINESS_REGISTRY.md`
- Create: `BOOTSTRAP_PROMPTS.md`
- Modify: `README.md`

**Interfaces:**
- Consumes: existing `MASTER_RECONSTRUCTION_SPEC.md` and `TASKBOARD.md`.
- Produces: one mandatory reading order, three role identities, a readiness transaction, and one common communication protocol.

- [x] Create `START_HERE.md` with exact cold-start order and readiness rules.
- [x] Create `COMMUNICATION_PROTOCOL.md` with authority, message types, format, blockers, handoffs, reviews and corrections.
- [x] Create three role files with cross-role recognition.
- [x] Initialize manager as READY and workers as NOT_READY.
- [x] Create readiness registry matching those states.
- [x] Create shared log with the manager infrastructure decision.
- [x] Create two teammate bootstrap prompts that stop after onboarding.
- [x] Update README so new AIs begin at `START_HERE.md`.
- [x] Verify all cross-references and readiness states.
- [x] Commit as one coherent documentation/infrastructure change.
