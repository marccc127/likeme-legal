# Reality Check Acceptance Checklist

Purpose: launch-facing acceptance criteria for real user flows, not just green tests.

Status legend:
- `PASS` proven by current code + recent iPhone Air QA evidence
- `BLOCKED` not acceptable for launch until external state is supplied
- `CHECK AT GO-LIVE` must be rerun with real live config before ship

## A. Product Truthfulness

### AC-A1 Onboarding promise matches delivered value
The app must not promise a deep personalized read and then show generic filler.

Acceptance:
- Onboarding hook, testimonial, analyzing, and first verdict must connect as one coherent promise.
- Verdict copy must visibly use the user context, score, headspace fields, flags, and when present the replay moment.
- Locked verdict and paywall must still feel grounded in the user case, not like a detached generic upsell.

Current status: `PASS`
Evidence:
- Flow 08 release screenshots
- Flow 19 normal Check headspace capture
- Flow 62 later-case verdict handoff
- Flow 52 skeptic proof
- Flow 53 locked proof teaser
- Flow 54 paywall proof continuity

### AC-A2 Screen content must be plausible to a real user
No screen may show debug-ish, placeholder, contradictory, or logically wrong content.

Acceptance:
- Daily, Wall, Move On, Verdict, and Paywall copy must read like finished consumer product text.
- Premium copy must match the actual unlocked benefit.
- Notification preview copy must align with the current user state and pattern history.

Current status: `PASS`
Evidence:
- Daily personalization flows 21, 42, 48
- Wall intelligence flows 28, 46, 47
- Paywall personalization flows 37, 38, 54

## B. First-Time User Flow

### AC-B1 A new user can reach a verdict without confusion or clipping

Acceptance:
- Hook -> onboarding -> testimonial -> analyzing -> verdict completes cleanly.
- No step is clipped, blocked by keyboard, or visually broken on iPhone Air.
- Voice entry is optional, text path remains fully usable.

Current status: `PASS`
Evidence:
- Flows 05, 08, 18
- keyboard fixes in onboarding and input screens

### AC-B2 The first locked verdict makes sense before purchase

Acceptance:
- Free verdict shows enough signal to feel credible.
- Unlock prompt does not overclaim.
- If billing is unavailable, the screen must say so honestly and must not pretend to sell.

Current status: `PASS`
Evidence:
- Flows 02, 53, 55

## C. Returning User / Case Loop

### AC-C1 A returning user can add a new case and get the right next state

Acceptance:
- Empty wall leads into Add Case cleanly.
- Later Add Case runs capture the same `dailyThought` and `desiredOutcome` headspace fields as onboarding.
- Populated wall re-entry works.
- Keyboard, sticky CTAs, and tab navigation stay stable.
- Score calculation stays unchanged; the new inputs feed personalization only.

Current status: `PASS`
Evidence:
- Flows 01, 07, 14, 19, 57, 60, 61, 62

### AC-C2 The app must read repeated behavior as repeated behavior

Acceptance:
- Multi-case users see pattern surfaces on Wall, Daily, Move On, and Premium.
- Repeat-loop users get stronger annual framing than one-off users.
- Later-case headspace inputs can inform those surfaces without introducing a new scoring model.

Current status: `PASS`
Evidence:
- Flows 22, 38, 42, 44, 45, 46, 47, 48, 49, 62, 64, 69

## D. Monetization Integrity

### AC-D1 Purchases must reflect the real billing state

Acceptance:
- With missing live billing config, purchase/manage/restore must be disabled or blocked honestly.
- With explicit E2E billing flags, QA purchase states must still work in native Release builds.
- Annual recommendation must only appear where the user behavior justifies it.

Current status: `PASS` for app behavior, `BLOCKED` for real live billing
Evidence:
- Flows 38, 40, 55, 56
- runtime QA flag hardening in `app.config.ts` + `src/services/runtimeFlags.ts`

### AC-D2 Paywall recommendations must be logically consistent

Acceptance:
- One-off users default to weekly.
- Repeat-loop users can default to annual.
- Preview/offline billing state must not show fake “most picked” sales framing.

Current status: `PASS`
Evidence:
- `src/services/paywallStrategy.ts`
- `src/services/paywallStrategy.test.ts`
- Flow 38 screenshot
- Flow 55 screenshot

## E. Retention / Notifications / Share

### AC-E1 Notification prompts must respect user timing

Acceptance:
- No startup prompt appears without user context.
- Soft ask appears only at the right moment.
- Granted/denied/settings recovery flows work.

Current status: `PASS`
Evidence:
- Flows 04, 10, 11
- RC-016 notes in release audit

### AC-E2 Share flows must work without breaking the main verdict experience

Acceptance:
- Locked teaser share works.
- Unlocked clean share works.
- E2E capture mode works in native Release builds without the system share sheet.

Current status: `PASS`
Evidence:
- Flows 17, 23

### AC-E3 Move On and Daily must not feel like empty stubs

Acceptance:
- Empty and populated states must be different and logically correct.
- Content must react to real case history, not static filler.

Current status: `PASS`
Evidence:
- Flows 07, 21, 29, 30, 42, 48, 57, 58

## F. Failure / Safety / Fallbacks

### AC-F1 Failure states must degrade honestly

Acceptance:
- LLM/network failure must still yield a coherent SAFE verdict.
- Purchase failure must surface an understandable error.
- Billing-off builds must not fake unlocks.

Current status: `PASS`
Evidence:
- Flow 16
- Flow 20
- Flows 55, 56

### AC-F2 Sensitive cases must not be mishandled

Acceptance:
- Crisis-like input must divert to support messaging.
- Voice denied / unsupported states must remain usable.

Current status: `PASS`
Evidence:
- Flows 09, 12, 13

## G. Launch Operations

### AC-G1 The repo must be able to prove release readiness on command

Acceptance:
- `npm run typecheck`
- `npm run test`
- `npm run launch:check`
- `npm run testflight:check`
- `npm run launch:sweep`

Current status:
- `PASS`: typecheck, tests, testflight precheck behavior, release sweep behavior
- `CHECK AT GO-LIVE`: `launch:check` and full `launch:sweep` with real live values

### AC-G2 Real release infra must exist before ship

Acceptance:
- Real RevenueCat iOS key
- Real RevenueCat product ids
- Real proxy URL
- Real Expo EAS project id
- Valid Expo login/session for EAS/TestFlight

Current status: `BLOCKED`

## Current Roadblock Verdict

### In-app roadblockers
Current status: none confirmed.

Meaning:
- No currently known P0 in app logic, navigation, layout, share, or QA-only release paths after the fresh persistence reruns.
- Remaining fixes are mostly release-fidelity maintenance, not product rescue.

### External roadblockers
Current status: still real and launch-blocking.

Blocked by:
- missing live RevenueCat values
- missing `EXPO_PUBLIC_VERDICT_PROXY_URL`
- missing `EXPO_PUBLIC_EAS_PROJECT_ID`
- live launch config is still incomplete even though Expo login/session is currently present

## Required Go-Live Recheck

Before actual ship, rerun:

1. `npm run launch:check`
2. `npm run testflight:check`
3. `npm run launch:sweep`
4. Final iPhone Air visual pass on:
   - onboarding
   - locked verdict
   - unlocked verdict
   - paywall
   - settings billing state

If all four pass with real live config, the app-side acceptance gate is satisfied.
