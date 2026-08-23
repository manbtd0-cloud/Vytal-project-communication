# Vytal Reconstruction Master Specification

## Goal

Reconstruct/migrate the Vytal product into `Ahmad-Ali-Shah/Project-Vytal-` as a clean, reviewable, multi-agent sequence derived from historical Git evidence in `Ahmad-Ali-Shah/Vital`.

The communication repository is the control plane. Historical source commits are explicitly recorded here. The product repository receives only the actual product implementation and normal product documentation.

## Scope

Included:

- Vytal application shell and scanner
- camera/WebRTC/MediaPipe capture
- rPPG and contact PPG
- uncertainty and quality handling
- SpO2 screening proxy
- irregular-rhythm screening proxy
- anemia screening proxy
- jaundice screening proxy
- BMI/malnutrition proxy
- single-site BP crest-time trend
- Auth, patients, consent, Supabase, RLS
- transactional screening/observation/referral persistence
- server-side AI explanation
- billing/donations through the secure supported boundary
- dashboard/reporting
- security, QA, performance, observability

Excluded:

- landing-page work
- landing-page assets/routes/design plans
- archive-only commits
- CI/deploy-only noise
- obsolete persistence paths
- hardcoded provider/payment/database secrets
- fabricated clinical measurements
- unsupported payment-provider claims

## Governing principle

Historical Git chronology is evidence, not an instruction to restore every historical mistake.

Every source commit receives one of these dispositions:

- `KEEP`: port the valid change substantially as-is, adapted to the current architecture.
- `PARTIAL`: port only the valid portion of a mixed or superseded commit.
- `COMBINE`: fold tightly coupled historical commits into one meaningful migration task.
- `SKIP`: documentation/deploy/archive/noise that is not worth a product task.
- `SUPERSEDED/EXCLUDE`: unsafe, fabricated, misleading, or replaced behavior that must not return.
- `REFERENCE`: a target/checkpoint used for comparison rather than directly imported as one giant change.

## Source-of-truth priority

When sources disagree, use this order:

1. Current baby-boss product status and limitations.
2. Baby-boss merge design and its secure-vs-clinical ownership rules.
3. Current reconciled runtime behavior.
4. Secure backend/security/performance/architecture documentation.
5. Algorithm research registry, especially `[VERIFY]` and `[SCOPE]` items.
6. Historical clinical commits.
7. Older roadmap/research/swarm claims.
8. Landing-page material: always excluded.

## Non-negotiable product boundaries

- Vytal is screening/triage decision support, not diagnosis.
- Camera-derived values are research screening proxies unless backed by approved hardware.
- Low-confidence/invalid visual captures return retry/unknown behavior and do not become valid abnormal readings.
- Production PHI must not persist in `localStorage` or IndexedDB.
- BP calibration must not persist in browser storage; production calibration is owner-scoped server data.
- Provider, payment, service-role, webhook, and AI secrets never enter browser bundles.
- Supabase Auth/PostgreSQL/RLS/database functions are production persistence authority.
- Alibaba `cloudSync` must not become a second clinical persistence authority.
- AI explains deterministic results; AI does not own clinical tier/referral authority.
- Population anomaly logic must not be presented as real regional surveillance over owner-scoped browser data.
- Wearable/BLE/thermal integrations stay capability-gated experiments unless actual devices are connected and verified.
- JazzCash/EasyPaisa/Web3 must not be represented as active payment providers without real verified server integrations.
- Stripe-hosted Checkout remains the supported secure payment boundary from the secure architecture.
- No worker may restore historical hardcoded keys.
- No worker may restore fabricated 215 ms PTT, fixed fake BMI inputs, or similar fake measurements.
- `npm run verify` is the application release gate.
- `supabase test db` is the DB/RLS gate when local Supabase/Docker is available.

## Historical development lines

### Line A: original prototype / signal processing

Root: `35b3297c...`

The root already contains a runnable prototype: camera scan, AI triage, multilingual behavior, offline/demo queue, dashboard, and report. Later commits add shell fixes, POS/CHROM, uncertainty, signal accuracy, hardware-aware capture, and fingertip PPG.

### Line B: clinical expansion

Branch: `vytal-final-version`

Adds the clinical screening family and later audit-driven corrections. Its landing-page tail is excluded.

### Line C: secure backend

Branch/PR head: `agent/secure-database-billing` at `6bae2e3d...`

Adds the Apple Health-inspired product redesign, Supabase/Auth/RLS, patient/consent/referrals, billing, performance, permissions, and observability.

### Line D: baby-boss / pop-pop

Boundary: `e67a1bf7...` — `Add baby-boss reconciled Vytal snapshot`.

This is treated as an integration reference target, not as a one-commit dump. Post-boundary scanner/auth/security/clinical corrections are evaluated individually.

## Core source ledger

### Base lineage

| SHA | Disposition | Reconstruction use |
|---|---|---|
| `35b3297c` | PARTIAL | Sanitized runnable baseline. No browser secrets; no production PHI authority in browser storage. |
| `5b01ab33` | COMBINE | Early scanner/UI stabilization. |
| `73874939` | COMBINE | Splash/intro stability. |
| `2fb62e7a` | COMBINE | Responsive product navigation. |
| `8561b7e9` | EXCLUDE | Historical frontend production Groq key must never return. |
| `dc2e25ea` | KEEP | POS/CHROM hybrid rPPG. |
| `4bdb1927` | PARTIAL | Compatible signal/viewfinder/readout polish. |
| `0e04a28d` | PARTIAL | Defensible signal/stress refinements only. |
| `50b8a412` | KEEP | Pulse variability, SNR selection, timing refinement. |
| `457457ee` | KEEP | Signal stabilization, camera quality, uncertainty. |
| `3c7d6911` | KEEP | rPPG accuracy/harmonic/SNR improvements. |
| `9536dcbb` | KEEP | Hardware-aware camera assessment. |
| `9caa8073` | KEEP | Fingertip contact PPG. |
| README/CI/redeploy cleanup commits | SKIP | No independent product task. |

### Clinical lineage

| SHA | Disposition | Reconstruction use |
|---|---|---|
| `f6c6d09f` | PARTIAL | Split broad clinical expansion into independent modules. |
| `d6b66958` | PARTIAL | BP/BMI/BLE/thermal/anomaly additions; experimental features remain gated. |
| `3bb38ead`, `56a9e4f2`, `5ad41424`, `e71d49ff` | COMBINE | Restore valid scan UX/rPPG behavior as one integration unit. |
| `f1c87aaa` | EXCLUDE | Alibaba FC/Tablestore sync cannot compete with Supabase production persistence. |
| `dd400304` | KEEP/PARTIAL | Beat timestamps, secret removal, sync correctness, dynamic eye ROI, fake PTT removal. |
| `b5978fcd` | KEEP | Capture reliability, tracked eye guide, anemia confidence gate, voice guidance. |
| `1fdfbd81` | KEEP/PARTIAL | BLE SFLOAT, multi-signal rhythm evidence, ITA uncertainty, scoped EWMA. |
| `8cccd8dc` | KEEP | Red/green SpO2 proxy and single-site crest-time BP semantics. |
| `67edbf65` | KEEP | Erythema anemia and gray-world jaundice. |
| `26bff9b9` | KEEP | Remove fake BMI constants; adaptive IBI rejection. |
| `4bfd4e7d` | EXCLUDE | Landing-page plan. |

### Secure backend lineage

| SHA | Disposition | Reconstruction use |
|---|---|---|
| `7b7077a7` | COMBINE | Product motion redesign. |
| `7f473dd4` | COMBINE | Clinical interface redesign. |
| `8fd0b391` | COMBINE | Apple Health-inspired visual base. |
| `d0871568` | KEEP | Secure database/auth/billing foundation. |
| `9b3e6195` | KEEP | Consent-first patient/referral workflow. |
| `2932bfca` | KEEP | Secure billing/donation hardening. |
| `74a6871c` | KEEP | Backend/application performance. |
| `868ad1a5` | PARTIAL | Useful architecture/refactors/tests without academic overengineering. |
| `9709e102` | KEEP | Service-role billing permission correction. |
| `6bae2e3d` | KEEP | Observability/load testing. |

### Post-baby-boss lineage

| SHA | Disposition | Reconstruction use |
|---|---|---|
| `e67a1bf7` | REFERENCE | Reconciliation target, not giant import. |
| `b1a24df2` | KEEP | Mobile/desktop camera access and fallback fixes. |
| `689a1dc1` | KEEP | Landmark-driven anemia/jaundice/BMI overlays. |
| `6f23a82b`, `11f13e49`, `472ccadd` | COMBINE | Database verification cleanup. |
| `d52c5e6c` | PARTIAL | Keep visual scan fixes; exclude guest billing. |
| `d93673c6` | PARTIAL/SUPERSEDED | Keep environment configuration concept only; no hardcoded credentials. |
| `a9a8483b` | KEEP | Remove hardcoded API keys/security regression. |
| `2014ca9b` | EXCLUDE | Default credentials/guest billing conflict with secure contract. |
| `e4bfaabc` | KEEP | Security-check tooling fix. |
| `1532eb54` | EXCLUDE | Unsupported EasyPaisa/JazzCash/Web3 gateway claims. |
| `b0cfb353` | KEEP | Spoken scan positioning. |
| `62a6cc96` | KEEP | Alignment-gated countdown. |
| `75181930` | KEEP | Mobile alignment/contrast fixes. |
| `f4393a15` | KEEP | Auth email redirect correction. |
| `91992fcc` | PARTIAL | Keep BMI/CSS correction; skip content archives. |
| `1885f38a` | EXCLUDE | Local BP calibration fallback is superseded by owner-scoped backend calibration. |
| archive/content ZIP commits | SKIP | No product task. |

## Worker model

### Manager

The manager owns:

- dependency graph;
- task assignment;
- source disposition decisions;
- cross-agent ownership boundaries;
- handoff acceptance/rejection;
- integration review;
- prevention of superseded behavior returning.

Only the manager changes task order or assigns overlapping work.

### Agent A — Scanner / Frontend

Owns primarily:

- app shell and navigation;
- `ScanPage` and camera lifecycle;
- viewfinder and MediaPipe landmarks;
- spoken positioning;
- alignment state/countdown;
- mobile scanner UX;
- dashboard/report presentation;
- product visual redesign and scanner CSS.

Agent A does not redefine clinical thresholds, RLS, referral authority, or payment security.

### Agent B — Clinical Algorithms

Owns primarily:

- `rppg`;
- uncertainty;
- SpO2 proxy;
- irregular-rhythm proxy;
- alert scale;
- anemia;
- jaundice;
- BMI/malnutrition;
- BP trend;
- normalized clinical observations;
- clinical risk policy and unit/regression tests.

Agent B does not redefine Auth/RLS/payment/persistence ownership.

### Agent C — Backend / Security

Owns primarily:

- Supabase client/config boundary;
- Auth;
- patients/consent;
- screening/observation/referral persistence;
- RLS/RPCs/migrations;
- server-side AI explanation;
- Stripe billing/donations;
- server-only secrets;
- pgTAP/query-plan tests;
- performance/observability/security tooling.

Agent C does not redefine clinical thresholds or scanner algorithms without handoff.

## Task state machine

`PLANNED -> READY -> ASSIGNED -> IN_PROGRESS -> HANDOFF -> REVIEW -> ACCEPTED -> MERGED`

Review may send a task to `CHANGES_REQUESTED`, which returns it to `IN_PROGRESS`.

A worker does not self-mark a task `MERGED`.

## Branch convention

Product branch:

`rebuild/TASK-###-short-slug`

Commit examples:

- `feat(TASK-003): add POS CHROM rPPG extraction`
- `fix(TASK-024): enforce consent-gated screening writes`
- `test(TASK-027): cover referral transaction concurrency`

Avoid history-only/no-op commits.

## Handoff contract

Every task handoff must contain:

```markdown
# TASK-### Handoff

Agent:
Branch:
Commit:
Source SHAs:

## Implemented
- exact behavior

## Explicitly Not Implemented
- excluded/superseded historical behavior

## Files Changed
- path — purpose

## Verification
- command
- result

## Clinical/Security Notes
- limits and data-handling implications

## Open Issues
- concrete unresolved issues only

## Ready for Review
YES / NO
```

No verification output means not review-ready.

## Reconstruction task graph

1. TASK-001 — Sanitized baseline prototype
2. TASK-002 — App shell and early scanner stabilization
3. TASK-003 — POS/CHROM hybrid rPPG
4. TASK-004 — Pulse variability, SNR selection, timing refinement
5. TASK-005 — Reading uncertainty and camera quality
6. TASK-006 — rPPG accuracy upgrade
7. TASK-007 — Hardware-aware camera assessment
8. TASK-008 — Fingertip contact PPG
9. TASK-009 — Shared clinical module interfaces/observation contract
10. TASK-010 — Context-aware alert scale
11. TASK-011 — SpO2 screening proxy
12. TASK-012 — Irregular-rhythm screening proxy
13. TASK-013 — Anemia screening proxy
14. TASK-014 — Jaundice screening proxy
15. TASK-015 — BMI/malnutrition anthropometric proxy
16. TASK-016 — Single-site BP crest-time trend
17. TASK-017 — Capability-gated device helpers
18. TASK-018 — Clinical integrity correction pass
19. TASK-019 — Capture reliability and specialized guides
20. TASK-020 — Algorithm refinement pass
21. TASK-021 — Apple Health-inspired product redesign
22. TASK-022 — Supabase/Auth foundation
23. TASK-023 — Patients, consent, ownership, RLS
24. TASK-024 — Transactional screenings, observations, referrals, audit
25. TASK-025 — Server-side AI explanation boundary
26. TASK-026 — Stripe billing and donations
27. TASK-027 — Backend performance, architecture, observability, DB verification
28. TASK-028 — Baby-boss reconciliation
29. TASK-029 — Post-integration camera compatibility/specialized capture
30. TASK-030 — Final scanner/auth/clinical/security corrections
31. TASK-031 — Final documentation and release gate

## Dependency structure

Foundation:

`001 -> 002 -> 003 -> 004 -> 005 -> 006 -> 007 -> 008 -> 009`

Clinical fan-out after TASK-009:

`010, 011, 012, 013, 014, 015, 016, 017` may proceed independently where file ownership permits.

Then:

`010..017 -> 018 -> 019 -> 020`

Frontend redesign may begin after TASK-002:

`002 -> 021`

Backend may begin after TASK-001:

`001 -> 022 -> 023 -> 024`

`022 -> 025`

`023 -> 026`

`024 + 025 + 026 -> 027`

Integration:

`020 + 021 + 027 -> 028 -> 029 -> 030 -> 031`

## Baby-boss reconciliation authority

At TASK-028:

Secure line wins for:

- Auth;
- consent;
- patient identity;
- production persistence;
- RLS;
- transactional screening/referral writes;
- billing/donations;
- server/provider secret handling;
- request security;
- memory-only preview persistence.

Clinical line wins for:

- rPPG;
- uncertainty;
- anemia;
- jaundice;
- SpO2 proxy;
- rhythm proxy;
- alert scale;
- BMI/malnutrition proxy;
- single-site BP trend;
- voice guidance;
- scientific limitations.

Secure Apple Health-inspired UI remains the product visual base.

## Prohibited regression checklist

Reject any task that introduces:

- landing-page routes/assets/design work;
- hardcoded Groq/DashScope/provider keys;
- Supabase service-role key in browser code;
- payment/webhook secrets in browser code;
- persistent browser PHI;
- persistent browser BP calibration;
- Alibaba cloudSync as production authority;
- marking failed sync as successful;
- fabricated 215 ms PTT;
- claims of true PTT from one sequential camera;
- fixed fake BMI input;
- invalid anemia capture becoming severe anemia;
- invalid jaundice capture becoming positive jaundice;
- unknown/low-confidence visual result automatically creating referral;
- AI overriding deterministic clinical policy;
- simulated wearable displayed as a real connection;
- regional-surveillance claims from owner-scoped client data;
- default/guest billing from superseded history;
- unsupported EasyPaisa/JazzCash/Web3 payment claims;
- statements that camera outputs are certified medical-device readings.

## Verification gates

Per task:

1. focused test/reproducible verification;
2. no prohibited regression;
3. complete handoff;
4. source SHA traceability;
5. reviewable branch/commit.

Per wave:

- build remains green;
- previously green focused tests remain green;
- manager reviews ownership drift;
- taskboard is updated.

Integration gate:

- clinical modules have deterministic tests;
- RLS/transaction tests pass when infrastructure is available;
- memory-only preview still works;
- production writes require auth + patient + consent;
- no provider/payment secret reaches browser code.

Final gate:

```bash
npm run verify
```

and when Supabase/Docker is available:

```bash
supabase test db
```

Also verify:

- no landing work;
- no hardcoded secrets;
- no persistent browser PHI/calibration;
- no cloudSync production authority;
- no unsupported payment-provider claims;
- no fabricated PTT/BMI inputs;
- unknown visual scans do not refer;
- AI does not own clinical policy.

## Completion definition

The reconstruction is complete when all approved historical product behavior has been migrated through reviewable tasks, excluded/superseded behavior remains absent, baby-boss security/clinical boundaries are preserved, post-integration corrections are applied, verification is green or unavailable external infrastructure is explicitly recorded, and the communication repository contains the source/task/handoff/review trail.
