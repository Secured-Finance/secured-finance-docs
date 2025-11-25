---
description: Complete API documentation for all X402 packages
---

# 📚 API Reference

Complete reference for all published X402 packages and their APIs.

---

## Published Packages

| Package | Version | Description | Install |
|---------|---------|-------------|---------|
| `@secured-finance/sf-x402` | 0.1.0 | Core library | `pnpm add @secured-finance/sf-x402` |
| `@secured-finance/sf-x402-express` | 0.1.0 | Express middleware | `pnpm add @secured-finance/sf-x402-express` |
| `@secured-finance/sf-x402-next` | 0.1.0 | Next.js middleware | `pnpm add @secured-finance/sf-x402-next` |

---

## Core Package (@secured-finance/sf-x402)

### Facilitator Functions

#### `verify()`

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

#### `settle()`

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

#### `getSupportedKinds()`

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

### Client Functions

#### `selectPaymentRequirements()`

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

#### `createPaymentHeader()`

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

### Fee Calculation

#### `calculateFee()`

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

### USD to Atomic Conversion

#### `usdToAtomic()`

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

## Express Middleware (@secured-finance/sf-x402-express)

### `paymentMiddleware()`

Create payment middleware for Express.js applications.

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.get('/data', paymentMiddleware(
  payTo,           // Merchant wallet
  routes,          // Route config
  facilitator,     // Facilitator URL
  paywall          // Optional paywall config
), (req, res) => {
  res.json({ data: 'premium content' });
});
```

---

#### Parameters

**1. `payTo: Address`**

Merchant wallet address (where payments go).

```typescript
const payTo = "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb";
```

---

**2. `routes: RoutesConfig`**

Route patterns and payment requirements.

```typescript
const routes = {
  'GET /weather/:city': {
    price: '$0.01',
    network: 'polygon',
    token: 'JPYC'
  },
  'POST /checkout': {
    price: '$9.99',
    network: 'filecoin-mainnet',
    token: 'USDFC'
  }
};
```

**Route config options:**

```typescript
type RouteConfig = {
  // Required
  price: Money | ERC20TokenAmount;  // "$0.01" or { amount: "10000", asset: {...} }
  network: Network;                  // "sepolia", "polygon", "filecoin-mainnet", etc.

  // Optional
  token?: string;                    // "USDC", "JPYC", "USDFC" (filter available tokens)
  config?: {
    description?: string;            // Payment description
    maxTimeoutSeconds?: number;      // Payment expiration (default: 60s)
    customPaywallHtml?: string;      // Custom paywall HTML
  }
};
```

---

**3. `facilitator?: FacilitatorConfig`**

Facilitator service configuration.

```typescript
const facilitator = {
  url: 'https://facilitator.x402.org'
};
```

---

**4. `paywall?: PaywallConfig`**

Optional paywall customization and Coinbase onramp integration.

```typescript
type PaywallConfig = {
  cdpClientKey?: string;           // Coinbase Developer Platform API key
  appName?: string;                // Application name for wallet modal
  appLogo?: string;                // Logo URL for wallet modal
  sessionTokenEndpoint?: string;   // Custom endpoint for session tokens
  customPaywallHtml?: string;      // Custom paywall HTML
};

const paywall = {
  // Coinbase onramp integration (optional)
  cdpClientKey: process.env.CDP_CLIENT_KEY,
  appName: 'My Weather API',
  appLogo: '/logo.svg',
  sessionTokenEndpoint: '/api/x402/session-token',

  // Custom HTML (optional)
  customPaywallHtml: `
    <html>
      <body>
        <h1>Premium Content</h1>
        <p>Pay $0.01 to unlock</p>
        <!-- X402 injects payment button here -->
      </body>
    </html>
  `
};
```

---

### `POST()` - Session Token Handler

Generate Coinbase onramp session tokens for secure wallet funding.

```typescript
import { POST } from '@secured-finance/sf-x402-express/session-token';

// Add session token endpoint for Coinbase onramp
app.post('/api/x402/session-token', POST);
```

**Request body:**
```typescript
{
  addresses: Array<{
    address: string;
    blockchains?: string[];  // defaults to ["base"]
  }>;
  assets?: string[];
}
```

**Returns:** Session token for Coinbase onramp widget

---

### Complete Example

```typescript
import express from 'express';
import { paymentMiddleware, POST } from '@secured-finance/sf-x402-express';

const app = express();
app.use(express.json());

const merchantWallet = "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb";
const facilitatorUrl = "https://x402.org/facilitator";

// Optional: Add session token endpoint for Coinbase onramp
app.post('/api/x402/session-token', POST);

// JPYC payment on Sepolia (testnet)
app.get('/weather/:city', paymentMiddleware(
  merchantWallet,
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'sepolia',
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), (req, res) => {
  res.json({ temp: 72, condition: 'sunny' });
});

// USDFC payment on Filecoin Calibration (testnet)
app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$9.99',
      network: 'filecoin-calibration',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), (req, res) => {
  res.json({
    cid: 'bafy...',
    status: 'stored'
  });
});

// Dynamic pricing example
app.post('/translate', (req, res, next) => {
  const wordCount = req.body.text.split(' ').length;
  const price = Math.max(0.01, wordCount * 0.001);

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /translate': {
        price: `$${price.toFixed(2)}`,
        network: 'sepolia',
        token: 'JPYC'
      }
    },
    { url: facilitatorUrl }
  );

  middleware(req, res, next);
}, (req, res) => {
  res.json({ translation: 'Translated text...' });
});

app.listen(4000, () => {
  console.log('Server running on http://localhost:4000');
});
```

---

## Next.js Middleware (@secured-finance/sf-x402-next)

### `paymentMiddleware()`

Create payment middleware for Next.js applications (App Router or Pages Router).

```typescript
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function GET(request: NextRequest) {
  const middleware = paymentMiddleware(
    merchantWallet,
    routes,
    facilitator
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse; // 402 if unpaid

  // Payment verified - return data
  return Response.json({ data: 'premium' });
}
```

---

### App Router Example

```typescript
// app/api/weather/[city]/route.ts
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function GET(
  request: NextRequest,
  { params }: { params: { city: string } }
) {
  // JPYC payment on Sepolia testnet
  const middleware = paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      'GET /api/weather/:city': {
        price: '$0.01',
        network: 'sepolia',
        token: 'JPYC'
      }
    },
    { url: process.env.FACILITATOR_URL! }
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse;

  return Response.json({
    city: params.city,
    temp: 72,
    condition: 'sunny'
  });
}
```

### USDFC Example (Filecoin)

```typescript
// app/api/store/route.ts
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function POST(request: NextRequest) {
  // USDFC payment on Filecoin Calibration testnet
  const middleware = paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      'POST /api/store': {
        price: '$9.99',
        network: 'filecoin-calibration',
        token: 'USDFC'
      }
    },
    { url: process.env.FACILITATOR_URL! }
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse;

  const body = await request.json();
  // Store data to Filecoin...

  return Response.json({
    cid: 'bafy...',
    status: 'stored'
  });
}
```

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

// Supported networks (focused on JPYC and USDFC)
type Network =
  | "sepolia"                      // JPYC testnet
  | "mainnet"                      // JPYC mainnet (Ethereum)
  | "filecoin"                     // USDFC mainnet
  | "filecoin-calibration"         // USDFC testnet
  | "polygon"                      // JPYC mainnet
  | "polygon-amoy"                 // Testnet
  | "base"                         // USDC mainnet
  | "base-sepolia";                // USDC testnet

// Price formats
type Money = `$${number}`;  // "$0.01", "$9.99", etc.

type ERC20TokenAmount = {
  amount: string;
  asset: {
    address: Address;
    decimals: number;
    symbol: string;
  };
};

// Configuration
type X402Config = {
  evmConfig?: {
    rpcUrls?: Record<string, string>;  // network -> RPC URL mapping
  };
};
```

---

## Error Codes

### HTTP Status Codes

| Code | Meaning | Solution |
|------|---------|----------|
| `402` | Payment Required | User needs to pay |
| `400` | Invalid Payment | Check signature/format |
| `500` | Facilitator Error | Check facilitator logs |

---

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

## Network Configuration

### Supported Networks

#### Primary Networks (JPYC & USDFC)

| Network | Chain ID | Token | Decimals | Block Time | Finality |
|---------|----------|-------|----------|------------|----------|
| **Sepolia** (testnet) | 11155111 | JPYC | 18 | ~12s | ~2min |
| **Ethereum** (mainnet) | 1 | JPYC | 18 | ~12s | ~2min |
| **Polygon** (mainnet) | 137 | JPYC | 18 | ~2s | ~5s |
| **Filecoin Calibration** (testnet) | 314159 | USDFC | 18 | ~30s | ~60s |
| **Filecoin** (mainnet) | 314 | USDFC | 18 | ~30s | ~60s |

#### Additional Networks (USDC)

| Network | Chain ID | Token | Decimals | Block Time | Finality |
|---------|----------|-------|----------|------------|----------|
| **Base** | 8453 | USDC | 6 | ~2s | ~2s |
| **Base Sepolia** | 84532 | USDC | 6 | ~2s | ~2s |
| **Polygon Amoy** | 80002 | USDC | 6 | ~2s | ~5s |

---

### Token Addresses

#### JPYC (Japanese Yen Coin - 18 decimals)

```typescript
// Testnets
const SEPOLIA_JPYC = "0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29";

// Mainnets
const ETHEREUM_JPYC = "0x2370f9d504c7a6e775bf6e14b3f12846b594cd53";
const POLYGON_JPYC = "0x6AE7Dfc73E0dDE2aa99ac063DcF7e8A63265108c";
```

#### USDFC (USD for Filecoin Community - 18 decimals)

```typescript
// Testnets
const CALIBRATION_USDFC = "0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0";

// Mainnets
const FILECOIN_USDFC = "0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0";
```

#### USDC (USD Coin - 6 decimals)

```typescript
// Testnets
const SEPOLIA_USDC = "0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238";
const BASE_SEPOLIA_USDC = "0x036CbD53842c5426634e7929541eC2318f3dCF7e";

// Mainnets
const ETHEREUM_USDC = "0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48";
const POLYGON_USDC = "0x3c499c542cEF5E3811e1192ce70d8cC03d5c3359";
const BASE_USDC = "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913";
```

---

### FeeReceiver Contracts

The FeeReceiver contract automatically splits payments: 99.7% to merchant, 0.3% to facilitator.

```typescript
// Testnets
const SEPOLIA_FEE_RECEIVER = "0x8F35dfEC24944b5f87A97D38402dfA9117110d77";
const CALIBRATION_FEE_RECEIVER = "0x0f7A0E7942d1b7a60921Ec99E655402Bd014FDC2";
```

---

## Troubleshooting

### Enable Debug Logs

```typescript
// Set environment variable
process.env.DEBUG = 'x402:*';

// Or in .env file
DEBUG=x402:*
```

---

### Test Payment Flow

Use curl to test the full flow:

```bash
# 1. Request without payment (get 402)
curl -v http://localhost:4000/weather/tokyo

# 2. Get payment requirements from 402 response
# Extract requirements from HTML

# 3. Sign payment in wallet (use browser/MetaMask)

# 4. Retry with X-PAYMENT header
curl http://localhost:4000/weather/tokyo \
  -H "X-PAYMENT: base64EncodedPayment"
```

---

## Related Resources

* [Overview](overview.md) - What is X402?
* [Network Guide](network-guide.md) - Choose the right network
* [Quick Start](quick-start.md) - Build your first paid API
* [Facilitator Guide](facilitator-guide.md) - Deploy and earn fees

---

## Community & Support

* 📖 [GitHub](https://github.com/Secured-Finance/x402) - Source code & issues
* 💬 [Discord](https://discord.gg/securedfinance) - Community support
* 🐦 [Twitter](https://twitter.com/securedfinance) - Updates
* 📧 [Email](mailto:support@secured.finance) - Direct support

---

**Need help?** [Open an issue](https://github.com/Secured-Finance/x402/issues) or join [Discord](https://discord.gg/securedfinance)
