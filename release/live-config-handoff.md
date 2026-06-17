# Live Config Handoff

This is the final non-code setup for a real launch.

Until this is done, the app should be treated as `NO-GO` even if the UI and flows look correct.

## What you need

You need six real required values, plus one entitlement override only if your RevenueCat project does not use the default:

1. `EXPO_PUBLIC_EAS_PROJECT_ID`
2. `EXPO_PUBLIC_REVENUECAT_IOS_API_KEY`
3. `EXPO_PUBLIC_REVENUECAT_PRODUCT_WEEK`
4. `EXPO_PUBLIC_REVENUECAT_PRODUCT_YEAR`
5. `EXPO_PUBLIC_REVENUECAT_PRODUCT_ONCE`
6. `EXPO_PUBLIC_VERDICT_PROXY_URL`

Optional only when needed:

7. `EXPO_PUBLIC_REVENUECAT_ENTITLEMENT_ID`

The app already contains placeholder values in [app.json](/Users/marc-philliphansen/Projekte/Forks/likeme/app.json), but code now correctly prefers real env values over those placeholders. OTA/TestFlight config is now wired through [app.config.ts](/Users/marc-philliphansen/Projekte/Forks/likeme/app.config.ts) and [eas.json](/Users/marc-philliphansen/Projekte/Forks/likeme/eas.json).

## Part 0: Expo / EAS project id for OTA

### 1. Open Expo

1. Go to `https://expo.dev`
2. Open the correct Expo project for this app
3. Open the project settings page
4. Copy the project id

It becomes:

```env
EXPO_PUBLIC_EAS_PROJECT_ID=...
```

This value is not secret. It is what lets the TestFlight build know which EAS Update project it should pull OTA updates from.

## Part 1: RevenueCat

### 1. Open RevenueCat

1. Go to `https://app.revenuecat.com`
2. Open the correct project for this app
3. Open the iOS app entry

### 2. Copy the iOS API key

1. In RevenueCat, open the app settings for iOS
2. Find the public iOS SDK key
3. Copy it
4. This becomes:

```env
EXPO_PUBLIC_REVENUECAT_IOS_API_KEY=...
```

### 3. Confirm the entitlement id

1. Open `Entitlements`
2. Find the entitlement that should unlock subscriptions
3. In this app, the built-in default is:

```env
EXPO_PUBLIC_REVENUECAT_ENTITLEMENT_ID=full_access
```

4. If your actual entitlement id is different, set the real one. If it is still `full_access`, no extra env var is required.

### 4. Copy the product ids

1. Open `Products`
2. Find the weekly subscription product
3. Copy its exact product identifier
4. Find the yearly subscription product
5. Copy its exact product identifier
6. Find the one-time unlock product
7. Copy its exact product identifier

They become:

```env
EXPO_PUBLIC_REVENUECAT_PRODUCT_WEEK=...
EXPO_PUBLIC_REVENUECAT_PRODUCT_YEAR=...
EXPO_PUBLIC_REVENUECAT_PRODUCT_ONCE=...
```

## Part 2: Verdict proxy

The app must never ship a raw Anthropic key in the client. The client only talks to a proxy URL.

### 1. Find the real proxy endpoint

You need the final live endpoint that accepts the verdict POST request.

Expected shape:

```env
EXPO_PUBLIC_VERDICT_PROXY_URL=https://your-domain.com/verdict
```

### 2. Sanity check the proxy

The proxy must:

- accept POST requests
- return the expected verdict JSON shape
- handle failures safely
- keep the real model key server-side only

## Part 3: Put the values into the app locally

### Option A: easiest local setup

1. In the project root, duplicate `.env.example`
2. Rename the copy to `.env.local`
3. Paste the required live values into `.env.local`

Example:

```env
EXPO_PUBLIC_REVENUECAT_IOS_API_KEY=appl_xxx
EXPO_PUBLIC_EAS_PROJECT_ID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
EXPO_PUBLIC_REVENUECAT_ENTITLEMENT_ID=full_access
EXPO_PUBLIC_REVENUECAT_PRODUCT_WEEK=realitycheck_weekly
EXPO_PUBLIC_REVENUECAT_PRODUCT_YEAR=realitycheck_yearly
EXPO_PUBLIC_REVENUECAT_PRODUCT_ONCE=realitycheck_once
EXPO_PUBLIC_VERDICT_PROXY_URL=https://api.yourdomain.com/verdict
```

`.env.local` is ignored by git.

The release scripts now load `.env.local` automatically. You do not need to re-export the same values manually just to run:

- `npm run launch:check`
- `npm run testflight:check`
- `npm run testflight:build`

Shell-exported values still win if you set them explicitly.

### Option B: shell env

You can also export the values in the terminal before building:

```bash
export EXPO_PUBLIC_REVENUECAT_IOS_API_KEY=...
export EXPO_PUBLIC_EAS_PROJECT_ID=...
export EXPO_PUBLIC_REVENUECAT_ENTITLEMENT_ID=...
export EXPO_PUBLIC_REVENUECAT_PRODUCT_WEEK=...
export EXPO_PUBLIC_REVENUECAT_PRODUCT_YEAR=...
export EXPO_PUBLIC_REVENUECAT_PRODUCT_ONCE=...
export EXPO_PUBLIC_VERDICT_PROXY_URL=...
```

## Part 4: Validate before launch

Run this in the project root:

```bash
npm run launch:check
```

Expected result:

```text
OK  RevenueCat iOS API key
OK  Expo EAS project id for OTA
OK  RevenueCat weekly product
OK  RevenueCat yearly product
OK  RevenueCat one-time product
OK  Verdict proxy URL

Launch config check passed.
```

If any line says `MISSING`, the app is still `NO-GO`.

For the broader release infra, also run:

```bash
npm run testflight:check
```

## Part 5: Final launch sweep

After the real values are present:

### Option A: one command

Run:

```bash
npm run launch:sweep
```

That command runs:

- `npm run typecheck`
- `npm run test`
- `npm run launch:check`
- release build on `iPhone Air`
- Maestro flow `40_subscription_unlocks_future_cases`
- Maestro flow `54_paywall_proof_continuity`

### Option B: step by step

1. Run:

```bash
npm run typecheck
npm run test
npm run launch:check
```

2. Build the release app on iPhone Air:

```bash
npx expo run:ios --configuration Release --device 3B47AA0C-3CBC-425C-B2D5-3FCB92249D6C --no-bundler
```

3. Run the monetization sweep:

```bash
maestro test --driver-host-port 7005 --udid 3B47AA0C-3CBC-425C-B2D5-3FCB92249D6C .maestro/40_subscription_unlocks_future_cases.yaml
```

4. If that passes and `launch:check` passes, the remaining blocker is gone

## Fast summary

If you want the shortest possible version later:

1. Fill `.env.local`
2. Run `npm run launch:sweep`
3. If it finishes without errors, config is no longer the blocker

## Part 6: Build for TestFlight with OTA enabled

After the required live values above are present and you are logged into Expo:

```bash
npm run testflight:check
npm run testflight:build
```

What this now does in this repo:

- loads `.env.local` automatically before checking launch/TestFlight readiness
- runs `npm run testflight:check` first and stops immediately if launch config or OTA wiring is still incomplete
- uses [eas.json](/Users/marc-philliphansen/Projekte/Forks/likeme/eas.json)
- builds the iOS app with the `production` channel
- includes `expo-updates`
- uses `runtimeVersion` policy `appVersion`
- wires the OTA update URL from `EXPO_PUBLIC_EAS_PROJECT_ID`

## Part 7: Publish an OTA update later

Preview / QA OTA:

```bash
npm run ota:publish:preview -- --message "Your message"
```

Production OTA:

```bash
npm run ota:publish:production -- --message "Your message"
```
