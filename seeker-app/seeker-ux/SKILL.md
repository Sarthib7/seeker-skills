---
name: seeker-ux
description: Seeker UX conventions for RN dApps. Triggers - "Seeker UX", "add haptics", "AMOLED palette", "one-tap approval", "120Hz animation".
---

# Seeker UX

## One-tap approve

Wallet biometric = only confirmation. No `Alert.alert("Are you sure?")` before `transact()`. Long-press confirm OK for destructive only.

## Batch ixs

Combine related ixs into one Transaction. Examples: mint+transfer, wrap+swap. Never chain `transact()` calls.

## Haptics

`expo-haptics`:

| Trigger | Type |
|---------|------|
| Tap | `Impact.Light` |
| Selection | `selectionAsync()` or `Impact.Medium` |
| Tx submit | `Impact.Heavy` |
| Tx success | `Notification.Success` |
| Tx error | `Notification.Error` |

No haptics on scroll/input.

## AMOLED palette

```ts
export const colors = {
  bg: '#000000',
  surface: '#0A0A0A',
  border: '#1A1A1A',
  primary: '#9945FF',
  accent: '#14F195',
  text: '#FFFFFF',
  textMuted: '#A1A1AA',
};
```

Pure `#000` only. Never `#111`.

## Tap targets

- Min 48×48 px interactive.
- Primary button: 56 px.
- Bottom nav: `paddingBottom: insets.bottom` via `react-native-safe-area-context`.

## 120 Hz

- Animate `transform` + `opacity`. Never `width/height/top`.
- `react-native-reanimated` v3 worklets. Never legacy `Animated`.
- Easing: `cubic-bezier(0.4, 0, 0.2, 1)`.

## Security floor

- No keys/mnemonics in app code or env.
- Sign only via MWA `transact()`.

## Refs

- docs.solanamobile.com
- github.com/solana-mobile/mobile-wallet-adapter
