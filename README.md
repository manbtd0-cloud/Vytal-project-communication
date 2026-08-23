# Vytal Project Communication

This repository is the coordination and execution control plane for the Vytal product reconstruction/migration.

## Purpose

- Keep manager decisions, source mapping, task assignments, worker handoffs, reviews, and QA evidence in one place.
- Coordinate three AI-assisted workstreams: scanner/frontend, clinical algorithms, and backend/security.
- Preserve explicit traceability from historical Vytal source commits to the migration tasks that port or supersede them.
- Keep landing-page work out of scope.

## Repositories

- Historical source/evidence: `Ahmad-Ali-Shah/Vital`
- Product repository: `Ahmad-Ali-Shah/Project-Vytal-`
- Coordination repository: `manbtd0-cloud/Vytal-project-communication`

## Source of truth

Start with `MASTER_RECONSTRUCTION_SPEC.md`. Workers must execute only tasks marked `READY` or `ASSIGNED` in `TASKBOARD.md` and must submit the required handoff record before review.

## Operating rule

Historical commits are source material, not an instruction to restore obsolete, unsafe, fabricated, or superseded behavior. Current baby-boss clinical/security boundaries override older implementations where they conflict.
