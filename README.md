# seeker-skills

Claude Code skills for building Solana Mobile (Seeker) dApps. Complements `solana-mobile/solana-mobile-dev-skill` (MWA, `.skr`, Genesis Token).

## Index

| Skill | Use when | Don't |
|-------|----------|-------|
| [`seeker-app-builder`](seeker-app/seeker-app-builder/SKILL.md) | "build a Seeker app" / multi-phase | Single phase → call sub-skill |
| [`seeker-app-scaffold`](seeker-app/seeker-app-scaffold/SKILL.md) | No project yet / toolchain setup | Already scaffolded |
| [`seeker-ux`](seeker-app/seeker-ux/SKILL.md) | Polish UX, haptics, AMOLED, 120 Hz | App doesn't run yet |
| [`solana-pay-mobile`](seeker-app/solana-pay-mobile/SKILL.md) | Move SOL/USDC, Solana Pay URLs | MWA not set up |
| [`seed-vault`](seeker-app/seed-vault/SKILL.md) | Wallet app (Android native) | Building a dApp |
| [`dapp-store-publishing`](seeker-app/dapp-store-publishing/SKILL.md) | Sign + ship APK | App not built / no publisher account |

Each `SKILL.md` opens with its own `Use` / `Not` block so an agent can confirm fit before reading further.

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
