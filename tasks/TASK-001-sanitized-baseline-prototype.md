# TASK-001 — Sanitized Baseline Prototype

**Status:** ASSIGNED

**Owner:** `MGR-MA` — Muhammad Ahmad's Central Manager / Orchestrator acting as Scanner / Frontend implementer for this task

**Product repository:** `Ahmad-Ali-Shah/Project-Vytal-`

**Product branch:** `rebuild/TASK-001-sanitized-baseline-prototype`

**Source repository:** `Ahmad-Ali-Shah/Vital`

**Primary source SHA:** `35b3297c9ce5f4f0ac8cfac2d16861a460c421b8`

**Historical source message:** `feat: complete Vytal rPPG camera scan, Qwen/Groq AI triage, multilingual support, offline IndexedDB queue, CHW dashboard, printable QR report, and hackathon documentation`

## Objective

Create the first runnable product baseline in `Project-Vytal-` by porting the useful product files from the historical root snapshot while sanitizing behavior that violates the current secure Vytal contract.

This is a migration task, not a redesign task. Do not improve later algorithms here. Later historical changes have dedicated tasks.

## Source boundary

The source root contains product files plus `.claude`, `idea`, README/documentation and other non-runtime material. The historical root also contains older persistence/provider behavior that is superseded later.

Port only the runnable product baseline needed for the first application milestone.

### Candidate root runtime files/directories

- `index.html`
- `package.json`
- `package-lock.json`
- `vite.config.js`
- `public/` product assets required by runtime
- `src/App.jsx`
- `src/main.jsx`
- `src/index.css`
- `src/components/`
- `src/pages/`
- `src/lib/` only to the extent required for this baseline to run

### Do not copy as part of TASK-001

- `.claude/`
- old agent/spec infrastructure
- `idea/` as implementation files
- landing-page material if encountered
- archive ZIPs
- old deployment-only artifacts not required to run the product

## Mandatory sanitization

While porting the baseline:

1. **No hardcoded AI/provider credentials.**
   - If the root source contains a Groq/Qwen/DashScope key or equivalent browser credential, remove it.
   - Do not invent a replacement key.
   - AI explanation may be disabled/unconfigured at this baseline.

2. **No production PHI authority in persistent browser storage.**
   - Historical IndexedDB/localStorage behavior may be retained only as an explicitly demo/preview-compatible temporary behavior if necessary to make the baseline usable.
   - Do not describe it as the final production storage architecture.
   - Prefer memory-only behavior when a small mechanical change is sufficient.

3. **Do not pull later features backward.**
   - Do not add Supabase/Auth/RLS yet; that starts in TASK-022.
   - Do not add later POS/CHROM improvements beyond what exists in the root; TASK-003 onward handles signal history.
   - Do not add anemia/jaundice/BMI/BP extensions yet.
   - Do not apply the Apple Health redesign yet.

4. **Do not touch landing-page code.**

## Required product state after this task

The product repository should contain a coherent baseline application capable of representing the original product concept:

- Vytal application shell boots;
- scanner route/page renders;
- baseline camera scan UI exists;
- dashboard exists;
- report/printable-result surface exists if present in the source baseline;
- multilingual/UI support present in the source baseline may be retained;
- build tooling is complete enough to install and run;
- no secret is embedded in browser source.

## Execution procedure

- [ ] Read `MASTER_RECONSTRUCTION_SPEC.md` in the communication repo before modifying the product repo.
- [ ] Inspect source commit `35b3297c9ce5f4f0ac8cfac2d16861a460c421b8` directly.
- [ ] Create product branch `rebuild/TASK-001-sanitized-baseline-prototype` from the current product base selected by the manager.
- [ ] Port the runtime root/build files required to boot the React/Vite application.
- [ ] Port `src/App.jsx`, `src/main.jsx`, `src/index.css`, required `src/components/`, `src/pages/`, and baseline `src/lib/` dependencies.
- [ ] Port only runtime-required `public/` assets.
- [ ] Remove/disable hardcoded provider credentials if encountered.
- [ ] Ensure the baseline does not claim old browser persistence is the final production clinical database.
- [ ] Do not copy `.claude/`, old orchestration material, landing work, or archive content.
- [ ] Install dependencies using the repository's package manager contract.
- [ ] Run the production build.
- [ ] Run any baseline tests that exist and are runnable.
- [ ] Manually confirm the application shell, scan page, dashboard, and report route/surface render.
- [ ] Inspect the final diff and remove accidental unrelated files.
- [ ] Commit as `feat(TASK-001): import sanitized Vytal baseline prototype`.
- [ ] Push the task branch.
- [ ] Create `handoffs/TASK-001-handoff.md` in the communication repo using the handoff contract.

## Verification evidence required in handoff

Record:

- exact product branch;
- exact product commit SHA;
- source SHA `35b3297c...`;
- dependency install command and result;
- build command and result;
- test command/result if tests exist;
- list of intentionally excluded root directories/files;
- confirmation that no provider secret was copied;
- confirmation that no landing-page material was copied;
- any baseline persistence limitation still present.

## Acceptance criteria

TASK-001 may be accepted only when:

- the product baseline boots/builds;
- the original product application surfaces are present enough for later tasks to build upon;
- no landing-page work is introduced;
- no hardcoded AI/payment/database-secret credential is introduced;
- no worker claims the historical baseline persistence is the final secure production architecture;
- the task contains no later-wave feature work;
- the handoff contains actual verification evidence.

## Manager note

After TASK-001 is MERGED, both TASK-002 and TASK-022 become eligible to move to READY, allowing the frontend/signal and secure-backend paths to begin in parallel.
