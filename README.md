# Vytal Project Communication

This repository is the persistent coordination and execution control plane for the Vytal product reconstruction/migration.

## New AI / New Session

**Start with `START_HERE.md`.**

No teammate AI is allowed to receive implementation work until it completes the repository cold-start procedure and is marked `READY` in `agents/READINESS_REGISTRY.md`.

## Purpose

- Keep manager decisions, source mapping, task assignments, worker handoffs, reviews, QA evidence and AI-to-AI communication in one place.
- Coordinate Muhammad Ahmad's Central Manager AI, Ahmad Ali Shah's Clinical/QA AI, and Laiba's Backend/Security AI.
- Preserve explicit traceability from historical Vytal source commits to reconstruction tasks that port, supersede or exclude them.
- Keep landing-page work out of scope.

## Repositories

- Historical source/evidence: `Ahmad-Ali-Shah/Vital`
- Product repository: `Ahmad-Ali-Shah/Project-Vytal-`
- Coordination repository: `manbtd0-cloud/Vytal-project-communication`

## Governing Documents

Read in this order for cold start:

1. `START_HERE.md`
2. `MASTER_RECONSTRUCTION_SPEC.md`
3. `COMMUNICATION_PROTOCOL.md`
4. `TASKBOARD.md`
5. all files under `agents/`
6. `COMMUNICATION_LOG.md`
7. assigned task, if one exists

## Operating Rule

Historical commits are source material, not an instruction to restore obsolete, unsafe, fabricated, or superseded behavior. Current baby-boss clinical/security boundaries override older implementations where they conflict.

Persistent repository state is shared team memory. Private AI chats are not a substitute for the communication protocol.
