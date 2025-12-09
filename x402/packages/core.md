---
description: Core X402 library for building facilitators and custom integrations
---

# Core Package

The `@secured-finance/sf-x402` package provides low-level functions for payment verification and settlement. Use this when building a facilitator or custom integration.

---

## Installation

```bash
pnpm add @secured-finance/sf-x402
```

---

## Main Functions

### `verify()`

Verify a payment signature without settling on-chain.

```typescript
import { verify } from '@secured-finance/sf-x402/facilitator';
import { createConnectedClient } from '@secured-finance/sf-x402/shared/evm';

const client = createConnectedClient('sepolia');
const result = await verify(client, paymentPayload, paymentRequirements);

if (result.isValid) {
  console.log('Valid payment from:', result.payer);
} else {
  console.error('Invalid:', result.invalidReason);
}
```

**Returns:**
```typescript
{
  isValid: boolean;
  payer?: string;
  invalidReason?: string;
}
```

---

### `settle()`

Settle a payment on-chain (execute the transfer).

```typescript
import { settle } from '@secured-finance/sf-x402/facilitator';
import { createSigner } from '@secured-finance/sf-x402/shared/evm';

const signer = await createSigner('sepolia', process.env.EVM_PRIVATE_KEY!);
const result = await settle(signer, paymentPayload, paymentRequirements);

if (result.success) {
  console.log('Transaction:', result.transaction);
} else {
  console.error('Failed:', result.errorReason);
}
```

**Returns:**
```typescript
{
  success: boolean;
  transaction?: string;    // Transaction hash
  errorReason?: string;
}
```

---

### `getSupportedKinds()`

Get supported payment schemes and networks.

```typescript
import { getSupportedKinds } from '@secured-finance/sf-x402/facilitator';

const kinds = getSupportedKinds();
console.log(kinds);
// [
//   { x402Version: 1, scheme: "exact", network: "sepolia" },
//   { x402Version: 1, scheme: "exact", network: "filecoin-calibration" },
//   ...
// ]
```

---

## Utilities

### `createConnectedClient()`

Create a read-only blockchain client for verification.

```typescript
import { createConnectedClient } from '@secured-finance/sf-x402/shared/evm';

const client = createConnectedClient('sepolia', {
  rpcUrl: 'https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY'  // Optional custom RPC
});
```

### `createSigner()`

Create a wallet client for signing transactions.

```typescript
import { createSigner } from '@secured-finance/sf-x402/shared/evm';

const signer = await createSigner(
  'sepolia',
  process.env.EVM_PRIVATE_KEY!,
  {
    rpcUrl: 'https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY'  // Optional custom RPC
  }
);
```

---

## Type Definitions

```typescript
interface PaymentPayload {
  from: string;           // User wallet
  to: string;             // Merchant wallet
  value: string;          // Amount in token units
  validAfter: number;     // Unix timestamp
  validBefore: number;    // Unix timestamp
  nonce: string;          // Unique nonce
  signature: string;      // EIP-712 signature
}

interface PaymentRequirements {
  payTo: string;          // Merchant wallet
  maxAmountRequired: bigint;
  network: string;        // 'sepolia', 'filecoin-calibration', etc.
  token?: string;         // 'JPYC', 'USDC', 'USDFC'
}
```

---

## Client-Side Functions

For creating payments from user wallets:

```typescript
import { createPaymentHeader } from '@secured-finance/sf-x402/client';

// User creates and signs payment
const paymentHeader = await createPaymentHeader(
  walletClient,
  {
    to: merchantWallet,
    value: '10000000000000000',  // 0.01 JPYC (18 decimals)
    validBefore: Math.floor(Date.now() / 1000) + 300  // 5 min expiry
  }
);

// Send payment header with API request
fetch('/api/data', {
  headers: {
    'X-PAYMENT': paymentHeader
  }
});
```

---

## Example: Building a Facilitator

```typescript
import express from 'express';
import { verify, settle } from '@secured-finance/sf-x402/facilitator';
import { createConnectedClient, createSigner } from '@secured-finance/sf-x402/shared/evm';

const app = express();
app.use(express.json());

// Verify endpoint
app.post('/verify', async (req, res) => {
  const { paymentPayload, paymentRequirements } = req.body;
  const client = createConnectedClient(paymentRequirements.network);
  const result = await verify(client, paymentPayload, paymentRequirements);
  res.json(result);
});

// Settle endpoint
app.post('/settle', async (req, res) => {
  const { paymentPayload, paymentRequirements } = req.body;
  const signer = await createSigner(
    paymentRequirements.network,
    process.env.EVM_PRIVATE_KEY!
  );
  const result = await settle(signer, paymentPayload, paymentRequirements);
  res.json(result);
});

app.listen(3000);
```

**Full example:** See [GitHub repository](https://github.com/Secured-Finance/x402/tree/main/examples/typescript/facilitator)

---

## Configuration

### Custom RPC Endpoints

```typescript
const config = {
  rpcUrl: 'https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY'
};

const client = createConnectedClient('sepolia', config);
const signer = await createSigner('sepolia', privateKey, config);
```

### Environment Variables

```bash
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY
FILECOIN_CALIBRATION_RPC_URL=https://api.calibration.node.glif.io/rpc/v1
```

---

## Next Steps

- **[Facilitator Guide](../guides/facilitator-guide.md)** - Build your own facilitator
- **[Middleware Docs](middleware.md)** - Use with Express/Next.js
- **[Network Guide](../guides/network-guide.md)** - Network details
- **[GitHub Examples](https://github.com/Secured-Finance/x402/tree/main/examples)** - Working code
