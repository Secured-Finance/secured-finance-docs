---
description: Express.js middleware for X402 payments
---

# Express Middleware (@secured-finance/sf-x402-express)

Drop-in Express middleware for payment-gated API endpoints. Add paid routes with just 3 lines of code.

---

## Installation

```bash
pnpm add @secured-finance/sf-x402-express express dotenv
pnpm add -D typescript @types/express @types/node
```

---

## Quick Example

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

const app = express();

app.get('/weather/:city', paymentMiddleware(
  "0xYourWallet",                 // Where payments go
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'sepolia',
      token: 'JPYC'
    }
  },
  { url: 'https://x402.org/facilitator' }
), (req, res) => {
  res.json({ temp: 72, condition: 'sunny' });
});

app.listen(4000);
```

---

## API Reference

### `paymentMiddleware()`

Create payment middleware for Express.js applications.

```typescript
function paymentMiddleware(
  payTo: Address,
  routes: RoutesConfig,
  facilitator?: FacilitatorConfig,
  paywall?: PaywallConfig
): Middleware
```

---

## Parameters

### 1. `payTo` (required)

Merchant wallet address where payments are sent.

```typescript
const payTo = "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb";
```

**Type:** `Address` (0x-prefixed hex string)

---

### 2. `routes` (required)

Route patterns and their payment requirements.

```typescript
const routes = {
  'GET /weather/:city': {
    price: '$0.01',
    network: 'polygon',
    token: 'JPYC'
  },
  'POST /checkout': {
    price: '$9.99',
    network: 'filecoin',
    token: 'USDFC'
  }
};
```

**Type:** `RoutesConfig`

#### Route Config Options

```typescript
type RouteConfig = {
  // Required
  price: Money | ERC20TokenAmount;  // "$0.01" or { amount: "10000", asset: {...} }
  network: Network;                  // "sepolia", "polygon", "filecoin", etc.

  // Optional
  token?: string;                    // "USDC", "JPYC", "USDFC" (filter available tokens)
  config?: {
    description?: string;            // Payment description
    maxTimeoutSeconds?: number;      // Payment expiration (default: 60s)
    customPaywallHtml?: string;      // Custom paywall HTML
  }
};
```

**Price Formats:**
- USD strings: `'$1.50'`, `'$0.001'`
- Numbers: `1.5`, `0.001`
- Atomic units: `{ amount: '1000000', asset: { address, decimals, eip712 } }`

---

### 3. `facilitator` (optional)

Facilitator service configuration.

```typescript
const facilitator = {
  url: 'https://x402.org/facilitator'
};
```

**Type:** `FacilitatorConfig`

**Default:** Uses public facilitator if not specified

---

### 4. `paywall` (optional)

Paywall customization and Coinbase Onramp integration.

```typescript
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

**Type:** `PaywallConfig`

---

## Complete Example

```typescript
import express from 'express';
import { paymentMiddleware, POST } from '@secured-finance/sf-x402-express';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
app.use(express.json());

const merchantWallet = process.env.MERCHANT_WALLET!;
const facilitatorUrl = process.env.FACILITATOR_URL!;

// Optional: Add session token endpoint for Coinbase onramp
app.post('/api/x402/session-token', POST);

// JPYC payment on Sepolia (testnet)
app.get('/weather/:city', paymentMiddleware(
  merchantWallet,
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'sepolia',
      token: 'JPYC',
      config: {
        description: 'Premium weather data'
      }
    }
  },
  { url: facilitatorUrl }
), (req, res) => {
  const txHash = res.getHeader('X-PAYMENT-TX-HASH');
  const explorer = res.getHeader('X-PAYMENT-TX-EXPLORER');

  res.json({
    city: req.params.city,
    temp: 72,
    condition: 'sunny',
    payment: { txHash, explorer }
  });
});

// USDFC payment on Filecoin Calibration (testnet)
app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$9.99',
      network: 'filecoin-calibration',
      token: 'USDFC',
      config: {
        description: 'Storage subscription'
      }
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
  console.log('Payments go to:', merchantWallet);
});
```

---

## Response Headers

After successful payment, the middleware adds these headers to the response:

| Header | Description | Example |
|--------|-------------|---------|
| `X-PAYMENT-RESPONSE` | Settlement result | `{success: true, transaction: "0x..."}` |
| `X-PAYMENT-TX-HASH` | Transaction hash | `0x1234...` |
| `X-PAYMENT-TX-EXPLORER` | Block explorer URL | `https://sepolia.etherscan.io/tx/0x...` |

**Accessing headers:**

```typescript
app.get('/data', paymentMiddleware(...), (req, res) => {
  const txHash = res.getHeader('X-PAYMENT-TX-HASH');
  const explorer = res.getHeader('X-PAYMENT-TX-EXPLORER');

  res.json({
    data: 'premium content',
    payment: { txHash, explorer }
  });
});
```

---

## Session Token API (Coinbase Onramp)

Generate Coinbase onramp session tokens for secure wallet funding.

```typescript
import { POST } from '@secured-finance/sf-x402-express/session-token';

// Add session token endpoint
app.post('/api/x402/session-token', POST);
```

**Environment Variables:**
```bash
CDP_API_KEY_ID=your_key_id
CDP_API_KEY_SECRET=your_key_secret
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

## Error Responses

When payment is required, the middleware returns a 402 status with payment requirements:

```json
{
  "x402Version": 1,
  "error": "payment_required",
  "accepts": [
    {
      "scheme": "exact",
      "network": "sepolia",
      "maxAmountRequired": "10000000000000000",
      "resource": "/weather/tokyo",
      "description": "Premium weather data",
      "payTo": "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb",
      "asset": "0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29",
      "extra": {
        "symbol": "JPYC",
        "decimals": 18,
        "useFeeReceiver": true
      }
    }
  ]
}
```

**Common Error Codes:**

| Error | Meaning | HTTP Status |
|-------|---------|-------------|
| `payment_required` | No payment provided | 402 |
| `nonce_already_used` | Payment already settled | 402 |
| `invalid_signature` | Signature verification failed | 400 |
| `insufficient_balance` | User has insufficient funds | 400 |

---

## TypeScript Types

```typescript
import type {
  Network,
  Money,
  PaymentMiddlewareConfig,
  RouteConfig,
  RoutesConfig,
  Resource
} from '@secured-finance/sf-x402-express';

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

// Route configuration
type RouteConfig = {
  price: Money | ERC20TokenAmount;
  network: Network;
  token?: string;
  config?: {
    description?: string;
    maxTimeoutSeconds?: number;
    customPaywallHtml?: string;
  };
};

// Networks
type Network =
  | "sepolia"
  | "mainnet"
  | "filecoin"
  | "filecoin-calibration"
  | "polygon"
  | "polygon-amoy"
  | "base"
  | "base-sepolia";
```

---

## Related Resources

* [🚀 Quick Start](../quick-start.md) - Get started in 10 minutes
* [📦 Core Package](core.md) - Core library for facilitators
* [📦 Next.js Package](next.md) - Next.js middleware
* [🌍 Network Guide](../guides/network-guide.md) - Choose the right network
* [💡 Use Cases](../guides/use-cases.md) - Real-world examples
