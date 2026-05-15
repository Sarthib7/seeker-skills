---
name: seeker-app-builder
description: Router for building a Solana Mobile (Seeker) dApp end-to-end. Triggers - "build a Seeker app", "ship to dApp Store", "start Solana Mobile RN project". Delegates to sub-skills.
---

# Seeker App Builder

## Route

| State | Sub-skill |
|-------|-----------|
| No project | `seeker-app-scaffold` |
| No wallet | `@solana-mobile/mobile-wallet-adapter` (from `solana-mobile/solana-mobile-dev-skill`) |
| No on-chain action | `solana-pay-mobile` |
| Untuned UX | `seeker-ux` |
| Ready to ship | `dapp-store-publishing` |
| Building a wallet (not dApp) | `seed-vault` |

## Order

scaffold → MWA → tx action → UX → publish.

## Companion (external)

MWA, `.skr` resolution, Genesis Token: `solana-mobile/solana-mobile-dev-skill`.

## Constraints

- No private keys in app code. MWA signs.
- APK only. No AAB.
- minSdkVersion 26.
- Different signing key from Google Play if dual-ship.

## Refs

- docs.solanamobile.com
- docs.solanamobile.com/dapp-store/intro
- github.com/solana-mobile/solana-mobile-dev-skill
