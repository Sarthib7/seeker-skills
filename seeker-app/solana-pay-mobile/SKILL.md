---
name: solana-pay-mobile
description: SOL/USDC transfers in RN signed via MWA. Triggers - "add USDC payments", "Solana Pay", "send SOL", "checkout flow", "payment QR/link".
---

# Solana Pay (Mobile)

## Prereq

MWA setup done. If not → `mwa-setup` from `solana-mobile/solana-mobile-dev-skill`.

## Mints

| Token | Mainnet | Devnet |
|-------|---------|--------|
| USDC | `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v` | `4zMMC9srt5Ri5X14GAgXhaHii3GnPAEERYPJgZJDncDU` |
| SOL | native | native |

Always from constants file. Never inline.

## Build tx

`@solana/pay` = web-only. Use `@solana/web3.js`:

```ts
import { SystemProgram, Transaction } from '@solana/web3.js';
import {
  createTransferCheckedInstruction,
  getAssociatedTokenAddressSync,
  createAssociatedTokenAccountIdempotentInstruction,
} from '@solana/spl-token';

// SOL
const solIx = SystemProgram.transfer({
  fromPubkey: payer, toPubkey: recipient, lamports: sol * 1e9,
});

// USDC (6 dec)
const usdcIx = createTransferCheckedInstruction(
  getAssociatedTokenAddressSync(USDC_MINT, payer),
  USDC_MINT,
  getAssociatedTokenAddressSync(USDC_MINT, recipient),
  payer, usdc * 1e6, 6,
);
```

Recipient ATA may not exist? Prepend `createAssociatedTokenAccountIdempotentInstruction`. **Batch into same tx** (Seeker = one approval).

## Sign via MWA

```ts
import { transact } from '@solana-mobile/mobile-wallet-adapter-protocol-web3js';

const sig = await transact(async (wallet) => {
  const { blockhash } = await connection.getLatestBlockhash();
  const tx = new Transaction({ feePayer: payer, recentBlockhash: blockhash }).add(usdcIx);
  const [sent] = await wallet.signAndSendTransactions({ transactions: [tx] });
  return sent;
});
```

`signAndSendTransactions` = one tap. `signTransactions` only if inspecting before broadcast.

## Solana Pay URL

```
solana:<recipient>?amount=<n>&spl-token=<mint>&reference=<pubkey>&label=<>&message=<>
```

- `amount` in UI units (`10.50`), not lamports.
- `reference` = throwaway pubkey for tx lookup.
- `encodeURIComponent` label/message.

Incoming: parse → build tx → MWA sign.

## Confirm

```ts
await connection.confirmTransaction(
  { signature: sig, blockhash, lastValidBlockHeight }, 'confirmed',
);
```

Trigger `Notification.Success/Error` haptic.

## RPC

Never ship public RPC for mainnet. Use Helius/QuickNode/Triton via backend-issued key. Never embed in bundle.

## Refs

- docs.solanapay.com
- github.com/solana-mobile/mobile-wallet-adapter
