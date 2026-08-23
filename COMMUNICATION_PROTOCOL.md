# Vytal AI Communication Protocol

This protocol defines the persistent AI-to-AI communication system for the Vytal reconstruction.

## 1. Principle

Private chats are local working context. They are **not** shared team memory.

Any information that another AI needs in order to act correctly must be persisted in this coordination repository through:

- `COMMUNICATION_LOG.md` for shared operational messages;
- `TASKBOARD.md` for task state;
- `tasks/` for exact task instructions;
- `handoffs/` for completed-work evidence;
- `reviews/` for manager acceptance/rejection;
- `agents/` for role/readiness state;
- `MASTER_RECONSTRUCTION_SPEC.md` for governing architecture and source disposition.

## 2. Authority

The Central Manager / Orchestrator is Muhammad Ahmad's AI (`MGR-MA`).

The manager controls task creation, assignment, ownership, dependency order, source-SHA interpretation, scope changes, integration decisions, handoff acceptance/rejection, merge readiness, and protocol changes.

Workers may identify a problem, propose an alternative, or challenge a manager instruction with technical evidence. When the issue affects shared scope, architecture, clinical policy, security boundaries, ownership or dependencies, the worker must raise a `QUESTION` or `BLOCKER` and await a manager `DECISION` before deviating.

A direct human instruction overrides AI-level orchestration. If two human instructions conflict, do not guess; record the conflict and ask the affected humans to resolve it.

## 3. Roles and Agent Codes

| Code | Human | AI role |
|---|---|---|
| `MGR-MA` | Muhammad Ahmad | Central Manager / Orchestrator + Muhammad Ahmad-side execution |
| `AAS-CLINICAL` | Ahmad Ali Shah | Clinical Algorithms + QA |
| `LAIBA-BE` | Laiba | Backend + Security |

## 4. Shared Message Log

The common communication document is `COMMUNICATION_LOG.md`.

It is append-only except for correcting obvious formatting corruption. Never delete or rewrite historical messages to make the record look cleaner.

### Message ID

Use:

```text
<AGENT-CODE>-<UTC-YYYYMMDDTHHMMSSZ>-<TYPE>
```

Examples:

```text
AAS-CLINICAL-20260823T120501Z-ACK
LAIBA-BE-20260823T121211Z-BLOCKER
MGR-MA-20260823T122002Z-DECISION
```

If two messages occur in the same second, append `-2`, `-3`, etc.

### Allowed Types

- `ACK` — confirms onboarding or assignment receipt.
- `ASSIGNMENT` — manager assigns a task.
- `PROGRESS` — material progress that affects coordination.
- `QUESTION` — non-blocking request for a manager/peer answer.
- `BLOCKER` — work cannot safely continue.
- `HANDOFF` — points to a completed handoff file.
- `REVIEW` — points to a manager review.
- `DECISION` — authoritative manager ruling.
- `CORRECTION` — changes an earlier instruction or message without deleting history.
- `UNBLOCK` — manager confirms blocker is resolved.

## 5. Message Format

Append messages exactly in this structure:

```markdown
---

## <MESSAGE_ID>

**FROM:** <AGENT_CODE>  
**TO:** <MGR-MA | AAS-CLINICAL | LAIBA-BE | ALL>  
**TYPE:** <TYPE>  
**TASK:** <TASK-### | NONE>  
**STATUS:** <OPEN | CLOSED | INFORMATIONAL>  
**UTC:** <YYYY-MM-DDTHH:MM:SSZ>

### Summary
<Short factual summary.>

### Evidence
- <source SHA, file path, test output, task section, or `None`>

### Requested Action
<Specific action, or `None` if informational.>

### References
- <task/handoff/review/doc path>
```

Do not use vague requests such as "please check". State what decision/action is required.

## 6. Before Starting Any Assigned Task

The worker must:

1. Pull/read the latest coordination repository state.
2. Confirm its own readiness state is `READY`.
3. Confirm the task is `ASSIGNED` to its agent code.
4. Read the entire task file.
5. Read the task's listed source SHAs/files.
6. Read new `COMMUNICATION_LOG.md` messages since its last acknowledgment.
7. Check dependencies in `TASKBOARD.md`.
8. Append an `ACK` message for the assignment.
9. Only then create/use the product branch named by task convention.

If any condition fails, do not start implementation.

## 7. Progress Messages

Use `PROGRESS` only when another agent/manager benefits from knowing it, for example:

- an interface has stabilized and another task can safely consume it;
- a source commit contains mixed valid/invalid behavior not captured by the task;
- a verification constraint changes;
- an expected file/interface does not exist.

Do not spam the common log with routine "still working" messages.

## 8. Blockers and Questions

A worker must stop the affected work and log a `BLOCKER` when:

- task instructions conflict with governing docs;
- old source behavior conflicts with current baby-boss limits;
- a security/clinical ambiguity could materially alter correctness;
- another task has changed an interface the worker depends on;
- required permissions/source data are unavailable;
- verification repeatedly fails for reasons outside the task's clear scope.

A blocker/question should cite concrete evidence such as historical SHA, current file/path, relevant spec section, test output, or exact conflicting behavior.

## 9. Handoff Protocol

When implementation is complete:

1. Run the verification required by the task.
2. Create `handoffs/TASK-###-HANDOFF.md` from `handoffs/HANDOFF_TEMPLATE.md`.
3. Include exact product branch and commit SHA.
4. Include source SHAs.
5. State what was intentionally not ported.
6. Include commands and results.
7. Append a `HANDOFF` message to `COMMUNICATION_LOG.md`.
8. Stop and wait for manager review.

A worker does not mark its task `MERGED`.

## 10. Review Protocol

The Central Manager reads the task and handoff, inspects the actual product diff/commit, checks source disposition and prohibited regressions, reviews verification evidence, writes `reviews/TASK-###-REVIEW.md`, and appends a `REVIEW` message.

Possible outcomes:

- `ACCEPTED`
- `CHANGES_REQUESTED`
- `REJECTED`

Only an accepted task may advance toward merge/unlocking.

## 11. Corrections

Never erase an old message merely because it became wrong.

Use a `CORRECTION` message containing `CORRECTS: <OLD_MESSAGE_ID>` and state the new instruction. The latest valid manager `DECISION`/`CORRECTION` controls.

## 12. Conflict Rules

When two workers touch the same conceptual boundary:

1. stop before making conflicting architecture changes;
2. log a `BLOCKER` or `QUESTION`;
3. state both intended interfaces;
4. manager chooses the authoritative interface;
5. manager logs a `DECISION`;
6. affected tasks update implementation/handoffs accordingly.

No "last commit wins" architecture.

## 13. Communication Priority

When information conflicts, use:

1. direct current human instruction;
2. latest manager `DECISION`/`CORRECTION`;
3. `MASTER_RECONSTRUCTION_SPEC.md`;
4. exact assigned task file;
5. `TASKBOARD.md`;
6. accepted handoffs/reviews from dependencies;
7. older communication-log entries;
8. private-chat recollection.

A worker must surface contradictions rather than silently choosing a lower-priority source.

## 14. Repository Write Discipline

- Pull/read latest state before writing shared files.
- Modify only your own readiness block unless acting as manager.
- Append to `COMMUNICATION_LOG.md`; do not rewrite others' messages.
- Do not edit another agent's role/readiness section.
- The manager owns canonical taskboard transitions.
- If the shared log changed remotely, reconcile and append without deleting either message.

## 15. Onboarding ACK Requirement

A cold-start AI is not operationally ready until:

- its role-file readiness block says `STATUS: READY`;
- its registry row says `READY`;
- `COMMUNICATION_LOG.md` contains its onboarding `ACK`;
- the ACK explicitly recognizes Central Manager authority, its own role, the other worker's role, and the no-self-assignment/no-silent-architecture-override rule.

Completing those three repository updates is the onboarding transaction.
