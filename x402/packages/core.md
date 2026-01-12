---
description: Core X402 library for x402x settlement framework
---

# Core Package

The `@secured-finance/x402-core` package provides core utilities for the x402x settlement framework - a lightweight library that extends x402 with programmable settlement capabilities.

---

## Installation

```bash
pnpm add @secured-finance/x402-core
```

---

## Quick Start

### Resource Server (Generating PaymentRequirements)

```typescript
import { addSettlementExtra, TransferHook, getNetworkConfig } from "@secured-finance/x402-core";

// Base PaymentRequirements (standard x402)
const baseRequirements = {
  scheme: "exact",
  network: "base-sepolia",
  maxAmountRequired: "100000", // 0.1 USDC
  asset: "0x036CbD53842c5426634e7929541eC2318f3dCF7e",
  payTo: merchantAddress,
  resource: "/api/payment",
};

// Add settlement extension
const requirements = addSettlementExtra(baseRequirements, {
  hook: TransferHook.getAddress("base-sepolia"),
  hookData: TransferHook.encode(),
  facilitatorFee: "10000", // 0.01 USDC
  payTo: merchantAddress,
});

// Return 402 response
res.status(402).json({
  accepts: [requirements],
  x402Version: 1,
});
```

---

## API Reference

### Core Functions

#### `calculateCommitment(params: CommitmentParams): string`

Calculate commitment hash that binds all settlement parameters.

```typescript
import { calculateCommitment } from "@secured-finance/x402-core";

const commitment = calculateCommitment({
  chainId: 84532,
  hub: "0x...",
  asset: "0x...",
  from: "0x...",
  value: "100000",
  validAfter: "0",
  validBefore: "1234567890",
  salt: "0x...",
  payTo: "0x...",
  facilitatorFee: "10000",
  hook: "0x...",
  hookData: "0x",
});
```

#### `generateSalt(): string`

Generate a random 32-byte salt for settlement uniqueness.

```typescript
import { generateSalt } from "@secured-finance/x402-core";

const salt = generateSalt();
// => '0x1234567890abcdef...'
```

#### `addSettlementExtra(requirements, params): PaymentRequirements`

Add settlement extension to PaymentRequirements.

```typescript
import { addSettlementExtra } from "@secured-finance/x402-core";

const requirements = addSettlementExtra(baseRequirements, {
  hook: "0x...",
  hookData: "0x",
  facilitatorFee: "10000",
  payTo: "0x...",
});
```

### Network Functions

#### `getNetworkConfig(network: string): NetworkConfig`

Get configuration for a specific network.

```typescript
import { getNetworkConfig } from "@secured-finance/x402-core";

const config = getNetworkConfig("base-sepolia");
// => { chainId: 84532, settlementRouter: '0x...', ... }
```

#### `getSupportedNetworks(): string[]`

Get list of all supported networks.

```typescript
import { getSupportedNetworks } from "@secured-finance/x402-core";

const networks = getSupportedNetworks();
// => ['base-sepolia', 'x-layer-testnet']
```

### Built-in Hooks

#### `TransferHook`

TransferHook for simple transfers and revenue splits.

```typescript
import { TransferHook } from "@secured-finance/x402-core";

// Get address for a network
const hookAddress = TransferHook.getAddress("base-sepolia");

// Encode hook data (simple transfer)
const hookData = TransferHook.encode();

// Encode hook data with revenue split
const hookDataWithSplit = TransferHook.encode([
  { recipient: "0xAlice...", bips: 6000 }, // 60% to Alice
  { recipient: "0xBob...", bips: 4000 }, // 40% to Bob
]);
```

#### `NFTMintHook`

NFTMintHook for NFT minting operations.

```typescript
import { NFTMintHook } from "@secured-finance/x402-core";

const hookAddress = NFTMintHook.getAddress("base-sepolia");
const hookData = NFTMintHook.encode({
  collection: "0x...",
  tokenId: 1,
});
```

#### `RewardHook`

RewardHook for reward point distribution.

```typescript
import { RewardHook } from "@secured-finance/x402-core";

const hookAddress = RewardHook.getAddress("base-sepolia");
const hookData = RewardHook.encode({
  recipient: "0x...",
  points: 1000,
});
```

### Amount Utilities

#### `parseDefaultAssetAmount(usdAmount: string, network: string): string`

Convert USD amount to atomic units for the default asset on a network.

```typescript
import { parseDefaultAssetAmount } from "@secured-finance/x402-core";

const atomicAmount = parseDefaultAssetAmount("1", "base-sepolia");
// => '1000000' (1 USDC with 6 decimals)
```

#### `formatDefaultAssetAmount(atomicAmount: string, network: string): string`

Convert atomic units back to USD amount for display.

```typescript
import { formatDefaultAssetAmount } from "@secured-finance/x402-core";

const displayAmount = formatDefaultAssetAmount("1000000", "base-sepolia");
// => '1'
```

### Facilitator API

The core package provides HTTP client functions to interact with facilitator services.

#### `verify(facilitatorUrl, paymentPayload, paymentRequirements): Promise<VerifyResponse>`

Verify a payment payload with a facilitator without executing it.

```typescript
import { verify } from "@secured-finance/x402-core";

const result = await verify("https://facilitator.x402x.dev", paymentPayload, paymentRequirements);

if (result.isValid) {
  console.log("Payment is valid, payer:", result.payer);
} else {
  console.error("Invalid payment:", result.invalidReason);
}
```

#### `settle(facilitatorUrl, paymentPayload, paymentRequirements, timeout?): Promise<SettleResponse>`

Settle a payment with a facilitator service.

```typescript
import { settle } from "@secured-finance/x402-core";

const result = await settle(
  "https://facilitator.x402x.dev",
  paymentPayload,
  paymentRequirements,
  30000, // optional timeout in ms
);

if (result.success) {
  console.log("Settlement successful!");
  console.log("Transaction:", result.transaction);
  console.log("Network:", result.network);
} else {
  console.error("Settlement failed:", result.errorReason);
}
```

#### `calculateFacilitatorFee(facilitatorUrl, network, hook, hookData?): Promise<FeeCalculationResult>`

Calculate recommended facilitator fee from a facilitator service.

```typescript
import { calculateFacilitatorFee } from "@secured-finance/x402-core";

const feeResult = await calculateFacilitatorFee(
  "https://facilitator.x402x.dev",
  "base-sepolia",
  "0x1234...",
  "0x",
);

console.log(`Fee: ${feeResult.facilitatorFee} (${feeResult.facilitatorFeeUSD} USD)`);
```

#### Other Utilities

- `isSettlementMode(paymentRequirements)` - Check if SettlementRouter mode is required
- `parseSettlementExtra(extra)` - Parse and validate settlement extra parameters
- `clearFeeCache()` - Clear the fee calculation cache

---

## Supported Networks

**Mainnet (Live):**
- **base**: Base Mainnet - Production payments
- **x-layer**: X-Layer Mainnet - Production payments

**Testnet:**
- **base-sepolia**: Base Sepolia testnet
- **x-layer-testnet**: X-Layer testnet
- **sepolia**: Sepolia testnet (JPYC, USDC)
- **filecoin-calibration**: Filecoin Calibration testnet (USDFC)

See [Network Guide](../guides/network-guide.md) for full details and contract addresses.

---

## Type Definitions

```typescript
interface CommitmentParams {
  chainId: number;
  hub: string;
  asset: string;
  from: string;
  value: string;
  validAfter: string;
  validBefore: string;
  salt: string;
  payTo: string;
  facilitatorFee: string;
  hook: string;
  hookData: string;
}

interface NetworkConfig {
  chainId: number;
  name: string;
  type: "testnet" | "mainnet";
  settlementRouter: string;
  defaultAsset: {
    address: string;
    symbol: string;
    decimals: number;
    eip712: {
      name: string;
      version: string;
    };
  };
  hooks: {
    transfer: string;
  };
  demoHooks?: {
    nftMint?: string;
    randomNFT?: string;
    reward?: string;
    rewardToken?: string;
  };
}

interface SettlementExtra {
  settlementRouter: string;
  salt: string;
  payTo: string;
  facilitatorFee: string;
  hook: string;
  hookData: string;
}
```

---

## Next Steps

- **[Express Middleware](express.md)** - Use with Express.js
- **[Hono Middleware](hono.md)** - Use with Hono
- **[Client SDK](client.md)** - Client-side integration
- **[Network Guide](../guides/network-guide.md)** - Network details
- **[Facilitator Guide](../guides/facilitator-guide.md)** - Build your own facilitator
