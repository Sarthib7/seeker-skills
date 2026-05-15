# seeker-skills

Claude Code skills for building Solana Mobile (Seeker) dApps. Complements `solana-mobile/solana-mobile-dev-skill` (MWA, `.skr`, Genesis Token).

## Layout

```
seeker-app/
├── seeker-app-builder/      # router — "build a Seeker app"
├── seeker-app-scaffold/     # npm create solana-dapp + Android toolchain
├── seeker-ux/               # one-tap, haptics, AMOLED, 120Hz
├── solana-pay-mobile/       # USDC/SOL via MWA
├── seed-vault/              # wallet devs only
└── dapp-store-publishing/   # APK sign + dapp-store CLI
```

## Install

```bash
# This set
cp -r seeker-app/* ~/.claude/skills/

# Official companion
git clone https://github.com/solana-mobile/solana-mobile-dev-skill
cp -r solana-mobile-dev-skill/mwa/* ~/.claude/skills/
cp -r solana-mobile-dev-skill/genesis-token ~/.claude/skills/
cp -r solana-mobile-dev-skill/skr-address-resolution ~/.claude/skills/
```

## Route

Start at `seeker-app-builder`. Enforces: scaffold → MWA → tx → UX → publish.

## Not

- Not a replacement for MWA skills. Install both.
- Not for wallet developers (except `seed-vault/`).
- Not the full spec. Read docs.solanamobile.com.

## Frontmatter

```yaml
---
name: <slug>
description: <capability + trigger phrases>
---
```

No other fields. Triggers in description.

## License

CC0.
