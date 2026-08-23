# Vytal AI Readiness Registry

This is the canonical high-level onboarding state for project AIs.

An AI is operationally `READY` only when:

1. its role-file readiness block is complete;
2. its row below says `READY`;
3. its onboarding `ACK` exists in `COMMUNICATION_LOG.md`.

| Agent code | Human | Role | Infrastructure read | Other roles acknowledged | Manager authority acknowledged | Log ACK | Status |
|---|---|---|---|---|---|---|---|
| `MGR-MA` | Muhammad Ahmad | Central Manager / Orchestrator | YES | YES | YES | manager initialization decision | READY |
| `AAS-CLINICAL` | Ahmad Ali Shah | Clinical Algorithms + QA | NO | NO | NO | NO | NOT_READY |
| `LAIBA-BE` | Laiba | Backend + Security | NO | NO | NO | NO | NOT_READY |

## Worker Update Rule

A worker AI may edit **only its own row** after completing `START_HERE.md` onboarding.

Required final values:

```text
Infrastructure read: YES
Other roles acknowledged: YES
Manager authority acknowledged: YES
Log ACK: <MESSAGE_ID>
Status: READY
```

The worker must not change another agent's row.

The Central Manager may correct registry inconsistencies after reviewing the worker's role block and ACK.
