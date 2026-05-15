---
name: seeker-app-scaffold
description: Scaffold Solana Mobile RN app. Triggers - "create Solana Mobile app", "start Seeker dApp", "solana.new", "set up Android toolchain".
---

# Seeker App Scaffold

## Prereq

```bash
node -v          # >= 20
java -version    # JDK 17
adb version
```

macOS missing:

```bash
brew install --cask zulu@17
brew install android-platform-tools
```

`ANDROID_HOME=~/Library/Android/sdk`. Add `$ANDROID_HOME/platform-tools` to PATH.

## Scaffold

```bash
npm create solana-dapp@latest
# Category: Mobile
# Template: solana-mobile-expo-template (or other Expo RN template)
cd <name> && npm install && npm run android
```

Direct template (skip prompts):

```bash
npm create solana-dapp@latest -t gh:solana-foundation/templates/mobile/solana-mobile-expo-template
```

## Config

- `app.json` → `expo.android.package` = final reverse-DNS id. Must match dApp Store entry.
- `android/app/build.gradle` → `minSdkVersion 26` (MWA req).

## Rule

MWA = native modules. **Expo Go fails.** Always dev client:

```bash
npx expo prebuild --platform android --clean
npx expo run:android
```

## Pitfalls

| Error | Fix |
|-------|-----|
| `SDK location not found` | Set `ANDROID_HOME`; `android/local.properties` with `sdk.dir=...` |
| `Unable to locate a Java Runtime` | JDK 17 + `export JAVA_HOME=$(/usr/libexec/java_home -v 17)` |
| MWA error in Expo Go | Use dev client, not Go |

## Refs

- docs.solanamobile.com/get-started/react-native/create-solana-mobile-app
- docs.solanamobile.com/get-started/react-native/setup
