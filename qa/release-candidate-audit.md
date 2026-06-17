# Reality Check Release-Candidate Audit

Date: 2026-06-16
Device baseline: iPhone Air simulator, iOS 26.4, 420x912 screenshots
Visual reference: `RealityCheck-App-standalone v2.html` plus the rendered `reference-v2-*.png` snapshots

## Standing Maestro QA Rule

Every Maestro flow in this project is a release-candidate QA artifact, not a pass/fail shortcut. For every current and future Maestro run:

- read the full command log;
- inspect debug screenshots and hierarchy when a screen is visited or fails;
- compare visually against the HTML reference where relevant;
- classify findings as P0/P1/P2;
- fix visual, copy, logic, navigation, safe-area, keyboard, modal, clipping, overlap, or state issues even if assertions pass;
- never mark a flow done until the user experience is correct, not merely automated.

## Screen Inventory

- [x] Onboarding Hook: first-run score promise, skip, CTA, disclaimer.
- [x] Onboarding Commitment: name input, back, disabled/enabled CTA.
- [x] Onboarding Context: context chips, back, disabled/enabled CTA.
- [x] Onboarding Quiz Q1-Q6: progress, option selection, auto-advance.
- [x] Onboarding Relevance: daily-thought select.
- [x] Onboarding Want: desired outcome select.
- [x] Onboarding Flags: evidence grid, sticky Done CTA.
- [x] Onboarding Moment: text input, voice input, skip, continue, keyboard.
- [x] Onboarding Testimonial: paper review, final CTA.
- [x] Wall Loading: hydration placeholder.
- [x] Wall Empty: no cases, add-first-case CTA, settings.
- [x] Wall Populated: stats, case grid, add tile, case-card navigation.
- [x] Check Intro: name input, context chips, disabled/enabled CTA.
- [x] Check Quiz Q1-Q6: progress, option selection, auto-advance, back.
- [x] Check Relevance: daily-thought select.
- [x] Check Want: desired outcome select.
- [x] Check Flags: evidence grid, sticky Done CTA.
- [x] Check Moment: text input, voice input, skip/build CTA, keyboard.
- [x] Analyzing: spinner, animated percent, checklist, progress, ticker.
- [x] Crisis Support: moderation fallback support screen.
- [x] Verdict Locked: free score, stamp, locked depth, share teaser, unlock CTA.
- [x] Verdict Unlocked: receipts, character card, thoughts, share, add another.
- [x] Rating Prompt: modal sheet, primary, Not now.
- [x] Notification Soft Ask: modal sheet, primary, Not now, iOS permission handoff.
- [x] Paywall: locked cards backdrop, plans, annual weekly-price emphasis, purchase, dismiss.
- [x] Settings: plan, restore/manage, notification toggles, permission state, privacy, delete confirm, about links.
- [x] Daily Stub: daily card, reactions, tab navigation.
- [x] Move On Stub: teaser, tab navigation.
- [x] Share Export: offscreen 9:16 and 4:5 cards, Share sheet.
- [x] iOS Speech/Microphone Permission: granted, denied, unavailable recognizer.
- [x] iOS Notification Permission: granted, denied, skipped.

## Navigation Map

- [x] First launch: Onboarding Hook -> Commitment -> Context -> Quiz -> Relevance -> Want -> Flags -> Moment -> Testimonial -> Analyzing -> Verdict.
- [x] Skip launch: Onboarding Hook -> Wall Empty.
- [x] Returning user empty: Wall Empty -> Add first case -> Check.
- [x] Returning user populated: Wall Populated -> Case Card -> Verdict.
- [x] Main tabs: Wall <-> Daily <-> Move On with no duplicate/broken stacks.
- [x] Add case: Wall -> Check Intro -> Quiz -> Relevance -> Want -> Flags -> Moment -> Analyzing -> Verdict.
- [x] Verdict locked: share teaser, notification/rating prompts, unlock paywall, dismiss returns locked verdict.
- [x] Purchase: Paywall -> unlock -> Verdict Unlocked.
- [x] Settings: Wall -> Settings -> back, restore/manage, toggles, delete confirm.
- [x] Permission recovery: Moment voice denied -> Settings link; Notification accepted -> iOS system prompt -> rating prompt.
- [x] Error recovery: purchase failure message, LLM proxy fallback, crisis path to Wall.

## Issue Register

| ID | Severity | Area | Finding | Status |
| --- | --- | --- | --- | --- |
| RC-001 | P0 | Check Flags | Done CTA was partly hidden behind bottom edge and Maestro could not reliably progress. | Fixed with sticky footer; multiple downstream Air flows now progress through Flags into Moment. Dedicated Flags visual sign-off is still pending. |
| RC-002 | P1 | Onboarding Commitment | Second onboarding title was reported clipped. | Fixed with larger line-height; visually verified on iPhone Air screenshot. |
| RC-003 | P1 | Check/Onboarding Moment | User needs voice input; spoken moment must influence LLM verdict without exposing API key. | Fixed with on-device dictation into editable `moment`; Check Moment visual flow passed and screenshot verified. |
| RC-004 | P1 | Maestro Flow 02 | Test asserted transient Analyzing title; the screen may advance before assertion. | Fixed by waiting for stable Verdict; downstream reruns passed on iPhone Air. |
| RC-005 | P1 | Visual QA Process | HTML visual reference was not screenshot-compared; Playwright not installed. | Fixed for local QA: Playwright + Chromium installed and `reference-v2-onboarding/paywall/verdict.png` rendered for comparison. |
| RC-006 | P1 | Daily/Move On | Stub copy included prototype-like labels (`V2`, `Coming in V3`). | Fixed copy to user-facing `tap`, `starts here`, and `Preview`; Flow 07 screenshots verified with stable tab layout and no top clipping. |
| RC-007 | P1 | Notification Prompt | Prompt was clipped risk on small devices and Maestro captured the sheet mid-transition. | Fixed with safe-area bottom padding, shorter copy, and `waitForAnimationToEnd` before visual screenshots; Flow 02 notification screenshot verified. |
| RC-008 | P0 | Maestro Environment | Parallel local iOS Maestro runs for Sanctuary and Reality Check were colliding on the same host/XCTest driver port (`7001`), which could route the wrong UI hierarchy and screenshots into the Reality Check flow. | Root cause confirmed in Maestro debug logs. Fixed operationally by pinning Reality Check runs on the iPhone Air to `--driver-host-port 7005` while Sanctuary remains on `7001`; fresh Air reruns stayed isolated and visually correct. |
| RC-009 | P0 | Add Case Navigation | Analyzing could navigate to Verdict while Wall remained visibly active in the hierarchy. | Fixed with pending reveal handoff through Wall; Flow 02 verified. |
| RC-010 | P1 | Locked Verdict | Footer share label wrapped and locked-card blurred text overlapped overlay text. | Fixed with compact Share CTA, stronger overlay, two-card locked preview; Flow 02 screenshot verified. |
| RC-011 | P1 | Verdict Score | Large Anton score was clipped or still appeared clipped at the top on locked verdict. | Fixed and verified: score glyphs reduced slightly with larger line-height/top-bottom reserve; fresh Flow 02 locked-verdict screenshot shows no top clipping. |
| RC-012 | P1 | Unlocked Verdict | Rating prompt appeared immediately over the newly unlocked premium verdict, blocking the reveal. | Fixed by suppressing peak prompts for unlocked verdicts; Flow 03 screenshot verified. |
| RC-013 | P1 | Settings Notifications | Settings exposed technical notification wording (`undetermined`, notification service language) during the notification flow. | Fixed with user-facing system-status copy and calmer notification description; Flow 04 passed and screenshots verified. |
| RC-014 | P1 | Input Keyboard Layout | Onboarding/Check input steps could leave the primary CTA partially behind the iOS keyboard. | Fixed by collapsing the bottom spacer while the keyboard is open on commitment and moment/input steps; rerun confirmed onboarding flow can progress past commitment. |
| RC-015 | P1 | Onboarding Analyzing Visual QA | The onboarding path previously skipped past the transient analyzing screen before Maestro could visually assert it. | Fixed with an `EXPO_PUBLIC_E2E=1`-only hold on `Analyzing`, plus a shorter settle timeout on the verdict CTA; fresh Flow 08 screenshots verified testimonial, analyzing, and verdict. |
| RC-016 | P1 | iOS Notification Entry State | A prior iPhone Air Maestro run showed an early iOS notification prompt before the in-app soft ask, suggesting broken sequencing. | Re-tested with a minimal launch-only flow on iPhone Air (`notifications: unset`) and the prompt did not appear. No startup notification-permission request exists in app code; the request path is only triggered from the verdict soft ask. Current conclusion: simulator/Maestro permission-state nondeterminism, mitigated in flows `10` and `11` with explicit optional alert handling. |
| RC-017 | P1 | Verdict -> Paywall Prompt Collision | The delayed notification soft ask could appear over the paywall sheet if the user opened paywall quickly from the locked verdict. | Fixed by clearing/suppressing verdict peak prompts whenever the verdict screen loses focus. Fresh Flow `14` on iPhone Air verified normal paywall entry, back-to-wall, populated grid, and case re-entry. |
| RC-018 | P0 | Launch Config | `app.json` placeholder RevenueCat values were taking precedence over real env values in `revenueCat.ts`, and the current workspace still has no real RevenueCat live values, no `EXPO_PUBLIC_VERDICT_PROXY_URL`, and no Expo EAS project id configured for OTA/TestFlight. | Code fixed so env now overrides app-config placeholders. `expo-updates`, dynamic `app.config.ts`, `eas.json`, and a stricter `npm run launch:check` now prove launch readiness for RevenueCat, proxy, and OTA wiring. Current external state still fails that check, so launch/TestFlight remain blocked until the real live values, proxy URL, and EAS project id are supplied. Expo login is now present locally again. |
| RC-019 | P0 | Monetization Safety | Release builds without live RevenueCat config could still present placeholder pricing and simulate unlocks, which is unacceptable for launch. | Fixed by gating purchases behind real live RevenueCat config unless explicit E2E simulation is enabled. The paywall now shows preview-only pricing, non-interactive plans, a disabled CTA, and a clear unavailable message when live billing is missing; Flow 55 verified the fallback visually on iPhone Air. |
| RC-020 | P1 | Delete All Cases | `Delete all cases` only removed case records, which left case-linked reset state like Move On progress and reopen history alive under the hood. | Fixed by resetting case-linked Move On and re-entry stores alongside cases. Fresh Flow 57 verifies populated wall -> Settings delete confirm -> empty Wall -> empty Move On state on iPhone Air. |
| RC-021 | P0 | Persistence / Returning Launch | Native persistence had silently fallen back to in-memory state because `react-native-mmkv` v4 was being initialized with the wrong API shape, which put returning-user launch, delete/recreate recovery, and relaunch trust at risk. | Fixed by supporting `createMMKV(...)`, falling back only when necessary, and using the native `remove()` path for deletes. Fresh Flows 57, 58, 60, and 61 on iPhone Air now prove delete reset, generic Daily fallback, relaunch into the correct empty returning-user wall, recreate after reset, and case history surviving a further relaunch. The simulator data container now contains `Documents/mmkv/reality-check`, confirming native persistence is active again. |
| RC-022 | P1 | Later-Case Personalization | Normal Add Case runs were less personalized than onboarding because they did not capture the user's current headspace (`dailyThought`) or desired outcome. | Fixed without changing score logic: Check now asks the same Relevance and Want single-selects after Q6 and before Flags. Fresh Flows 19, 38, 62, 64, and 69 prove the new required steps, verdict personalization, paywall fit, Daily handoff, Move On handoff, and notification carry-forward remain clean on iPhone Air. |

## Current Verification

- [x] `npm run typecheck`
- [x] `npm run test`
- [x] `npx expo install --check`
- [x] iOS export after voice-input install
- [x] `pod install` after `expo-speech-recognition`
- [x] Maestro syntax checks for existing flows
- [x] Flow 01 pass with fresh hook and empty-wall screenshots
- [x] Flow 05 pass with hook and commitment screenshots
- [x] Release rebuild with speech recognition
- [x] Flow 02 rerun after score-clipping hardening
- [x] Flow 03 pass after unlocked prompt suppression and scroll-aware assertions
- [x] Flow 04 pass after rebuild and Settings notification screenshots inspected
- [x] Flow 06 visual Check Moment Voice passed with screenshot
- [x] Flow 07 main tabs visual pass with screenshots inspected
- [x] Flow 08 onboarding value path fully visually signed off
- [x] Flow 09 voice-permission denied path with screenshot
- [x] Flow 10 notification accept path on iPhone Air with isolated Maestro port
- [x] Flow 11 notification denied path on iPhone Air with isolated Maestro port
- [x] Flow 12 crisis support path after keyboard/scroll fix with screenshot
- [x] Flow 13 voice-unavailable path on iPhone Air with QA-only unsupported recognizer build
- [x] Flow 14 populated wall return path after verdict/paywall focus fix
- [x] Flow 15 wall loading placeholder path on iPhone Air
- [x] Flow 16 paywall loading + purchase error path on iPhone Air
- [x] Flow 17 teaser share -> unlock -> clean share path on iPhone Air
- [x] Flow 18 onboarding Context/Quiz/Relevance/Want/Flags/Moment visual pass on iPhone Air
- [x] Flow 19 Check Intro/Quiz/Relevance/Want/Flags visual pass on iPhone Air
- [x] Flow 20 unlocked SAFE fallback visual pass on iPhone Air
- [x] Flow 40 subscription unlocks future cases rerun after paywall-surface changes
- [x] Flow 54 paywall proof continuity visual pass on iPhone Air
- [x] Flow 55 missing-config paywall fallback visual pass on iPhone Air
- [x] Flow 56 settings missing-config billing fallback visual pass on iPhone Air
- [x] Flow 57 delete-all-cases reset path on iPhone Air
- [x] Flow 58 delete-all -> Daily generic fallback on iPhone Air
- [x] Flow 60 reset -> relaunch empty returning-user wall -> recreate case on iPhone Air
- [x] Flow 61 relaunch with stored case history on iPhone Air
- [x] Flow 62 unlocked verdict -> Move On source-context handoff on iPhone Air
- [x] Flow 64 unlocked verdict -> Daily source-context handoff on iPhone Air
- [x] Flow 65 locked verdict -> Daily source-context handoff on iPhone Air
- [x] Flow 66 Daily reaction -> follow-up -> Move On handoff on iPhone Air
- [x] Flow 67 Move On momentum and day-logged completion states on iPhone Air
- [x] Flow 68 Daily reflects closed Move On reset state on iPhone Air
- [x] Flow 69 notification preview reflects closed Move On reset state on iPhone Air
- [x] Flow 70 notification preview reflects open Move On reset state on iPhone Air
- [x] Flow 71 notification preview keeps the active mode visible on iPhone Air
- [x] Full screenshot audit across inventory
- [x] HTML v2 reference rendered with Playwright for onboarding/paywall/verdict comparison
- [x] `EXPO_PUBLIC_EAS_PROJECT_ID=... npx expo config --json` resolves OTA url + runtimeVersion correctly
- [x] local iPhone Air release build still passes after adding `expo-updates`
- [x] `npm run testflight:check` fails cleanly on the remaining external blockers instead of failing later inside EAS
- [x] `npm run launch:sweep` proves code/test gates pass and then stops only on missing live launch config
- [ ] `npm run launch:check` with real live RevenueCat/proxy values
- [x] Live-config handoff doc added: `docs/release/live-config-handoff.md`

Flow 08 sign-off note: build the iOS Release artifact with `EXPO_PUBLIC_E2E=1` before running the flow so Maestro can hold the transient `Analyzing` screen long enough for visual QA. Production builds are unaffected. Reran after the runtime-flag hardening so the testimonial, analyzing, and verdict screenshots still prove the native Release path.

Flow 02 sign-off note: reran on a fresh normal Release build after the recent paywall and prompt-surface changes. The notification soft ask, rating prompt, locked verdict, paywall dismiss path, and post-dismiss locked state still behave correctly and remain visually clean on iPhone Air.

Flow 09 sign-off note: reran on a fresh normal Release build after the recent voice-surface hardening. The denied-permission card still shows the right copy and Settings escape hatch on iPhone Air.

Flow 16 sign-off note: build the iOS Release artifact with `EXPO_PUBLIC_E2E=1`, `EXPO_PUBLIC_E2E_PAYWALL_PLANS_DELAY_MS=7000`, and `EXPO_PUBLIC_E2E_PURCHASE_RESULT=error` before running the flow so the loading and purchase-error states stay visually inspectable. Reran after the runtime-flag hardening; the loading card and purchase-error message still verify cleanly on iPhone Air.

Flow 17 sign-off note: build the iOS Release artifact with `EXPO_PUBLIC_E2E=1`, `EXPO_PUBLIC_E2E_SHARE_CAPTURE=1`, and `EXPO_PUBLIC_E2E_DISABLE_PEAK_PROMPTS=1` before running the flow so teaser and clean share exports can be asserted without invoking the native share sheet. Reran after the runtime-flag hardening; both teaser and unlocked share captures still pass in the Release path.

Flow 13 sign-off note: build the iOS Release artifact with `EXPO_PUBLIC_E2E=1` and `EXPO_PUBLIC_E2E_VOICE=unsupported` so the unavailable-recognizer state is embedded through runtime flags. Reran after the runtime-flag hardening; the fallback copy stays visually clean and the case flow remains usable.

Flow 19 sign-off note: reran on a fresh Release build after adding the two headspace steps to normal Check. The Add Case path now visually proves the same required `dailyThought` and `desiredOutcome` capture as onboarding before the user reaches Flags.

Flow 38 sign-off note: build the iOS Release artifact with `EXPO_PUBLIC_E2E=1` so the runtime QA flags are embedded through `app.config.ts`. The flow now buys `Just this verdict` on case one, then verifies the repeat-loop annual-fit paywall on case two without accidentally granting a weekly subscription first.

Flow 62 sign-off note: reran on a fresh Release build after adding later-case headspace capture and compacting the verdict-to-Move-On handoff detail. The unlocked verdict now uses the new `closure` and daily-headspace inputs in the narrative, and the Move On teaser no longer clips on iPhone Air.

Flow 57 sign-off note: reran on a fresh normal Release build after tightening the delete path. The user can create a case, return to Wall, open Settings, confirm delete, land back on the true empty Wall, and see the empty Move On state with `0` cases informing the plan.

Flow 58 sign-off note: reran on a fresh normal Release build to prove that delete is not only visual on the Wall. After deleting the only case, Daily falls back to the generic `wall not built yet` state instead of continuing to render personalized case-driven content.

Flow 60 sign-off note: reran immediately after the destructive reset proof on the same fresh Release build. After a true app relaunch, the app returns to the empty Wall as a returning user instead of throwing the user back into onboarding, and the next case can be created end to end without broken navigation.

Flow 61 sign-off note: reran after recreating a case post-reset to prove that the fix is not only route logic. A second relaunch still lands on `Your Hall of Fame` with `case-card-001` visible, which matches the MMKV file now present in the app container under `Documents/mmkv/reality-check`.

Flow 64 sign-off note: reran on a fresh Release build after adding the verdict-to-Daily handoff. The unlocked verdict now opens Daily with a visible `From your latest read` source card tied to the just-closed case instead of dropping the user into a generic daily surface.

Flow 65 sign-off note: reran on a fresh Release build after moving the locked Daily CTA out from under the fixed footer. The locked verdict now reaches Daily cleanly, and the source card copy stays honest about the free-user path while remaining visually clean on iPhone Air.

Flow 66 sign-off note: reran on a fresh Release build after adding the post-reaction follow-up card. Reacting in Daily now leads into a visible, case-tied next-step card and a working Move On CTA instead of ending at a logged emoji state.

Flow 67 sign-off note: reran on a fresh Release build after moving the momentum card into `Today's reset` and fixing the day-progression logic. The partial-progress state now stays visible next to the tasks, the second task advances the card to `2 steps down`, and the fully completed day resolves into a `Day logged` state without prematurely jumping the plan forward.

Flow 68 sign-off note: reran on a fresh Release build after wiring `Daily` to the `Move On` completion store. Completing Day 1 in `Move On`, then switching to `Daily`, now shows the carry-forward `Reset landed` card with the closed-loop message instead of acting like no reset work happened.

Flow 69 sign-off note: reran on a fresh Release build after wiring the notification preview and nudge generator to the same `Move On` completion state. Completing Day 1 in `Move On`, then opening Settings, now shows the `Reset landed` chip, the closed-loop target copy, and a follow-through fit note instead of burying the reset state under generic notification language.

Flow 70 sign-off note: reran on a fresh Release build after proving the closed-loop path to cover the unfinished side as well. Stopping after two `Move On` tasks, then opening Settings, now shows the `Reset still open` chip, the `2 of 3 reset steps into Jake` target copy, and the matching follow-through sample instead of flattening an open reset into generic notification language.

Flow 71 sign-off note: reran on a fresh Release build after tightening the Settings preview hierarchy. Once `Move on mode` is selected and the user scrolls into the preview, the card now keeps the selection explicit via the in-card `Active pack` line instead of relying on the off-screen picker state.

## Release Gate

Current verdict: NO-GO.

Operator-facing summary:

- [final-launch-audit.md](/Users/marc-philliphansen/Projekte/Forks/likeme/docs/release/final-launch-audit.md)

Release notes:

- Internal app readiness is now materially different from external launch readiness: current release code passes the maintained iPhone Air flow inventory and the latest freeze gates, while actual ship remains blocked by missing live config only.
- The current release build on iPhone Air passes the full Maestro screen and flow inventory, including purchase failure, crisis support, permission recovery, share export, unlocked SAFE fallback, paywall proof continuity, and the subscription path where annual access unlocks the next case automatically.
- Later Add Case personalization is now launch-grade instead of onboarding-only: normal Check captures the same `dailyThought` and `desiredOutcome` headspace fields after Q6, leaves score calculation unchanged, and feeds the existing verdict, Daily, Move On, notification, and paywall continuity surfaces.
- All maintained normal Check Maestro flows were updated for those two required headspace steps, so future regressions will fail in the real user path instead of silently bypassing personalization.
- The verdict-to-Move-On handoff card now uses compact source-aware copy, preventing the first reset detail from clipping while preserving the case-specific next action.
- If live RevenueCat values are still missing, the paywall now fails safe instead of pretending purchases work: preview-only pricing, disabled CTA, explicit unavailable message, and no simulated unlock path in a normal release build.
- Settings now mirrors that same missing-config truth: manage and restore are visually disabled, and the billing card explains why purchases are unavailable in this build.
- OTA/TestFlight wiring is now present in the repo: `expo-updates` is installed, the app resolves `runtimeVersion` from app version, and `app.config.ts` injects the EAS update URL when `EXPO_PUBLIC_EAS_PROJECT_ID` is present.
- Release QA flags are now injected through `app.config.ts` and resolved at runtime instead of depending only on raw `process.env`, which makes E2E-only purchase simulation, loading delays, share capture, and analyzing holds behave consistently in native Release builds.
- The destructive reset path is now explicitly proven: deleting all cases clears the Wall and removes case-linked reset/re-entry state instead of leaving a half-reset app shell behind.
- Daily now has explicit QA proof that the same delete path also drops back to a generic no-wall state, so case-derived personalization does not ghost on after reset.
- Daily now also has explicit QA proof for both verdict handoff paths: unlocked and locked users can jump into a case-pinned Daily drop instead of landing on a contextless generic companion screen.
- Daily also now proves its post-reaction loop in Release: the user can react, get a case-aware follow-up card, and continue into Move On without breaking the current emotional thread.
- Move On now also has explicit Release proof for its in-progress and completed-day states: task feedback sits in the active reset section, and finishing the third task resolves into a visible `Day logged` reinforcement instead of a confusing plan jump.
- Daily now also proves carry-forward from that same reset work: after the user closes the active Move On loop, the next Daily surface acknowledges the completed reset instead of resetting back to generic detached copy.
- Notifications now also prove carry-forward from that same reset work: Settings preview can surface a just-closed reset as the active nudge target instead of flattening everything back into generic pack copy.
- Notifications now also prove the unfinished side of that same reset work: a partially completed Move On loop surfaces as `Reset still open` with concrete `2 of 3 steps` copy instead of waiting for another reopen before the app reacts.
- Settings notification UX now also keeps the chosen pack explicit at preview depth, so the user does not have to infer the active mode from an off-screen picker once they are reading the sample copy.
- Native persistence is now proven again instead of assumed: the app writes MMKV data back into the simulator container, relaunches into the correct returning-user state, and retains recreated case history across a further relaunch.
- The empty `Hall of Fame` state now uses the freestanding character asset instead of the old gray placeholder emoji, and Flow 01 was rerun to verify the updated visual on iPhone Air.
- `npm run testflight:check` now preflights the remaining release-infra blockers before any EAS build: launch config and OTA project id. Expo login is currently present on this machine.
- `npm run testflight:build` now uses that same readiness gate first, so this repo no longer starts an EAS production build while launch config is still incomplete.
- The repo-side local handoff path is now proven as well: both `launch:check` and `testflight:check` auto-load `.env.local`, and both pass when dummy live values are supplied there.
- The LLM-network failure path is covered in code by `src/services/verdictGeneration.test.ts`; the unlocked SAFE UI state is covered visually by Flow 20.
- `npm run launch:check` currently fails in the real workspace because `EXPO_PUBLIC_EAS_PROJECT_ID`, live RevenueCat values, and `EXPO_PUBLIC_VERDICT_PROXY_URL` have not been supplied yet.
- `npm run testflight:check` currently reports: `OK app.config.ts`, `OK eas.json`, `OK Expo login`, `MISSING launch config`, and `MISSING OTA project id`.
- `npm run launch:sweep` currently passes typecheck and tests, then stops at `launch:check`, which confirms the remaining NO-GO edge is live config rather than app behavior.
- Non-blocking build warning remains from `react-native-view-shot-RNViewShotPrivacyInfo` using an old simulator deployment target in Pods. This did not affect build/install/runtime behavior in Release.
