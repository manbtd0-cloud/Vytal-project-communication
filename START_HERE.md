# Vytal Multi-Agent Control Plane — Start Here

This repository is the persistent coordination layer for the Vytal reconstruction. Every AI agent must complete this document's cold-start procedure before receiving or executing project work.

## Repositories

- Historical source/evidence: `Ahmad-Ali-Shah/Vital`
- Product implementation: `Ahmad-Ali-Shah/Project-Vytal-`
- Coordination/control plane: `manbtd0-cloud/Vytal-project-communication`

## What We Are Doing

We are reconstructing the Vytal product into `Project-Vytal-` through explicit, reviewable tasks derived from historical Git evidence in `Vital`.

Historical commits are source material. They are not permission to restore obsolete, unsafe, fabricated, or superseded behavior. The current baby-boss security and clinical boundaries in `MASTER_RECONSTRUCTION_SPEC.md` override older implementations where they conflict.

Landing-page work is completely out of scope.

## AI Authority Model

### Central Manager / Orchestrator

**Human:** Muhammad Ahmad  
**AI role:** Central Manager / Orchestrator  
**Role file:** `agents/MANAGER_MUHAMMAD_AHMAD.md`

Muhammad Ahmad's AI has final orchestration authority for:

- task order and dependency unlocking;
- task assignment and ownership;
- interpretation of historical source SHAs;
- `KEEP / PARTIAL / COMBINE / SKIP / SUPERSEDED / EXCLUDE` decisions;
- cross-agent scope conflicts;
- acceptance/rejection of handoffs;
- integration and merge readiness;
- corrections and rework;
- changes to the shared orchestration protocol.

This is organizational authority, not a claim that one model is inherently more capable than another. Worker AIs may challenge an instruction with evidence, but they must not silently override a manager decision that affects shared scope or architecture.

### Ahmad Ali Shah's AI

**Human:** Ahmad Ali Shah  
**AI role:** Clinical Algorithms + QA specialist  
**Role file:** `agents/AHMAD_ALI_SHAH.md`

Primary domain: rPPG, uncertainty, SpO2 proxy, rhythm screening, anemia, jaundice, BMI/malnutrition, BP trend, clinical policy, clinical tests and verification.

### Laiba's AI

**Human:** Laiba  
**AI role:** Backend + Security specialist  
**Role file:** `agents/LAIBA.md`

Primary domain: Supabase/Auth, patients, consent, RLS, persistence, referrals, Edge Functions, billing, security, observability, database verification.

### Muhammad Ahmad's execution domain

The Central Manager may directly execute or delegate Muhammad Ahmad-owned scanner/frontend work, including camera lifecycle, MediaPipe/viewfinder UX, spoken guidance, alignment behavior, mobile scanner UX, dashboard/report presentation, and product visual integration.

## Mandatory Cold-Start Reading Order

An AI is **NOT READY** until it reads all of the following in this exact order:

1. `START_HERE.md`
2. `MASTER_RECONSTRUCTION_SPEC.md`
3. `COMMUNICATION_PROTOCOL.md`
4. `TASKBOARD.md`
5. `agents/MANAGER_MUHAMMAD_AHMAD.md`
6. `agents/AHMAD_ALI_SHAH.md`
7. `agents/LAIBA.md`
8. its own role file a second time
9. `COMMUNICATION_LOG.md`
10. its assigned task file, only if the manager has already assigned one

Reading only the agent's own role file is insufficient. Every AI must understand the manager, both worker roles, the communication protocol, and the reconstruction boundaries.

## Mandatory Readiness Handshake

After completing the reading order, a teammate AI must:

1. Edit **only its own readiness block** in its role file.
2. Change every required `NO` field to `YES`.
3. Set `STATUS: READY`.
4. Add a concise acknowledgment of:
   - its own role;
   - the other worker's role;
   - the Central Manager's orchestration authority;
   - the rule that it cannot self-assign tasks or alter shared architecture silently.
5. Update only its row in `agents/READINESS_REGISTRY.md`.
6. Append one `ACK` entry to `COMMUNICATION_LOG.md` using the format in `COMMUNICATION_PROTOCOL.md`.
7. Commit those communication-repo changes.
8. Stop. Do **not** begin coding unless a task is explicitly `ASSIGNED` to that AI.

If the AI cannot write to this repository, it must return the exact proposed readiness block and ACK entry to its human teammate for commit. It is not considered operationally READY until the repository reflects the acknowledgment.

## Normal Work Loop

```text
Manager marks task READY
        ↓
Manager assigns task
        ↓
Worker rereads task + recent communication
        ↓
Worker ACKs assignment
        ↓
Worker executes in product repo branch
        ↓
Worker verifies
        ↓
Worker writes handoff
        ↓
Manager reviews actual diff + evidence
        ↓
Rejected → correction / rework
Accepted → merge
        ↓
Manager updates taskboard and unlocks dependencies
```

## Non-Negotiable Rules

- Never self-assign a task.
- Never start a `PLANNED` task.
- Never silently alter task scope.
- Never restore excluded or superseded historical behavior.
- Never put provider/payment/service-role secrets in browser code.
- Never represent screening proxies as diagnosis or certified device readings.
- Never use landing-page work in the product reconstruction.
- Never claim a handoff is complete without verification evidence.
- Never treat private-chat context as shared team memory; persistent coordination belongs in this repository.
- When repository state and private-chat memory conflict, current repository documents control unless a human explicitly overrides them.

## Readiness Test

Before saying "ready", an AI must be able to answer all of these from the repository:

1. What are the three repositories and what is each for?
2. Who is the Central Manager?
3. What is Ahmad Ali Shah's AI responsible for?
4. What is Laiba's AI responsible for?
5. What work may Muhammad Ahmad's side execute directly?
6. What task states may a worker execute?
7. Where are blockers/questions communicated?
8. What is required in a handoff?
9. Which historical behaviors are prohibited from returning?
10. Who decides whether a task is accepted and what unlocks next?

If any answer is uncertain, reread the relevant document before acknowledging readiness.
