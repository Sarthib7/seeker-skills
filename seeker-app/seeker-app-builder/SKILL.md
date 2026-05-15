---
name: seeker-app-builder
description: Router for building a Solana Mobile (Seeker) dApp end-to-end. Triggers - "build a Seeker app", "ship to dApp Store", "start Solana Mobile RN project". Delegates to sub-skills.
---

# Seeker App Builder

## Route

| State | Sub-skill |
|-------|-----------|
| No project | `seeker-app-scaffold` |
| No wallet | `mwa-setup` → `mwa-connection` (from `solana-mobile/solana-mobile-dev-skill`) — uses `@wallet-ui/react-native-web3js` |
| Need Seeker-owner gating | `genesis-token` (same repo) — SIWS + SGT check |
| Need `.skr` name resolution | `skr-address-resolution` (same repo) |
| No on-chain action | `mwa-transactions` (SOL) or `solana-pay-mobile` (USDC) |
| Untuned UX | `seeker-ux` |
| Ready to ship | `dapp-store-publishing` |
| Building a wallet (not dApp) | `seed-vault` |

## Order

scaffold → MWA setup → connection → tx action → UX → publish.

## Companion (external)

`solana-mobile/solana-mobile-dev-skill` — official MWA skills (setup/connection/transactions), Genesis Token gating, `.skr` resolution.

## Constraints

- No private keys in app code. MWA signs.
- APK only. No AAB.
- minSdkVersion 26.
- Different signing key from Google Play if dual-ship.

## Refs

- docs.solanamobile.com
- docs.solanamobile.com/dapp-store/intro
- github.com/solana-mobile/solana-mobile-dev-skill
