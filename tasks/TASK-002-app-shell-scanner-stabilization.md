# TASK-002 — App Shell and Early Scanner Stabilization

**Status:** ASSIGNED

**Owner:** `MGR-MA` — Muhammad Ahmad's Central Manager / Orchestrator acting as Scanner / Frontend implementer

**Depends on:** `TASK-001` — MERGED at product `main@9258ea86845bee6aef74c24ae929ed7afcc262ac`

**Product repository:** `Ahmad-Ali-Shah/Project-Vytal-`

**Product branch:** `rebuild/TASK-002-app-shell-scanner-stabilization`

## Objective

Port only the early shell/scanner UX stabilization that followed the root prototype: stable/skippable intro splash, replay control, responsive visibility of the honest Preview status, cleaner scanner status placement, desktop/webcam-aware fingertip placement handling, and the WebKit circular-viewfinder clipping fix.

This task MUST NOT port provider configuration UI, browser API-key entry, provider claims, referral/stress algorithm changes, or later rPPG pipeline work that was mixed into the historical commits.

## Historical Sources and Disposition

### `5b01ab330d77c49d169608ade8e29d3a3975a706` — PARTIAL
Historical message: `fix: resolve stress index score & referral flag consistency, optimize desktop webcam fingertip mode, add Figma logo pulse intro splash animation and interactive AI engine modal`

KEEP only:
- app-shell splash introduction pattern;
- `SplashAnimation` visual shell concept;
- scanner status banner placed above the circular viewfinder instead of overloading the camera surface;
- desktop/webcam-aware fingertip red-dominance thresholds using torch capability as a device signal;
- neutral fingertip guidance suitable for rear-camera or webcam capture.

EXCLUDE:
- `AiConfigModal.jsx`;
- browser API-key field;
- live provider test button;
- Groq/Qwen/DashScope provider-state UI;
- navbar AI-engine control;
- stress-score implementation changes;
- referral-policy changes;
- any clinical logic not strictly required for shell/scanner UX.

### `73874939aad877983bb597ccb19afca67605502f` — PARTIAL
Historical message: `fix: ensure splash animation timer stability on React hydration and add replay intro button in navbar for Vercel deployment`

KEEP:
- stable splash timers via a stored `onFinish` callback reference;
- one-shot timer lifecycle that does not reset when callback identity changes;
- click/tap-to-skip behavior;
- optional navbar Intro replay control.

SANITIZE:
- historical splash/provider wording such as `AI Triage`; current copy must describe camera-based screening and must not imply provider-backed AI or diagnosis.

### `2fb62e7a1fd5592340087756176b73e330abfbbd` — KEEP COMPATIBLE CSS ONLY
Historical message: `fix: ensure navbar status bar and AI Engine button stay visible across all responsive screen sizes`

KEEP:
- responsive navbar gap refinement;
- `.navbar__status` remains visible on small screens with compact typography.

EXCLUDE:
- there is no AI Engine button in the sanitized product, so do not restore one.

### `4bdb19271d6e23dbcdef9a7c527228704bdc5a8e` — PARTIAL UI-ONLY
Historical message: `perf: polish AI readout card, fix camera viewfinder webkit overflow mask, and optimize hybrid rPPG signal pipeline`

KEEP only:
- WebKit circular viewfinder clipping compatibility:
  - `-webkit-mask-image: -webkit-radial-gradient(white, black);`
  - `isolation: isolate;`

EXCLUDE:
- `Qwen & Groq AI Engine Ready` readout;
- provider-readiness copy;
- hybrid rPPG/signal-pipeline changes. Signal history starts with TASK-003 and must remain attributable there.

## Product Interfaces That Must Remain Stable

TASK-002 consumes the TASK-001 product contract:

- routes remain `/`, `/dashboard`, `/report`;
- `ScanPage` continues to call the existing local `fetchAIExplanation` interface;
- `src/lib/ai.js` remains provider-free;
- `src/lib/storage.js` remains session-memory preview storage;
- `src/lib/rppg.js` remains unchanged by TASK-002;
- no Supabase/backend feature is introduced.

TASK-002 produces:

- `src/components/SplashAnimation.jsx`;
- `App` splash lifecycle;
- `NavBar({ onReplayIntro })` optional replay interface;
- scanner status banner styling/placement;
- device-aware fingertip placement thresholds/guidance;
- WebKit-safe viewfinder clipping.

## TDD Contract

Before changing production files, add `tests/task002-shell-scanner.test.mjs` and confirm it fails because TASK-002 behavior is absent.

The test must verify at least:

1. `src/components/SplashAnimation.jsx` exists.
2. `App.jsx` renders `SplashAnimation` and passes an intro-replay callback to `NavBar`.
3. splash implementation stores the finish callback in a ref, uses a one-shot timer effect, and exposes skip behavior.
4. `NavBar.jsx` accepts `onReplayIntro` and exposes a neutral Intro replay control.
5. runtime source does NOT contain `AiConfigModal`, `Custom API Key`, `Test Live AI`, `Qwen`, `Groq`, `DashScope`, or a provider-key input path.
6. mobile CSS keeps `.navbar__status` visible and compact.
7. `.viewfinder` contains the WebKit radial mask and `isolation: isolate`.
8. `ScanPage.jsx` contains the scanner status banner above the viewfinder.
9. `ScanPage.jsx` contains torch-capability-aware fingertip threshold logic and webcam-compatible guidance.
10. existing TASK-001 contract tests remain green.

## Implementation Procedure

- [ ] Read this task, current `MASTER_RECONSTRUCTION_SPEC.md`, and latest `COMMUNICATION_LOG.md`.
- [ ] Confirm TASK-001 merge `9258ea86845bee6aef74c24ae929ed7afcc262ac` is the product base.
- [ ] Create `rebuild/TASK-002-app-shell-scanner-stabilization` from product `main`.
- [ ] Write TASK-002 failing contract test first.
- [ ] Run TASK-002 test and confirm RED for missing stabilization behavior.
- [ ] Create sanitized `SplashAnimation.jsx`.
- [ ] Modify `App.jsx` to control splash visibility/replay.
- [ ] Modify `NavBar.jsx` to expose optional Intro replay without provider controls.
- [ ] Modify `ScanPage.jsx` only for scanner status placement, fingertip placement compatibility and guidance.
- [ ] Modify `index.css` for splash styles, status banner, responsive status visibility, and WebKit viewfinder clipping.
- [ ] Do not modify `src/lib/rppg.js`.
- [ ] Do not add provider configuration or browser credentials.
- [ ] Run `npm test`.
- [ ] Run `npm run build`.
- [ ] Review product diff against `main`; confirm no signal/clinical/provider/backend scope slipped in.
- [ ] Commit using `feat(TASK-002): stabilize app shell and scanner UX` or equivalent task-scoped commit naming.
- [ ] Push branch and use the existing PR verification workflow for one bounded install/test/build run.
- [ ] Write `handoffs/TASK-002-handoff.md` with exact evidence.
- [ ] Stop for manager review before merge.

## Acceptance Criteria

TASK-002 may be accepted only when:

- intro splash is stable, skippable, and replayable;
- splash wording is screening-oriented and provider-neutral;
- Preview status remains visible responsively;
- scanner status is clearly placed above the camera circle;
- fingertip placement logic tolerates torchless webcam environments without claiming medical accuracy improvements;
- viewfinder clipping includes the compatible WebKit mask/isolation fix;
- no API-key/provider UI is restored;
- no Groq/Qwen/DashScope runtime claim is restored;
- no stress/referral/rPPG algorithm change is attributed to this task;
- `src/lib/rppg.js`, storage authority, and backend boundary remain unchanged;
- existing and new tests pass;
- production build passes;
- handoff contains actual verification evidence.

## Manager Unlock Note

After TASK-002 is MERGED:
- TASK-003 becomes READY for `AAS-CLINICAL`.
- TASK-021 also becomes dependency-ready on the frontend path, but manager controls when it is actually assigned relative to the signal chain and integration plan.
