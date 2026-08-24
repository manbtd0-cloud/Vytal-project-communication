# TASK-003 — POS/CHROM Hybrid rPPG

**Status:** ASSIGNED

**Owner:** `AAS-CLINICAL` — Ahmad Ali Shah's Clinical Algorithms + QA AI

**Depends on:** `TASK-002` — MERGED at product `main@1f8b1b1b95c11a309ed8e55f59d1306004b2d498`

**Product repository:** `Ahmad-Ali-Shah/Project-Vytal-`

**Product branch:** `rebuild/TASK-003-pos-chrom-hybrid-rppg`

**Historical source repository:** `Ahmad-Ali-Shah/Vital`

**Primary historical source:** `dc2e25ea9392bd00b320fe38fc821a958315a2de`

Historical message: `feat: implement POS (Wang et al., 2016) + CHROM (de Haan & Jeanne, 2013) hybrid rPPG extraction with harmonic peak verification to eliminate sub-harmonic heart rate traps`

## Objective

Upgrade only the signal-extraction core from CHROM-only to a POS + CHROM hybrid and add harmonic peak verification for heart-rate peak selection.

This task is intentionally narrow. The historical source commit mixed the desired hybrid extraction with several unrelated tuning and clinical-behavior changes. Those unrelated changes MUST NOT be replayed here.

## Source Disposition

### KEEP

From `dc2e25ea...`, port the following ideas into the current sanitized product implementation:

1. Defensive mean/std/median handling where required to avoid divide-by-zero/empty-array failure in the new signal path.
2. `posSignal(r, g, b)` implementing the Plane-Orthogonal-to-Skin projection.
3. Existing `chromSignal(r, g, b)` retained as the second extraction path.
4. Equal-weight POS + CHROM combination before detrending/high-pass filtering unless testing demonstrates an equivalent formulation is required for numerical stability.
5. Harmonic peak verification in the BPM search so a strong doubled-frequency harmonic can replace a suspicious low-frequency peak.
6. Clear source comments naming POS and CHROM as research signal-processing methods, without claiming clinical-device equivalence.

### EXCLUDE / DEFER

Do NOT import these mixed-commit changes during TASK-003:

- changing `HR_MIN_BPM` / `HR_MAX_BPM` merely because the historical commit changed them;
- changing `BR_MIN_BPM` / `BR_MAX_BPM`;
- changing `MIN_SAMPLES_MS`;
- changing `MIN_WINDOW_SNR`;
- changing window length/step/timing;
- changing capture-rate acceptance;
- adding heart-rate-derived stress fallbacks;
- changing the stress formula;
- fabricating breathing rate with a fallback such as `15` when no valid breathing estimate exists;
- changing referral policy;
- changing UI/provider/backend/storage behavior;
- changing camera placement logic from TASK-002.

Parameter/SNR/timing refinement belongs to TASK-004 and later accuracy work. Clinical-policy changes belong to later clinical tasks.

## Current Product Contract That Must Be Preserved

At product `main@1f8b1b1b...`:

- `src/lib/rppg.js` is the only production file TASK-003 is expected to modify unless tests require a test-only file.
- `analyzeSignal(samples)` remains the public interface.
- insufficient/invalid input returns `null` rather than inventing a reading.
- breathing rate remains `null` if a valid estimate is unavailable.
- stress remains the existing short-window variability proxy and is not redefined in TASK-003.
- scanner/UI/session-storage/provider boundaries from TASK-001/002 remain unchanged.

## Required TDD Work

Before changing `src/lib/rppg.js`, add a dedicated TASK-003 test file and establish RED for the missing hybrid behavior.

Recommended path:

`tests/task003-pos-chrom-rppg.test.mjs`

The tests must cover at minimum:

1. Existing baseline contract remains green.
2. `src/lib/rppg.js` contains a POS extraction path in addition to CHROM.
3. `analyzeSignal` combines POS and CHROM before the existing detrend/high-pass/window flow.
4. Harmonic verification exists in BPM peak selection.
5. Invalid/too-short/too-sparse input still returns `null`.
6. Missing breathing information is never replaced with a fabricated normal-looking default.
7. Existing stress logic remains materially unchanged by TASK-003.
8. Existing signal/timing constants remain unchanged unless an exact, documented numerical necessity is proven and approved by MGR-MA before implementation.
9. Add at least one deterministic synthetic RGB trace test where the hybrid analyzer recovers a known pulse frequency within a stated tolerance.
10. Add a deterministic harmonic/sub-harmonic case demonstrating that the peak-selection logic avoids the intended low-frequency trap.

Do not weaken or delete existing TASK-001/TASK-002 tests to make TASK-003 pass.

## Implementation Procedure

- [ ] Pull/read latest communication repository state.
- [ ] Confirm `AAS-CLINICAL` is READY.
- [ ] Read `MASTER_RECONSTRUCTION_SPEC.md`.
- [ ] Read `COMMUNICATION_PROTOCOL.md` and latest `COMMUNICATION_LOG.md` entries.
- [ ] Read this complete TASK-003 file.
- [ ] Inspect product `main@1f8b1b1b95c11a309ed8e55f59d1306004b2d498` and branch `rebuild/TASK-003-pos-chrom-hybrid-rppg`.
- [ ] Inspect historical source commit `dc2e25ea9392bd00b320fe38fc821a958315a2de` carefully.
- [ ] Write TASK-003 tests first and confirm RED for the missing POS/harmonic behavior.
- [ ] Implement only the approved signal-extraction/harmonic subset.
- [ ] Run `npm test`.
- [ ] Run `npm run build`.
- [ ] Review the complete product diff against `main`.
- [ ] Confirm no UI/provider/backend/referral/stress/timing work slipped in.
- [ ] Commit with task-scoped naming, preferably `feat(TASK-003): add POS CHROM hybrid rPPG extraction`.
- [ ] Push the branch if write credentials are available.
- [ ] Create `handoffs/TASK-003-handoff.md` in the communication repo using the handoff template and append the required HANDOFF message to `COMMUNICATION_LOG.md`.
- [ ] STOP for MGR-MA review. Do not self-assign TASK-004.

## No-Push Fallback

If the AI environment still lacks GitHub write credentials:

1. Perform the implementation and verification locally on the exact TASK-003 branch/base.
2. Return to Ahmad Ali Shah:
   - exact changed file contents or a clean unified patch;
   - exact test file contents;
   - commands executed and full PASS/FAIL summary;
   - intended commit message;
   - exact handoff document;
   - exact COMMUNICATION_LOG HANDOFF entry.
3. Do not claim the task is persisted or complete until the changes are actually committed/pushed by Ahmad Ali Shah or MGR-MA.

## Acceptance Criteria

TASK-003 may be accepted only if:

- POS + CHROM hybrid extraction is genuinely present;
- harmonic peak verification is genuinely present;
- synthetic verification demonstrates expected pulse-frequency behavior;
- old tests remain green;
- new TASK-003 tests are green;
- production build passes;
- no fabricated breathing default is introduced;
- no stress/referral policy change is introduced;
- no timing/SNR tuning belonging to TASK-004 is pulled forward;
- no UI/provider/backend/storage change is introduced;
- handoff contains exact source SHA, product branch/SHA, tests, build result, and exclusions.

## Manager Unlock Note

After TASK-003 is reviewed, accepted, and MERGED, `TASK-004` becomes READY for `AAS-CLINICAL`.
