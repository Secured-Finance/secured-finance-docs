---
description: Core X402 library for building facilitators and custom integrations
---

# Core Package (@secured-finance/sf-x402)

The core package provides low-level functions for payment verification and settlement. Use this package if you're building a facilitator service or need direct access to the X402 protocol.

---

## Installation

```bash
pnpm add @secured-finance/sf-x402
```

---

## Facilitator Functions

### `verify()`

Verify a payment signature without settling on-chain.

```typescript
import { verify } from '@secured-finance/sf-x402/facilitator';
import { createConnectedClient } from '@secured-finance/sf-x402/shared/evm';

// Create a read-only client for verification
const client = createConnectedClient('sepolia');

const result = await verify(client, paymentPayload, paymentRequirements);

if (result.isValid) {
  console.log('Payment valid from:', result.payer);
} else {
  console.error('Invalid:', result.invalidReason);
}
```

**Parameters:**
- `client: ConnectedClient` - Blockchain client for reading state
- `paymentPayload: PaymentPayload` - Signed payment from user
- `paymentRequirements: PaymentRequirements` - What merchant requires
- `config?: X402Config` - Optional configuration (custom RPC URLs)

**Returns:**
```typescript
{
  isValid: boolean;
  payer?: string;           // User's wallet address
  invalidReason?: string;   // Error reason if invalid
}
```

---

### `settle()`

Settle a payment on blockchain (execute the transfer).

```typescript
import { settle } from '@secured-finance/sf-x402/facilitator';
import { createSigner } from '@secured-finance/sf-x402/shared/evm';

// Create a signer wallet (this wallet pays gas and receives fees)
const signer = await createSigner('sepolia', process.env.EVM_PRIVATE_KEY!);

const result = await settle(signer, paymentPayload, paymentRequirements);

if (result.success) {
  console.log('Transaction:', result.transaction);
} else {
  console.error('Failed:', result.errorReason);
}
```

**Parameters:**
- `signer: Signer` - Wallet client for signing transactions (pays gas)
- `paymentPayload: PaymentPayload` - Signed payment from user
- `paymentRequirements: PaymentRequirements` - What merchant requires
- `config?: X402Config` - Optional configuration (custom RPC URLs)

**Returns:**
```typescript
{
  success: boolean;
  transaction?: string;     // Transaction hash
  network?: string;         // Network name
  payer?: string;          // User's wallet
  errorReason?: string;    // Error if failed
}
```

---

### `getSupportedKinds()`

Get list of supported payment types.

```typescript
import { getSupportedKinds } from '@secured-finance/sf-x402/facilitator';

const kinds = getSupportedKinds();
console.log(kinds);
```

**Returns:**
```typescript
Array<{
  x402Version: number;
  scheme: string;
  network: string;
}>
```

**Example output:**
```typescript
[
  { x402Version: 1, scheme: "exact", network: "sepolia" },
  { x402Version: 1, scheme: "exact", network: "polygon" },
  { x402Version: 1, scheme: "exact", network: "filecoin-calibration" },
  { x402Version: 1, scheme: "exact", network: "base" }
]
```

---

## Client Functions

### `selectPaymentRequirements()`

Select the best payment requirement from a list (used by clients to choose which token to pay with).

```typescript
import { selectPaymentRequirements } from '@secured-finance/sf-x402/client';

// From 402 response, select which payment option to use
const selectedRequirement = selectPaymentRequirements(
  accepts,           // Array of payment requirements from 402 response
  'sepolia',         // Optional: filter by network
  'exact'            // Optional: filter by scheme
);
```

**Parameters:**
- `requirements: PaymentRequirements[]` - Array of payment options from 402 response
- `network?: Network` - Optional network filter
- `scheme?: string` - Optional scheme filter (default: "exact")

**Returns:** `PaymentRequirements` - Selected payment requirement

**Behavior:**
- Prioritizes USDC tokens when available
- Falls back to first available requirement if no USDC found
- Filters by network/scheme if provided

---

### `createPaymentHeader()`

Create a signed payment header for the X-PAYMENT HTTP header (client-side).

```typescript
import { createPaymentHeader } from '@secured-finance/sf-x402/client';

// walletClient is a wagmi/viem wallet client
const paymentHeader = await createPaymentHeader(
  walletClient,
  1,                      // x402Version
  paymentRequirement,     // From selectPaymentRequirements
  { evmConfig: { rpcUrls: { sepolia: 'https://...' } } }
);

// Use in request
const response = await fetch(url, {
  headers: { 'X-PAYMENT': paymentHeader }
});
```

**Parameters:**
- `client: WalletClient` - Wagmi/viem wallet client for signing
- `x402Version: number` - Protocol version (currently 1)
- `paymentRequirements: PaymentRequirements` - Selected payment requirement
- `config?: X402Config` - Optional configuration

**Returns:** `string` - Base64-encoded payment header

---

## Utility Functions

### `calculateFee()`

Calculate facilitator fee for a payment.

```typescript
import { calculateFee } from '@secured-finance/sf-x402';

const { feeAmount, merchantAmount } = calculateFee(
  BigInt(1000000),  // 1.00 USDC (6 decimals)
  6                 // Token decimals
);

console.log('Fee:', feeAmount);       // 10000n (0.01 USDC - minimum)
console.log('Merchant:', merchantAmount); // 990000n (0.99 USDC)
```

**Parameters:**
- `totalAmount: bigint` - Payment amount in atomic units
- `decimals: number` - Token decimals (6 for USDC, 18 for JPYC/USDFC)

**Returns:**
```typescript
{
  feeAmount: bigint;        // Fee in atomic units
  merchantAmount: bigint;   // Merchant receives in atomic units
}
```

---

### `usdToAtomic()`

Convert USD amount to atomic units (avoids floating-point precision issues).

```typescript
import { usdToAtomic } from '@secured-finance/sf-x402';

const usdc = usdToAtomic(1.25, 6);   // "1250000" (6 decimals)
const jpyc = usdToAtomic(1.25, 18);  // "1250000000000000000" (18 decimals)
```

**Parameters:**
- `usdAmount: number` - USD amount (e.g., 1.25)
- `decimals: number` - Token decimals

**Returns:** `string` - Atomic units as string

---

## TypeScript Types

### Core Types

```typescript
// Payment payload (what user sends in X-PAYMENT header)
type PaymentPayload = {
  x402Version: number;
  scheme: "exact";
  network: Network;
  payload: ExactEvmPayload;
};

// EVM payment payload (EIP-3009 authorization)
type ExactEvmPayload = {
  signature: Hex;                  // EIP-712 signature
  authorization: {
    from: Address;                 // Payer wallet
    to: Address;                   // Merchant wallet
    value: string;                 // Amount in atomic units
    validAfter: string;            // Unix timestamp (start)
    validBefore: string;           // Unix timestamp (expiry)
    nonce: Hex;                    // Random 32-byte hex (0x + 64 chars)
  };
};

// What merchant requires (from 402 response)
type PaymentRequirements = {
  scheme: "exact";
  network: Network;
  maxAmountRequired: string;       // Amount in atomic units
  resource: string;                // API endpoint URL
  description: string;             // Human-readable description
  mimeType: string;                // Response content type
  payTo: Address;                  // Merchant wallet
  maxTimeoutSeconds: number;       // Payment expiration (default: 60)
  asset: Address;                  // Token contract address
  extra?: {
    name?: string;                 // Token name
    symbol?: string;               // Token symbol (JPYC, USDFC, USDC)
    decimals?: number;             // Token decimals (6 or 18)
    useFeeReceiver?: boolean;      // Use FeeReceiver contract
  };
  outputSchema?: object;           // Expected response schema
};

// Supported networks
type Network =
  | "sepolia"                      // JPYC testnet
  | "mainnet"                      // JPYC mainnet (Ethereum)
  | "filecoin"                     // USDFC mainnet
  | "filecoin-calibration"         // USDFC testnet
  | "polygon"                      // JPYC mainnet
  | "polygon-amoy"                 // Testnet
  | "base"                         // USDC mainnet
  | "base-sepolia";                // USDC testnet
```

---

## Error Handling

### Common Errors

#### "Insufficient balance"

```json
{
  "isValid": false,
  "invalidReason": "Insufficient balance"
}
```

**Cause**: User doesn't have enough tokens
**Solution**: User needs to acquire tokens from faucet (testnet) or DEX (mainnet)

---

#### "Nonce already used"

```json
{
  "success": false,
  "errorReason": "Nonce already used"
}
```

**Cause**: Payment was already settled (replay protection)
**Solution**: This is correct behavior - user needs new payment

---

#### "Payment expired"

```json
{
  "isValid": false,
  "invalidReason": "Payment expired (validBefore passed)"
}
```

**Cause**: Payment deadline passed
**Solution**: Increase `maxTimeoutSeconds` or user creates new payment

---

#### "Invalid signature"

```json
{
  "isValid": false,
  "invalidReason": "Invalid signature"
}
```

**Cause**: Signature doesn't match payment data
**Solution**: Check network matches, wallet address correct, no tampering

---

## Related Resources

* [🚀 Quick Start](../quick-start.md) - Get started in 10 minutes
* [📦 Express Package](express.md) - Express middleware
* [📦 Next.js Package](next.md) - Next.js middleware
* [🏦 Facilitator Guide](../guides/facilitator-guide.md) - Build your own facilitator
* [🌍 Network Guide](../guides/network-guide.md) - Choose the right network
