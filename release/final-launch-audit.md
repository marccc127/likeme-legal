# Final Launch Audit

Date: 2026-06-17
Device baseline: iPhone Air simulator
Current verdict: `NO-GO`

This file is the operator-facing end state for launch freeze. It answers one question only:

Can this repo ship to TestFlight or live right now?

## Short answer

- Internal app readiness: `GO-leaning`
- External launch readiness: `NO-GO`

The app itself is currently in a launch-ready state by code, QA, and release-flow evidence. The final in-app personalization gap is closed: later Add Case runs now capture the same headspace fields as onboarding and feed the existing personalized surfaces without changing score logic. The remaining blockers are external live configuration values that are still absent from this workspace.

The local handoff path is now also proven repo-side: `launch:check` and `testflight:check` both succeed when the required values are present in `.env.local`, without needing extra manual shell exports.

## Proven current state

### 1. App-side evidence

These current gates are green:

- `npm run typecheck`
- `npm run test`
- release-candidate Maestro inventory on iPhone Air
- final later-case personalization slice on iPhone Air: Check Relevance/Want capture, verdict narrative, Move On handoff, Daily handoff, paywall fit, and notification carry-forward
- monetization fallback proof on missing billing config
- persistence / relaunch / reset proof
- TestFlight build path now hard-stops on readiness gates before starting EAS

Primary evidence lives in:

- [release-candidate-audit.md](/Users/marc-philliphansen/Projekte/Forks/likeme/docs/qa/release-candidate-audit.md)
- [acceptance-checklist.md](/Users/marc-philliphansen/Projekte/Forks/likeme/docs/qa/acceptance-checklist.md)

### 2. Current blocker evidence

#### `npm run launch:check`

Current result:

```text
MISSING  Expo EAS project id for OTA
MISSING  RevenueCat iOS API key
MISSING  RevenueCat weekly product
MISSING  RevenueCat yearly product
MISSING  RevenueCat one-time product
MISSING  Verdict proxy URL
```

Interpretation:

- the repo is still missing the live OTA project id
- the repo is still missing all required live RevenueCat values
- the repo is still missing the live verdict proxy URL

#### `npm run testflight:check`

Current result:

```text
OK  app.config.ts — present
OK  eas.json — present
MISSING  launch config — run npm run launch:check
OK  Expo login — hnsn127 marccc127@gmail.com
MISSING  OTA project id — EXPO_PUBLIC_EAS_PROJECT_ID is not set
```

Interpretation:

- Expo login is present
- OTA/TestFlight code wiring exists
- TestFlight remains blocked only by live launch config

#### `npm run launch:sweep`

Current result:

```text
typecheck: passed
tests: 25 files, 94 tests passed
launch:check: failed on missing live config
```

Interpretation:

- code and test gates are currently green
- the release sweep stops only where launch config is still incomplete
- the newest in-app QA pass also leaves no confirmed P0/P1 blocker in normal case creation or downstream personalization

## Exact remaining blockers

The current blocker list is short and concrete:

1. `EXPO_PUBLIC_EAS_PROJECT_ID`
2. `EXPO_PUBLIC_REVENUECAT_IOS_API_KEY`
3. `EXPO_PUBLIC_REVENUECAT_PRODUCT_WEEK`
4. `EXPO_PUBLIC_REVENUECAT_PRODUCT_YEAR`
5. `EXPO_PUBLIC_REVENUECAT_PRODUCT_ONCE`
6. `EXPO_PUBLIC_VERDICT_PROXY_URL`

Optional only if needed:

7. `EXPO_PUBLIC_REVENUECAT_ENTITLEMENT_ID`

## Exact last steps to TestFlight

1. Fill the live values in `.env.local` or export them in shell.
2. Run `npm run launch:check`.
3. Run `npm run testflight:check`.
4. Run `npm run launch:sweep`.
5. If all three pass, run `npm run testflight:build`.

The source-of-truth setup instructions are in:

- [live-config-handoff.md](/Users/marc-philliphansen/Projekte/Forks/likeme/docs/release/live-config-handoff.md)

## GO condition

This project becomes `GO` for TestFlight when all of the following are simultaneously true:

- `npm run launch:check` passes
- `npm run testflight:check` passes
- `npm run launch:sweep` passes end to end
- no new P0/P1 issue appears in the release path

Until then, the correct operator status remains:

`NO-GO because live config is incomplete, not because the app is internally unfinished.`
