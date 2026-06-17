# Reality Check Post-Go-Live Wave 01

Date: 2026-06-16
Baseline: release-candidate build on iPhone Air after QA gate reached GO

## Objective

Run the app mentally and structurally through 15 likely user personas, identify where the current product still feels generic or emotionally shallow, and prioritize the next feature/content wave for stronger WOW, retention, and MRR.

## Product Read Before Wave 01

The core loop is already strong:

- the app gets to value quickly;
- the verdict reveal is screenshotable;
- the paywall gates depth, not the initial payoff;
- voice input adds emotional specificity;
- the unlocked verdict now has more analysis depth and feels closer to a "tiny pocket psychologist" without crossing into therapy language.

The remaining product ceiling is not basic UX. It is emotional specificity, repeatability, and reasons to come back after the first case.

## Persona Matrix

| # | Persona | What they want | Where current app lands | Gap |
|---|---|---|---|---|
| 1 | Ghosted overthinker, 22 | One clean answer to stop re-reading texts | Very strong first-session fit | Needs a stronger "now what" post-verdict path |
| 2 | Situationship optimist, 24 | Permission to keep hope alive, but safely | Verdict works, but can feel a bit too binary | Needs softer nuance tracks in mid buckets |
| 3 | Angry closure-seeker, 27 | Validation plus something sharp to share | Great score reveal and share energy | Needs more savage, variant-rich share captions |
| 4 | Private lurker, 21 | Quiet reassurance, no public posting | App is usable without sharing | Needs a private journaling / saved notes layer |
| 5 | Group-chat entertainer, 20 | Viral fodder for friends | Current teaser/clean share is good | Needs "send to group chat" framing and more meme variants |
| 6 | Serial checker, 23 | Run multiple cases fast | Wall supports this | Needs comparison mechanics across cases |
| 7 | High-anxiety texter, 25 | Strong interpretation of mixed signals | Improved analysis helps | Needs clearer emotional de-spiral language after result |
| 8 | Voice-first user, 19 | Speak instead of type | Voice input works | Needs stronger proof that the spoken moment shaped the result |
| 9 | Skeptic, 28 | "Convince me this is not random" | Receipts and flags help | Needs more visible grounding from selected flags |
|10 | Low-attention casual, 18 | Fast dopamine hit | Hook and reveal are good | Daily / Move On still not sticky enough |
|11 | Returning user with relapse, 26 | New daily micro-hit and emotional check-in | Daily is visually fun but shallow | Needs personalized daily content tied to her case history |
|12 | Breakup survivor, 29 | More nuanced emotional framing | Current app can feel crush-coded | Needs breakup / ex-specific copy and modules |
|13 | Paywall-resistant user, 24 | Enough value before paying | Free score is good | Needs clearer premium delta beyond "3 receipts" |
|14 | Power user who unlocks, 23 | Feels special after purchase | Better now with longer analysis | Still needs premium-only depth beyond one extra scroll section |
|15 | Notifications-sensitive user, 27 | Useful nudges, not spam | Soft ask is cleaner now | Needs more granular notification value props and modes |

## Cross-Persona Findings

### What already feels strong

- Hook to first value moment is fast.
- Score reveal is legible and emotionally satisfying.
- The app has a clear tone and a strong visual signature.
- Voice input and flags give the verdict a grounded shape.
- Premium unlock now feels more justified after the deeper analysis extension.

### Where the app still feels generic

1. Unlocked verdict depth still stops too early.
   The user now gets receipts, archetype, inner monologue, pattern read, and a reset line. Better, but still mostly one-screen depth.

2. Daily is no longer a stub, but it is still wave-one retention only.
   It now personalizes from case history and persists a real reaction streak, but it still stops short of deeper continuity.

3. Case history is now partially activated, but still not a full system.
   The unlocked verdict now synthesizes multiple premium cases into `case compare`, `his playbook`, and `why you stayed`, but the wall still does not expose a dedicated history intelligence view.

4. Premium value is still mostly content volume.
   The next MRR step should be content specificity and continuity, not just more cards.

5. Shareability is strong visually, but not yet varied enough socially.
   Users need multiple export tones: brutal, funny, classy, anonymous, group-chat.

## Wave-01 Priorities

### P0 Product Opportunity: Make unlocked verdict feel unmistakably premium

Build next:

- `Pattern read` section with richer relationship dynamic explanation
- `Reality reset` section with one concrete reframing move
- explicit grounding chips like `Built from: late-night texting, no date picked, hot-cold replies`

Status:

- First slice implemented in code this turn: longer analysis via `pattern_read` and `next_move`

### P1 Retention Opportunity: Turn Daily into a personalized return loop

Build next:

- daily verdict remix based on past case bucket + top flags
- rotating mini formats: `reality check`, `text audit`, `breadcrumb detector`, `your pattern today`
- streaks tied to insight, not just taps

Why:

- This is the clearest path from one-off novelty to repeat habit

### P1 MRR Opportunity: Premium should unlock continuity, not just one deeper card

Build next:

- `His playbook` card: recurring tactics inferred from selected flags
- `Why you stayed` card: user-side pattern framed safely and non-clinically
- `Case compare` view across unlocked cases

Why:

- Premium becomes "ongoing self-insight with receipts", not merely content reveal

Status:

- second slice implemented in code this turn inside the unlocked verdict flow

### P1 Viral Opportunity: Sharable outputs need tone variants

Build next:

- export modes: `Brutal`, `Funniest`, `Clean`, `Anonymous`
- one-tap group-chat caption variants
- optional blurred "receipts teaser" carousel

Why:

- Share growth improves without forcing every user into the same tone

Status:

- implemented in code this turn for the first export layer: four share variants with distinct captions, teaser/clean behavior, and anonymous identity masking

### P2 Trust Opportunity: Show more proof that the verdict is grounded

Build next:

- "Pulled from your case" chips
- a small "Used your replay moment" marker when voice/text influenced the narrative
- tap-to-expand receipt provenance

Why:

- Helps skeptics and increases perceived intelligence

## WOW / Bonding / MRR Review

### WOW

Current:

- strong visual identity
- strong stamp moment
- satisfying free reveal

Missing:

- a second surprise after unlock
- more "how did this app clock me so specifically?" moments

### User bonding

Current:

- first session creates emotional investment

Missing:

- relationship memory across cases
- personalized daily companionship
- a sense that the app understands *her pattern*, not just *this guy*

### MRR

Current:

- solid first-session conversion structure

Biggest upside:

- recurring premium insight layer
- daily personalized content
- richer unlocked outputs that justify subscription beyond one transaction

## Recommended Build Order

1. Deepen unlocked verdict further with visible grounding from user inputs
2. Personalize `Daily` from stored case history
3. Add premium `Case compare` / `Your pattern` views
4. Expand share variants
5. Add breakup/ex-specific content tracks

## Wave-01 Implementation Started

Completed in this pass:

- extended `NarrativeVerdict` with longer-form `pattern_read` and `next_move`
- passed onboarding context into narrative generation for richer fallback/server handling
- upgraded stored legacy cases so older narratives receive the new fields
- extended the unlocked verdict UI with two additional analysis cards
- added a personalized `Daily` digest engine with rotating formats derived from case history
- added a persisted daily reaction streak so Daily now behaves like a real return loop instead of demo state
- verified empty-wall and populated Daily states on iPhone Air with Maestro screenshots
- added premium continuity inside unlocked verdicts: `Case compare`, `His playbook`, and `Why you stayed`
- verified the two-unlocked-case premium continuity path on iPhone Air with Maestro screenshots
- added tone-controlled share exports: `Brutal`, `Funniest`, `Clean`, `Anonymous`
- verified teaser and unlocked share-sheet variants on iPhone Air with Maestro screenshots
- fixed a tab-bar remount bug by making active-tab presses inert, so repeated taps do not re-trigger the current screen lifecycle and replay animations
- added explicit group-chat caption payloads per share variant instead of only generic export copy
- added a persistent private-save path for non-sharing users inside locked and unlocked verdicts
- added private notes on saved cases, surfaced them back on the Wall, and fed them into Daily as a personalization signal
- fixed a real keyboard-coverage bug in the private-note sheet so the save CTA stays usable on iPhone Air with the keyboard open
- added breakup-aware fallback tracks for `almostEx` and `ghosted`, so these verdicts no longer read like generic crush cases
- fixed another keyboard-coverage bug in the `moment` composer for both onboarding and in-app case creation
- added explicit input provenance inside unlocked verdicts: context lens, user-state chips, and a quoted replay-moment proof block
- added `Wall intelligence / pattern radar`, so repeat users now see a multi-case read before opening any individual verdict
- reworked the wall radar card for scanability after visual QA feedback: short headline, highlighted repeat signal, visible evidence line, shorter supporting copy
- verified the wall radar path on iPhone Air with a dedicated Maestro flow and refreshed screenshot
- replaced the `Move On` preview stub with a persisted 7-day reset loop tied to real case history
- split `Move On` into a true empty state and a real populated plan state, so users cannot fake-complete `log one case` before the wall has any data
- verified both `Move On` states on iPhone Air: empty-state tab path and populated task-toggle path
- added a lightweight re-entry memory layer, so repeated Verdict opens now become a real product signal instead of invisible behavior
- surfaced that re-entry signal across Wall, Daily, and Move On with a shared `re-entry watch` read tied to the same case history
- verified the relapse-aware returning-user path on iPhone Air with a dedicated Maestro flow and fresh screenshots for Wall, Daily, and Move On
- turned notification settings from raw toggles into three clear packs: `Balanced`, `Only useful`, and `Move on mode`
- added a preview engine that shows actual notification value, sample copy, and active channels before opt-in
- introduced `re-entry nudges` as an explicit notification channel tied to repeated case reopening behavior
- verified notification modes and re-entry preview states on iPhone Air with dedicated Maestro coverage and refreshed screenshots
- deepened `situationship` fallback writing so mid-bucket and mutual-but-unsolid cases no longer read like generic crush leftovers
- separated the mixed-signal and low-bucket situationship lanes with different `what he was thinking`, `why this got in your head`, and `reality reset` language
- verified both situationship nuance states on iPhone Air with dedicated Maestro screenshots for a 72-score mixed case and a 61-score mutual-but-unsolid case
- expanded the verdict proxy payload with richer user-state: daily thought, desired outcome, signal summary, and tone hints
- made the fallback verdict visibly react harder to headspace inputs, so `Every single day` and `A tiny bit of hope` now meaningfully change the read instead of only sitting as chips
- verified the onboarding headspace path on iPhone Air with a dedicated unlocked-verdict screenshot
- added a section-level merge gate so weak proxy verdict sections cannot flatten the richer local headspace read
- kept the server path primary, but now selectively swap in grounded local `receipts`, `why this got in your head`, `reality reset`, or `what he was thinking` when the proxy response is too generic
- re-verified the unlocked onboarding headspace flow on iPhone Air after the parity guardrail, with no new layout regressions
- carried the stronger headspace read into Daily, so the card now surfaces a scanable `what keeps reopening` block instead of burying the emotional hook in body copy
- reshaped `Move On` around a visible `loop to break` and `why this reset today` layer, so the tab now sounds like the same app as the verdict instead of a separate generic reset tool
- upgraded re-entry copy across Daily and Move On to react to `hope`, `closure`, `brutal truth`, `drama`, and `daily brain space` instead of one flat reopen message
- verified the new Daily/Move On headspace path on iPhone Air with a dedicated Maestro flow, plus a re-entry regression rerun after the layout changes
- upgraded notification previews from generic samples to wall-aware copy, so Settings now shows what the app would actually say to someone still hoping for a softer answer or reopening the same case
- added a `current nudge target` block in Settings, so notification packs explain who or what they are reacting to right now instead of only naming channels
- split notification pack fit-notes by emotional job: `Balanced` for one daily reality interrupt, `Only useful` for receipts-only alerts, and `Move on mode` for reducing thumb-led checking
- verified the new notification headspace path on iPhone Air with a dedicated Maestro flow, plus a regression rerun for the re-entry settings path and mode switching
- gave each notification mode a concrete timing personality, so `Balanced`, `Only useful`, and `Move on mode` now promise different send windows, weekly load, and interruption rules instead of sharing one vague quiet-hours claim
- added a dedicated `Timing promise` block in Settings with scanable rhythm, quiet-hours, and volume-cap panels, so users can tell how noisy each pack will realistically be before they enable it
- aligned the pure notification policy code with the visible Settings promise, so mode-specific quiet hours now live in one shared timing layer instead of drifting between UX copy and runtime logic
- verified the timing layer on iPhone Air with dedicated Maestro coverage for `Balanced` and `Move on mode`, including the lower quiet-hours/volume sections after scroll
- rebuilt the locked verdict and paywall around case-specific reasons to unlock, so premium no longer sells generic “full access” language after the app itself has already read the user more personally
- fixed the live annual-plan formatting path so real RevenueCat annual products still render as `weekly equivalent big + yearly small`, matching the intended paywall design instead of collapsing to one blunt annual price string
- added plan-specific monetization notes, giving weekly / annual / one-time options clearer jobs instead of presenting them as mostly interchangeable prices
- verified the personalized locked verdict pitch and the new paywall top/pricing states on iPhone Air with dedicated Maestro screenshots
- added repeat-loop paywall strategy logic, so returning users with prior unlocks, multiple cases, heavy daily brain-space, or frequent reopens now land on an annual-default recommendation instead of the same weekly-first paywall as one-off users
- added a visible `Best fit for your wall` recommendation block plus plan-badge overrides, making the monetization logic legible instead of silently preselecting annual
- kept one-off users on the weekly-default path, so the paywall does not overreach on lighter first-case traffic
- tightened the paywall layout after QA caught a real conversion regression where the CTA fell too low once the new strategy copy was added
- verified the annual-default repeat-loop paywall on iPhone Air with a dedicated two-case Maestro flow and a fresh pricing screenshot
- pulled the same annual-fit recommendation forward into the locked verdict, so repeat-loop users now understand the premium fit before opening the paywall instead of only after the sheet appears
- kept the locked verdict footer and pre-paywall messaging in parity with the paywall strategy, so annual-preselected users now see the same repeat-pattern framing through the whole unlock path
- verified the pre-paywall annual-fit state on iPhone Air with a dedicated locked-verdict Maestro flow and fresh screenshot coverage
- fixed a real premium-contract bug where weekly and annual purchases only unlocked the current case instead of the broader subscription scope they were being sold as
- added a persisted subscription-access layer, applied subscription unlocks across all existing cases, and made newly analyzed cases auto-unlock while weekly or annual access is active
- kept one-time verdict purchases case-scoped, so the one-off product still behaves differently from recurring full-access plans
- fixed a paywall navigation regression caused by the new subscription bypass, where annual purchase could double-pop the stack back to the Wall instead of returning to the unlocked verdict
- verified the subscription contract on iPhone Air with a dedicated Maestro flow: buy annual on case one, create case two, land directly in an unlocked verdict with no second paywall stop
- added explicit full-access surfacing on the Wall, so subscribers now see that new cases are already included instead of having to infer it from the absence of a paywall
- upgraded premium continuity from simple compare cards into a sharper multi-case read: `What repeats`, `What changed`, and `Who keeps hooking you`
- verified the stronger multi-case premium continuity path on iPhone Air with refreshed Maestro screenshots for the compare and pattern blocks
- hardened the premium Maestro flows against the real app states they now encounter: the in-app notification soft ask, case-by-case unlock versus full-access unlock, and text-anchor scrolling where view ids are not stably exposed
- upgraded the add-case tile to explain when another file is already included in weekly or annual access, making the next paid action feel frictionless instead of ambiguous
- rebuilt the Settings plan card from a blunt status line into a clear active-access summary with included-value chips
- verified the subscriber surfaces on iPhone Air with dedicated Wall and Settings screenshots after an annual purchase path
- extended the same full-access framing into Daily and Move On, so subscriber retention tabs now talk like an already-paid product instead of sounding like they still need to earn another unlock
- upgraded the notification preview for subscribers, so `Balanced` / `Only useful` / `Move on mode` now explicitly frame their job as interruption and momentum while full access is already live
- verified Daily, Move On, and the subscriber-specific notification preview on iPhone Air with dedicated Maestro screenshots after the annual-purchase path
- surfaced premium continuity directly on the Wall and Daily instead of hiding it inside reopened premium verdicts, so repeat users now see the memory loop before deciding where to tap
- moved the Wall continuity card above the subscription status card after visual QA, because the multi-case pattern read is the stronger product signal on the browsing screen
- hardened the continuity Maestro flow around stable card ids instead of CTA-text lookup, after the Daily card was visually present but the text selector still failed
- verified the new Wall and Daily continuity teaser surfaces plus tap-through back into the latest unlocked case on iPhone Air with dedicated Maestro screenshots
- added Wall `Loop shortcuts` built from real repeated pattern signals instead of generic sort chips, so users can jump straight into the exact mess type they keep filing
- made the first shortcut layer evidence-driven: repeated flags, repeated contexts, and hard-case clusters are now derived from existing case history without adding a new data model
- verified the filter loop on iPhone Air with a dedicated three-case Maestro run: create cases, apply `Story > text`, confirm the wall drops to 2 matching files, then clear back to `All`
- added a compact premium timeline to the Wall, so repeat users now see the recent sequence of scores and the repeated signal instead of only a static pattern label
- fixed a real wall-layout issue while doing it: filter shortcuts and the premium timeline now live inside the scrollable FlashList header, not in a fixed area that can visually run into the bottom navigation
- verified the timeline surface on iPhone Air with a dedicated two-case Maestro flow and refreshed screenshot coverage

Files:

- [src/services/verdictGeneration.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/verdictGeneration.ts)
- [src/store/cases.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/store/cases.ts)
- [src/screens/AnalyzingScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/AnalyzingScreen.tsx)
- [src/store/reentry.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/store/reentry.ts)
- [src/services/reentryHooks.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/reentryHooks.ts)
- [.maestro/30_relapse_reentry_hooks.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/30_relapse_reentry_hooks.yaml)
- [src/store/preferences.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/store/preferences.ts)
- [src/store/preferences.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/store/preferences.test.ts)
- [src/services/notificationPreview.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.ts)
- [src/services/notificationPreview.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.test.ts)
- [src/screens/SettingsScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/SettingsScreen.tsx)
- [src/services/paywallStrategy.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallStrategy.ts)
- [src/services/paywallStrategy.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallStrategy.test.ts)
- [src/services/paywallMessaging.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallMessaging.ts)
- [src/screens/PaywallScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/PaywallScreen.tsx)
- [.maestro/38_paywall_annual_repeatloop.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/38_paywall_annual_repeatloop.yaml)
- [src/screens/VerdictScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/VerdictScreen.tsx)
- [.maestro/39_locked_verdict_annual_fit.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/39_locked_verdict_annual_fit.yaml)
- [src/store/premium.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/store/premium.ts)
- [src/store/cases.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/store/cases.ts)
- [src/services/revenueCat.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/revenueCat.ts)
- [src/services/revenueCatHelpers.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/revenueCatHelpers.ts)
- [src/screens/AnalyzingScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/AnalyzingScreen.tsx)
- [src/screens/SettingsScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/SettingsScreen.tsx)
- [.maestro/40_subscription_unlocks_future_cases.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/40_subscription_unlocks_future_cases.yaml)
- [src/services/subscriptionMessaging.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/subscriptionMessaging.ts)
- [src/services/subscriptionMessaging.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/subscriptionMessaging.test.ts)
- [src/components/Cards.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/components/Cards.tsx)
- [src/screens/WallScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/WallScreen.tsx)
- [.maestro/41_subscription_surfaces_visual.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/41_subscription_surfaces_visual.yaml)
- [src/screens/DailyScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/DailyScreen.tsx)
- [src/screens/MoveOnScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/MoveOnScreen.tsx)
- [src/services/notificationPreview.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.ts)
- [src/services/notificationPreview.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.test.ts)
- [.maestro/42_subscription_retention_surfaces.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/42_subscription_retention_surfaces.yaml)
- [.maestro/43_subscription_notification_preview.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/43_subscription_notification_preview.yaml)
- [.maestro/04_notification_settings.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/04_notification_settings.yaml)
- [.maestro/31_notification_modes_reentry.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/31_notification_modes_reentry.yaml)
- [src/services/verdictGeneration.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/verdictGeneration.ts)
- [src/services/verdictGeneration.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/verdictGeneration.test.ts)
- [.maestro/32_situationship_midbucket_visuals.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/32_situationship_midbucket_visuals.yaml)
- [verdict-generation.md](/Users/marc-philliphansen/Projekte/Forks/likeme/verdict-generation.md)
- [.maestro/33_onboarding_headspace_personalization.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/33_onboarding_headspace_personalization.yaml)
- [src/services/dailyDigest.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/dailyDigest.ts)
- [src/services/dailyDigest.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/dailyDigest.test.ts)
- [src/services/moveOnPlan.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/moveOnPlan.ts)
- [src/services/moveOnPlan.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/moveOnPlan.test.ts)
- [src/services/reentryHooks.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/reentryHooks.ts)
- [src/services/reentryHooks.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/reentryHooks.test.ts)
- [src/screens/DailyScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/DailyScreen.tsx)
- [src/screens/MoveOnScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/MoveOnScreen.tsx)
- [.maestro/34_daily_moveon_headspace_loop.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/34_daily_moveon_headspace_loop.yaml)
- [src/services/notificationPreview.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.ts)
- [src/services/notificationPreview.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.test.ts)
- [src/screens/SettingsScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/SettingsScreen.tsx)
- [.maestro/35_notification_headspace_preview.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/35_notification_headspace_preview.yaml)
- [src/services/notificationTiming.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationTiming.ts)
- [src/services/notificationTiming.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationTiming.test.ts)
- [src/services/notifications.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notifications.ts)
- [src/screens/SettingsScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/SettingsScreen.tsx)
- [.maestro/36_notification_timing_visual.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/36_notification_timing_visual.yaml)
- [src/services/paywallMessaging.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallMessaging.ts)
- [src/services/paywallMessaging.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallMessaging.test.ts)
- [src/services/paywallPricing.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallPricing.ts)
- [src/services/paywallPricing.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/paywallPricing.test.ts)
- [src/services/revenueCat.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/revenueCat.ts)
- [src/screens/PaywallScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/PaywallScreen.tsx)
- [src/screens/VerdictScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/VerdictScreen.tsx)
- [.maestro/37_paywall_personalized_visual.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/37_paywall_personalized_visual.yaml)
- [src/services/premiumContinuity.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/premiumContinuity.ts)
- [src/services/premiumContinuity.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/premiumContinuity.test.ts)
- [src/screens/WallScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/WallScreen.tsx)
- [src/screens/DailyScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/DailyScreen.tsx)
- [.maestro/45_continuity_surfaces.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/45_continuity_surfaces.yaml)
- [src/services/wallFilters.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/wallFilters.ts)
- [src/services/wallFilters.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/wallFilters.test.ts)
- [src/screens/WallScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/WallScreen.tsx)
- [.maestro/46_wall_pattern_filters.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/46_wall_pattern_filters.yaml)
- [src/services/wallTimeline.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/wallTimeline.ts)
- [src/services/wallTimeline.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/wallTimeline.test.ts)
- [src/screens/WallScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/WallScreen.tsx)
- [.maestro/47_wall_timeline_visual.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/47_wall_timeline_visual.yaml)
- [src/services/dailyDigest.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/dailyDigest.ts)
- [src/services/dailyDigest.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/dailyDigest.test.ts)
- [src/services/moveOnPlan.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/moveOnPlan.ts)
- [src/services/moveOnPlan.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/moveOnPlan.test.ts)
- [src/screens/DailyScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/DailyScreen.tsx)
- [src/screens/MoveOnScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/MoveOnScreen.tsx)
- [.maestro/48_timeline_retention_surfaces.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/48_timeline_retention_surfaces.yaml)
- [src/services/notificationPreview.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.ts)
- [src/services/notificationPreview.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notificationPreview.test.ts)
- [src/screens/SettingsScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/SettingsScreen.tsx)
- [.maestro/49_timeline_notification_preview.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/49_timeline_notification_preview.yaml)
- [src/services/notifications.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notifications.ts)
- [src/services/notifications.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/notifications.test.ts)
- [src/components/Controls.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/components/Controls.tsx)
- [src/screens/CheckScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/CheckScreen.tsx)
- [src/screens/OnboardingScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/OnboardingScreen.tsx)
- [.maestro/50_check_intro_visual.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/50_check_intro_visual.yaml)
- [.maestro/51_case_entry_keyboard_visuals.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/51_case_entry_keyboard_visuals.yaml)
- [src/services/verdictProof.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/verdictProof.ts)
- [src/services/verdictProof.test.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/src/services/verdictProof.test.ts)
- [src/screens/VerdictScreen.tsx](/Users/marc-philliphansen/Projekte/Forks/likeme/src/screens/VerdictScreen.tsx)
- [.maestro/52_verdict_skeptic_proof.yaml](/Users/marc-philliphansen/Projekte/Forks/likeme/.maestro/52_verdict_skeptic_proof.yaml)

## Fresh slice

`Daily reaction follow-up`

What shipped:

- reacting in `Daily` no longer ends at a logged emoji; it now resolves into one concrete next-step card tied to the same case and the same reset engine
- the follow-up carries the first real `Move On` task, the current day in the 7-day loop, and a direct CTA into `Move On`, so the tap becomes a behavioral handoff instead of a dead-end streak gesture
- this keeps the low-attention `Daily` habit loop emotionally hot for a few seconds longer without bloating the screen or inventing a second retention system
- this was verified on iPhone Air through a dedicated end-to-end flow:
  - [flow66-daily-followup.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow66-daily-followup.png)
  - [flow66-daily-followup-moveon.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow66-daily-followup-moveon.png)

`Daily source context`

What shipped:

- `Daily` can now pin itself to the exact case the user came from instead of only inferring from the latest wall state
- verdict handoffs now branch cleanly into `Open Daily` for both unlocked and locked users, and the resulting Daily screen explains why that specific case is the emotional anchor for the drop
- unlocked and locked copy are intentionally different, so the free path stays honest instead of pretending it has the same depth framing as the paid path
- this was verified on iPhone Air with dedicated end-to-end Maestro paths and fresh screenshots that now include the source card itself:
  - [flow64-daily-from-verdict.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow64-daily-from-verdict.png)
  - [flow65-daily-from-locked-verdict.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow65-daily-from-locked-verdict.png)

`Empty wall companion asset`

What shipped:

- the empty `Hall of Fame` state no longer uses the old gray person emoji; it now renders the new freestanding `cool guy` character asset
- the asset was background-removed and cropped tightly before wiring it in, so it reads as an intentional product illustration instead of a tiny full-canvas image dropped into the view
- the empty-state avatar sizing was also nudged up so the figure lands with enough presence on iPhone Air
- this was re-verified on iPhone Air through the onboarding-to-empty-wall path:
  - [flow01-empty-wall.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow01-empty-wall.png)

`Move On source context`

What shipped:

- `Move On` can now pin itself to the exact case the user came from instead of only inferring from the latest generic wall state
- when the handoff comes from a verdict, the top of `Move On` explicitly says that this reset starts with that case, which makes the transition feel read rather than routed
- unlocked and locked handoffs use different source copy, so free users do not get premium-shaped phrasing and premium users do not fall back into generic advice
- this was re-verified on iPhone Air in both paths:
  - [flow62-moveon-from-verdict.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow62-moveon-from-verdict.png)
  - [flow63-moveon-from-locked-verdict.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow63-moveon-from-locked-verdict.png)

`Locked verdict free handoff`

What shipped:

- locked verdicts now offer a real free next step instead of forcing the user into a binary `pay or leave` dead end
- the new `Free next step` card reuses the same Move On engine, but stays clearly secondary to the unlock CTA so monetization is not diluted
- this gives non-buyers a useful retention path on the same emotional beat where they would otherwise just bounce
- this was verified on iPhone Air with a dedicated locked path:
  - [flow63-locked-verdict-moveon-card.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow63-locked-verdict-moveon-card.png)
  - [flow63-moveon-from-locked-verdict.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow63-moveon-from-locked-verdict.png)

`Verdict to Move On handoff`

What shipped:

- unlocked verdicts now hand off into a concrete post-read action instead of ending on analysis, share, and add-case only
- the new `What now` block pulls the first real reset action from the existing Move On engine, shows the current day in the 7-day loop, and carries one evidence line from the case into the CTA
- the tap goes straight into `Move On`, so the user gets an immediate behavioral next step while the read is still emotionally hot
- this was verified on iPhone Air with a dedicated end-to-end Maestro path:
  - [flow62-verdict-moveon-card.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow62-verdict-moveon-card.png)
  - [flow62-moveon-from-verdict.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow62-moveon-from-verdict.png)

`Pattern file destination`

What shipped:

- premium continuity is no longer only a teaser that bounces back into the latest verdict; Wall and Daily now open a dedicated `Pattern File` screen
- that screen turns the existing multi-case intelligence into its own premium destination with `What repeats`, `Pattern progression`, `What changed`, `His playbook`, `Who keeps hooking you`, and `Why you stayed`
- during visual QA, two real clipping bugs surfaced on iPhone Air: the hero stat boxes in `Pattern File` and the top metric band on `Move On`
- both were hardened with less aggressive display sizing and more vertical breathing room, then re-verified instead of being hand-waved as font quirks
- this was verified on iPhone Air with refreshed continuity and Move On screenshots:
  - [flow45-wall-premium-continuity.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow45-wall-premium-continuity.png)
  - [flow45-daily-premium-continuity.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow45-daily-premium-continuity.png)
  - [flow45-pattern-file.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow45-pattern-file.png)
  - [flow45-pattern-file-progression.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow45-pattern-file-progression.png)
  - [flow29-moveon-populated.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow29-moveon-populated.png)

`Skeptic proof layer`

What shipped:

- unlocked verdicts now expose a compact `What pushed the score` block instead of relying on vibe and prose alone
- that block surfaces the three strongest answer signals directly from the real quiz answers, so the read feels grounded rather than magic-box
- replay evidence still sits directly below it, which now makes the trust chain legible: selected pattern, strongest answers, then the replay moment
- this was verified on iPhone Air with a fresh unlocked verdict screenshot: [flow52-verdict-skeptic-proof.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow52-verdict-skeptic-proof.png)

`Locked proof teaser`

What shipped:

- locked verdicts now show a compact grounded teaser before the paywall CTA instead of jumping straight from verdict to monetization
- the teaser reuses the same trust chain in a smaller form: strongest answer rows, top selected signal, and a replay marker when a replay moment exists
- this makes the paywall ask feel earned because the app proves it actually read the case before asking for unlock money
- this was verified on iPhone Air with a fresh locked verdict screenshot: [flow53-locked-proof-teaser.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow53-locked-proof-teaser.png)

`Paywall proof continuity`

What shipped:

- the paywall now continues the same grounded read instead of resetting into generic pricing language
- the new carry-over card keeps the proof chain alive across the sheet boundary: strongest answer rows, top selected signal, and replay marker
- this makes the monetization step feel like the next beat of the same case rather than a detached store page
- this was verified on iPhone Air with a fresh paywall screenshot: [flow54-paywall-proof-continuity.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow54-paywall-proof-continuity.png)

`Launch freeze sweep`

What shipped:

- fixed a real launch blocker in RevenueCat config resolution: env values now override placeholder values from `app.json`
- added `npm run launch:check`, which fails hard until real RevenueCat live values and `EXPO_PUBLIC_VERDICT_PROXY_URL` are present
- reran the annual-subscription path after the taller paywall and full-access wall surface changes; the Maestro flow was updated to match the current UX instead of assuming the old shorter layout
- the subscription path is freshly re-verified on iPhone Air via [flow40-subscription-second-case-unlocked.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow40-subscription-second-case-unlocked.png)

`Live-config handoff`

What shipped:

- added a final human-proof release handoff in [live-config-handoff.md](/Users/marc-philliphansen/Projekte/Forks/likeme/docs/release/live-config-handoff.md)
- added a tracked [.env.example](/Users/marc-philliphansen/Projekte/Forks/likeme/.env.example) and ignored real `.env` files in [.gitignore](/Users/marc-philliphansen/Projekte/Forks/likeme/.gitignore)
- `npm run launch:check` now points directly to the handoff doc when live values are still missing

`Move On momentum`

What shipped:

- the progress-feedback card is no longer buried high in the hero while the user is checking tasks below; it now sits directly inside `Today's reset`, next to the action it is commenting on
- finishing the current day no longer advances the whole `Move On` plan too early; the screen now keeps today's completion visible and only previews tomorrow inside the completion card
- the in-between state is now explicit and reinforcing: after one or two checked tasks the user gets a live `Keep it moving` card with the remaining count and the next interruption to close
- this was verified on iPhone Air with a dedicated end-to-end Maestro flow and fresh screenshots:
  - [flow67-moveon-momentum.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow67-moveon-momentum.png)
  - [flow67-moveon-day-logged.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow67-moveon-day-logged.png)

`Move On to Daily carry-forward`

What shipped:

- `Daily` now reads the current `Move On` completion state instead of acting like reset work never happened
- when the user already closed today's reset loop, the next `Daily` drop surfaces that explicitly with a `Reset landed` card instead of falling back to generic companion copy
- when the reset loop is still open or yesterday stalled, `Daily` can now carry that unfinished state forward as a concrete interruption signal
- this makes the retention loop more honest: `Verdict -> Move On -> Daily` now remembers whether the user actually did the work
- this was verified on iPhone Air with a dedicated end-to-end Maestro flow and fresh screenshot:
  - [flow68-daily-moveon-carryforward.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow68-daily-moveon-carryforward.png)

`Move On follow-through into notifications`

What shipped:

- `Settings` notification preview now reads the same `Move On` completion state as `Daily`, so a closed reset loop surfaces as a first-class follow-through target instead of getting buried under generic mode copy
- live notification generation now distinguishes `reset landed` from `reset still open`, which means daily and streak nudges can follow through on a started reset instead of waiting until the user reopens the loop again
- the preview chips now make that state visible with `Reset landed` or `Reset still open`, so the user can see why the pack would interrupt them right now
- this was verified on iPhone Air with dedicated end-to-end Maestro coverage for both follow-through states:
  - [flow69-settings-notification-reset-landed.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow69-settings-notification-reset-landed.png)
  - [flow70-settings-notification-reset-open.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow70-settings-notification-reset-open.png)

`Notification mode clarity near preview`

What shipped:

- the active notification pack now stays explicit inside the preview card itself, so the user no longer has to remember which mode was selected after scrolling away from the picker
- the preview now shows both selected-state pills and a plain `Active pack: Move on mode` line, which removes the earlier ambiguity where the visible mode card and preview header could drift apart in the viewport
- this was verified on iPhone Air with a dedicated Settings flow and fresh screenshot:
  - [flow71-notification-mode-clarity.png](/Users/marc-philliphansen/Projekte/Forks/likeme/flow71-notification-mode-clarity.png)

## Next slice

`Launch-freeze blocker audit`

Why next:

- the remaining work is no longer broad product building; it is now mostly hard proof and blocker separation between internal app readiness and external launch infra
- the next highest-leverage move is to tighten the blocker list, rerun the current freeze gates, and make the last true `GO / NO-GO` edges explicit
- that gives the shortest path from “strong app” to “shippable app”

## Next Build Slice

The highest-leverage next slice is:

`Launch-freeze blocker audit`

Scope:

- rerun the current release checks and classify what is still truly blocking
- separate internal app blockers from external config/account blockers in the audit
- avoid reopening product-surface work unless a real P0/P1 emerges from the freeze pass
