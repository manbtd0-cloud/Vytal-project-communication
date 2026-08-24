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
| TASK-001 Sanitized baseline prototype | Frontend | MGR-MA | — | IN_PROGRESS |
| TASK-002 App shell/scanner stabilization | Frontend | Agent A | 001 | PLANNED |
| TASK-003 POS/CHROM hybrid rPPG | Clinical | AAS-CLINICAL | 002 | PLANNED |
| TASK-004 Pulse variability/SNR/timing | Clinical | AAS-CLINICAL | 003 | PLANNED |
| TASK-005 Uncertainty/camera quality | Clinical | AAS-CLINICAL | 004 | PLANNED |
| TASK-006 rPPG accuracy upgrade | Clinical | AAS-CLINICAL | 005 | PLANNED |
| TASK-007 Hardware-aware camera assessment | Scanner/Clinical | MGR-MA + AAS-CLINICAL | 006 | PLANNED |
| TASK-008 Fingertip contact PPG | Scanner/Clinical | MGR-MA + AAS-CLINICAL | 007 | PLANNED |
| TASK-009 Clinical module interfaces | Clinical | AAS-CLINICAL | 008 | PLANNED |
| TASK-010 Context-aware alert scale | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-011 SpO2 screening proxy | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-012 Irregular-rhythm proxy | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-013 Anemia proxy | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-014 Jaundice proxy | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-015 BMI/malnutrition proxy | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-016 Single-site BP crest-time trend | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-017 Capability-gated device helpers | Clinical | AAS-CLINICAL | 009 | PLANNED |
| TASK-018 Clinical integrity correction | Clinical | AAS-CLINICAL | 010–017 | PLANNED |
| TASK-019 Capture reliability/specialized guides | Frontend | Agent A | 018 | PLANNED |
| TASK-020 Algorithm refinement pass | Clinical | AAS-CLINICAL | 019 | PLANNED |
| TASK-021 Apple Health product redesign | Frontend | Agent A | 002 | PLANNED |
| TASK-022 Supabase/Auth foundation | Backend | LAIBA-BE | 001 | PLANNED |
| TASK-023 Patients/consent/ownership/RLS | Backend | LAIBA-BE | 022 | PLANNED |
| TASK-024 Transactional screening/referral/audit | Backend | LAIBA-BE | 023 | PLANNED |
| TASK-025 Server-side AI explanation | Backend | LAIBA-BE | 022 | PLANNED |
| TASK-026 Stripe billing/donations | Backend | LAIBA-BE | 023 | PLANNED |
| TASK-027 Performance/observability/DB verification | Backend | LAIBA-BE | 024,025,026 | PLANNED |
| TASK-028 Baby-boss reconciliation | Integration | MGR-MA + AAS-CLINICAL + LAIBA-BE | 020,021,027 | PLANNED |
| TASK-029 Camera compatibility/specialized capture | Frontend | Agent A | 028 | PLANNED |
| TASK-030 Final scanner/auth/clinical/security corrections | Integration | MGR-MA + AAS-CLINICAL + LAIBA-BE | 029 | PLANNED |
| TASK-031 Final docs/release gate | Release | MGR-MA + AAS-CLINICAL + LAIBA-BE | 030 | PLANNED |

## Immediate queue

`TASK-001` is currently IN_PROGRESS under `MGR-MA` on product branch `rebuild/TASK-001-sanitized-baseline-prototype`.

`AAS-CLINICAL` is READY and waiting for the clinical dependency chain to unlock. `LAIBA-BE` remains unavailable until onboarding is complete.

Once TASK-001 is MERGED:
- TASK-002 becomes READY.
- TASK-022 becomes READY, but it may only be assigned when `LAIBA-BE` is operationally READY.

The manager is the only actor allowed to change dependency order or mark a task READY outside these rules.
