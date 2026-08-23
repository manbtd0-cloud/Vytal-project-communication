# Vytal Reconstruction Taskboard

Authoritative plan: `MASTER_RECONSTRUCTION_SPEC.md`

## Status legend

- `PLANNED` — defined but dependencies not satisfied
- `READY` — dependencies satisfied and may be assigned
- `ASSIGNED` — worker selected
- `IN_PROGRESS` — worker executing
- `HANDOFF` — worker submitted evidence
- `REVIEW` — manager reviewing
- `CHANGES_REQUESTED` — corrections required
- `ACCEPTED` — review passed
- `MERGED` — accepted product change merged

## Current board

| Task | Workstream | Owner | Depends on | Status |
|---|---|---|---|---|
| TASK-001 Sanitized baseline prototype | Frontend | Agent A | — | READY |
| TASK-002 App shell/scanner stabilization | Frontend | Agent A | 001 | PLANNED |
| TASK-003 POS/CHROM hybrid rPPG | Clinical | Agent B | 002 | PLANNED |
| TASK-004 Pulse variability/SNR/timing | Clinical | Agent B | 003 | PLANNED |
| TASK-005 Uncertainty/camera quality | Clinical | Agent B | 004 | PLANNED |
| TASK-006 rPPG accuracy upgrade | Clinical | Agent B | 005 | PLANNED |
| TASK-007 Hardware-aware camera assessment | Scanner/Clinical | A+B | 006 | PLANNED |
| TASK-008 Fingertip contact PPG | Scanner/Clinical | A+B | 007 | PLANNED |
| TASK-009 Clinical module interfaces | Clinical | Agent B | 008 | PLANNED |
| TASK-010 Context-aware alert scale | Clinical | Agent B | 009 | PLANNED |
| TASK-011 SpO2 screening proxy | Clinical | Agent B | 009 | PLANNED |
| TASK-012 Irregular-rhythm proxy | Clinical | Agent B | 009 | PLANNED |
| TASK-013 Anemia proxy | Clinical | Agent B | 009 | PLANNED |
| TASK-014 Jaundice proxy | Clinical | Agent B | 009 | PLANNED |
| TASK-015 BMI/malnutrition proxy | Clinical | Agent B | 009 | PLANNED |
| TASK-016 Single-site BP crest-time trend | Clinical | Agent B | 009 | PLANNED |
| TASK-017 Capability-gated device helpers | Clinical | Agent B | 009 | PLANNED |
| TASK-018 Clinical integrity correction | Clinical | Agent B | 010–017 | PLANNED |
| TASK-019 Capture reliability/specialized guides | Frontend | Agent A | 018 | PLANNED |
| TASK-020 Algorithm refinement pass | Clinical | Agent B | 019 | PLANNED |
| TASK-021 Apple Health product redesign | Frontend | Agent A | 002 | PLANNED |
| TASK-022 Supabase/Auth foundation | Backend | Agent C | 001 | PLANNED |
| TASK-023 Patients/consent/ownership/RLS | Backend | Agent C | 022 | PLANNED |
| TASK-024 Transactional screening/referral/audit | Backend | Agent C | 023 | PLANNED |
| TASK-025 Server-side AI explanation | Backend | Agent C | 022 | PLANNED |
| TASK-026 Stripe billing/donations | Backend | Agent C | 023 | PLANNED |
| TASK-027 Performance/observability/DB verification | Backend | Agent C | 024,025,026 | PLANNED |
| TASK-028 Baby-boss reconciliation | Integration | Manager + A/B/C | 020,021,027 | PLANNED |
| TASK-029 Camera compatibility/specialized capture | Frontend | Agent A | 028 | PLANNED |
| TASK-030 Final scanner/auth/clinical/security corrections | Integration | A/B/C | 029 | PLANNED |
| TASK-031 Final docs/release gate | Release | Manager + A/B/C | 030 | PLANNED |

## Immediate queue

Only `TASK-001` is currently READY.

Once TASK-001 is MERGED:
- TASK-002 becomes READY.
- TASK-022 becomes READY and may run in parallel with the frontend/clinical path.

The manager is the only actor allowed to change dependency order or mark a task READY outside these rules.
