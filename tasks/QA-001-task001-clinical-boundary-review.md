# QA-001 — TASK-001 Clinical Boundary Review

**Status:** ASSIGNED

**Assigned to:** `AAS-CLINICAL` — Ahmad Ali Shah's Clinical Algorithms + QA AI

**Review target repository:** `Ahmad-Ali-Shah/Project-Vytal-`

**Review target branch:** `rebuild/TASK-001-sanitized-baseline-prototype`

**Review target commit:** `63367a010aa7afdb2f4d0acd610034f112eb6d16`

**Historical reference:** `Ahmad-Ali-Shah/Vital@35b3297c9ce5f4f0ac8cfac2d16861a460c421b8`

## Purpose

Perform a read-only Clinical + QA review of the sanitized baseline while MGR-MA finishes implementation verification. This is an auxiliary review, not a reconstruction dependency and not permission to implement future clinical tasks early.

## Required Reading

Before reviewing:

1. Pull/read latest communication-repo state.
2. Confirm `AAS-CLINICAL` remains `READY`.
3. Read `MASTER_RECONSTRUCTION_SPEC.md` clinical/security boundaries.
4. Read `tasks/TASK-001-sanitized-baseline-prototype.md`.
5. Read recent `COMMUNICATION_LOG.md` entries.
6. Inspect product commit `63367a010aa7afdb2f4d0acd610034f112eb6d16` and its TASK-001 branch.
7. Compare relevant runtime behavior against historical source SHA `35b3297c...` only where needed to judge what was sanitized.

## Review Scope

Review only. Do not modify product code.

Check all of the following:

### Measurement integrity
- Missing breathing/stress values are not replaced with fabricated normal-looking numbers.
- TASK-001 does not claim diagnostic or certified-device equivalence.
- Camera/rPPG wording is clearly research screening/proxy wording where appropriate.
- Baseline heuristic flags are described as screening/follow-up rules, not diagnosis.

### Explanation integrity
- No browser provider credential is required.
- No direct Groq/DashScope/provider network call remains in the baseline explanation module.
- Offline/deterministic explanation cannot silently override the deterministic baseline flag.
- Wording does not falsely tell a patient they are medically healthy or diagnosed.

### Persistence/report integrity
- No production PHI authority is represented as browser-persistent storage.
- Session-memory behavior is stated honestly.
- No false backend/cloud synchronization success is displayed.
- Printable/QR report does not falsely imply durable record retrieval.

### Scope integrity
- No anemia, jaundice, BMI, BP, SpO2, rhythm, later signal upgrade, Supabase, billing, or Apple Health redesign has been pulled into TASK-001.
- No landing-page runtime work is present.

## Deliverable

Produce `reviews/QA-001-TASK-001-CLINICAL-BOUNDARY.md` using this structure:

```markdown
# QA-001 — TASK-001 Clinical Boundary Review

Reviewer: AAS-CLINICAL
Target commit: 63367a010aa7afdb2f4d0acd610034f112eb6d16
Outcome: PASS | PASS_WITH_NOTES | CHANGES_REQUIRED

## Findings

### Blocking
- None | <finding with exact file/line or code evidence>

### Non-blocking
- None | <finding>

## Checklist
- [PASS/FAIL] Missing-value integrity
- [PASS/FAIL] Screening-not-diagnosis wording
- [PASS/FAIL] No browser provider path
- [PASS/FAIL] Deterministic explanation boundary
- [PASS/FAIL] Session-memory honesty
- [PASS/FAIL] No false sync/cloud claim
- [PASS/FAIL] Report/QR durability honesty
- [PASS/FAIL] No later-wave clinical scope
- [PASS/FAIL] No landing runtime scope

## Evidence
- <exact paths, snippets, source SHA comparisons>

## Recommendation
ACCEPT_FOR_MANAGER_TECHNICAL_VERIFICATION | REQUEST_CHANGES
```

## Communication

Append an `ACK` for `QA-001` before review and a `REVIEW` message after completing it, following `COMMUNICATION_PROTOCOL.md`.

If repository write access is unavailable, return the exact review document and exact two log messages to Ahmad Ali Shah/Muhammad Ahmad for persistence.

## Stop Rule

After submitting the review, STOP. Do not self-assign TASK-003 or modify TASK-001 product code. MGR-MA owns the next decision.
