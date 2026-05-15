---
name: seed-vault
description: Solana Mobile Seed Vault SDK for native Android wallet apps. **Wallet devs only.** dApp builders use MWA. Triggers - "integrate Seed Vault", "build Solana wallet", "Seeker secure element", "Seed Vault Wallet API".
---

# Seed Vault

## Audience check

| Building | Use |
|----------|-----|
| Wallet app (manages seeds) | This skill |
| dApp (uses user's wallet) | **STOP.** Use MWA from `solana-mobile/solana-mobile-dev-skill` |

Misrouting = #1 mistake. Confirm before generating code.

## What

- System-level key custody. Secure element on Seeker.
- Wallet APIs: seed creation, account derivation, signing.
- Simulator for non-Seeker dev.
- Reference fake wallet.

## Stack

Native Android (Kotlin/Java). **No first-party RN bridge.** RN dApps → MWA.

## Gradle

```gradle
dependencies {
    implementation 'com.solanamobile:seedvault-wallet-sdk:0.4.0'
}
```

Check latest: github.com/solana-mobile/seed-vault-sdk/releases/latest.

## Dev w/o Seeker

Simulator (`impl/`) + fake wallet (`fakewallet/`) on emulator API 33+.

> Simulator = zero security. Test accounts only.

## Manifest

- `com.solanamobile.seedvault.WALLET_PROVIDER_SERVICE` (Seed Vault provides; you bind)
- Biometric + device-credential perms

Full list: `docs/integration_guide.md` in SDK repo.

## Core flow

1. Bind Seed Vault Wallet service.
2. Request seed authorization → user approves via system UI.
3. Derive Solana accounts: `m/44'/501'/...`.
4. Sign: message → Seed Vault API → user auth → signature.
5. Return signature (typically over MWA if exposing one).

## Never

- Export private keys. API forbids; mirroring breaks model.
- Store seed bytes anywhere app-readable.
- Bypass biometric.

## Refs

- github.com/solana-mobile/seed-vault-sdk
- github.com/solana-mobile/seed-vault-sdk/blob/main/docs/integration_guide.md
- solana-mobile.github.io/seed-vault-sdk/seedvault/javadoc/index.html
