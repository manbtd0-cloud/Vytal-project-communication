# TASK-001 Manager Assignment

**Task:** TASK-001 — Import Sanitized Baseline Prototype
**Assigned to:** `MGR-MA`
**Human:** Muhammad Ahmad
**Role for this task:** Manager-side Scanner / Frontend execution
**Product branch:** `rebuild/TASK-001-sanitized-baseline-prototype`
**Status:** ASSIGNED

## Rationale

TASK-001 is the baseline/frontend bootstrap dependency for the rest of the reconstruction. `AAS-CLINICAL` is onboarded but its clinical work depends on later signal/clinical interfaces, while `LAIBA-BE` is not yet onboarded. MGR-MA therefore executes TASK-001 directly so the dependency graph can advance without violating worker ownership boundaries.

## Governing Inputs

- `MASTER_RECONSTRUCTION_SPEC.md`
- `tasks/TASK-001-sanitized-baseline-prototype.md`
- source commit `35b3297c9ce5f4f0ac8cfac2d16861a460c421b8` from `Ahmad-Ali-Shah/Vital`

## Rules

- No landing-page work.
- No hardcoded browser AI/provider/payment/database secrets.
- No production PHI authority in localStorage/IndexedDB.
- Historical code is reference material; superseded/unsafe behavior is excluded.
- Work happens on the named rebuild branch, not product `main`.
- MGR-MA will review verification evidence before accepting/merging.
