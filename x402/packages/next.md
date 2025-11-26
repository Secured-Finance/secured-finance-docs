---
description: Next.js middleware for X402 payments
---

# Next.js Middleware (@secured-finance/sf-x402-next)

Next.js middleware for payment-gated API routes and server actions. Works with both App Router and Pages Router.

---

## Installation

```bash
pnpm add @secured-finance/sf-x402-next
```

---

## Quick Example (App Router)

```typescript
// app/api/weather/[city]/route.ts
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function GET(
  request: NextRequest,
  { params }: { params: { city: string } }
) {
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
  if (paymentResponse) return paymentResponse; // 402 if unpaid

  return Response.json({
    city: params.city,
    temp: 72,
    condition: 'sunny'
  });
}
```

---

## API Reference

### `paymentMiddleware()`

Create payment middleware for Next.js applications.

```typescript
function paymentMiddleware(
  payTo: Address | SolanaAddress,
  routes: RoutesConfig,
  facilitator?: FacilitatorConfig,
  paywall?: PaywallConfig
): NextMiddleware
```

**Parameters:**
- `payTo` - Merchant wallet address
- `routes` - Route patterns and payment requirements
- `facilitator` - Facilitator service configuration (optional)
- `paywall` - Paywall customization (optional)

---

## App Router Examples

### Basic Example (JPYC on Sepolia)

```typescript
// app/api/weather/[city]/route.ts
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function GET(
  request: NextRequest,
  { params }: { params: { city: string } }
) {
  const middleware = paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      'GET /api/weather/:city': {
        price: '$0.01',
        network: 'sepolia',
        token: 'JPYC',
        config: {
          description: 'Premium weather data'
        }
      }
    },
    { url: process.env.FACILITATOR_URL! }
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse;

  return Response.json({
    city: params.city,
    temperature: 72,
    condition: 'sunny',
    humidity: 45,
    wind: '10 mph'
  });
}
```

---

### USDFC Example (Filecoin Calibration)

```typescript
// app/api/store/route.ts
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function POST(request: NextRequest) {
  const middleware = paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      'POST /api/store': {
        price: '$9.99',
        network: 'filecoin-calibration',
        token: 'USDFC',
        config: {
          description: 'Storage subscription'
        }
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
    status: 'stored',
    expiresAt: '2026-11-17'
  });
}
```

---

### Dynamic Pricing Example

```typescript
// app/api/translate/route.ts
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function POST(request: NextRequest) {
  const body = await request.json();
  const wordCount = body.text.split(' ').length;
  const price = Math.max(0.01, wordCount * 0.001);

  const middleware = paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      'POST /api/translate': {
        price: `$${price.toFixed(2)}`,
        network: 'sepolia',
        token: 'JPYC'
      }
    },
    { url: process.env.FACILITATOR_URL! }
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse;

  return Response.json({
    translation: translateText(body.text)
  });
}
```

---

## Coinbase Onramp Setup

Enable Coinbase Onramp for easy wallet funding.

### Step 1: Add Session Token Endpoint

```typescript
// app/api/x402/session-token/route.ts
export { POST } from '@secured-finance/sf-x402-next';
```

### Step 2: Set Environment Variables

```bash
# .env.local
CDP_API_KEY_ID=your_key_id
CDP_API_KEY_SECRET=your_key_secret
```

### Step 3: Configure Paywall

```typescript
const paywall = {
  sessionTokenEndpoint: "/api/x402/session-token",
  cdpClientKey: process.env.NEXT_PUBLIC_CDP_CLIENT_KEY,
  appName: "My App"
};

const middleware = paymentMiddleware(
  merchantWallet,
  routes,
  { url: facilitatorUrl },
  paywall  // Add paywall config
);
```

---

## Configuration Options

### Route Config

```typescript
type RouteConfig = {
  // Required
  price: Money | ERC20TokenAmount;  // "$0.01" or token amount
  network: Network;                  // "sepolia", "polygon", "filecoin", etc.

  // Optional
  token?: string;                    // "USDC", "JPYC", "USDFC"
  config?: {
    description?: string;            // Payment description
    mimeType?: string;               // MIME type
    maxTimeoutSeconds?: number;      // Payment timeout (default: 60s)
    outputSchema?: object;           // JSON schema
    customPaywallHtml?: string;      // Custom HTML
    resource?: string;               // Resource URL
  }
};
```

### Paywall Config

```typescript
type PaywallConfig = {
  cdpClientKey?: string;           // Coinbase Developer Platform key
  appName?: string;                // App name for wallet modal
  appLogo?: string;                // Logo URL
  sessionTokenEndpoint?: string;   // Session token endpoint
  customPaywallHtml?: string;      // Custom paywall HTML
};
```

---

## Environment Setup

Create `.env.local`:

```bash
# Required
MERCHANT_WALLET=0xYourWalletAddress
FACILITATOR_URL=https://x402.org/facilitator

# Optional: Coinbase Onramp
CDP_API_KEY_ID=your_key_id
CDP_API_KEY_SECRET=your_key_secret
NEXT_PUBLIC_CDP_CLIENT_KEY=your_client_key

# Optional: Custom RPC
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_API_KEY
```

---

## Error Responses

When payment is required, the middleware returns a 402 status:

```json
{
  "x402Version": 1,
  "error": "payment_required",
  "accepts": [
    {
      "scheme": "exact",
      "network": "sepolia",
      "maxAmountRequired": "10000000000000000",
      "resource": "/api/weather/tokyo",
      "description": "Premium weather data",
      "payTo": "0x...",
      "asset": "0x...",
      "extra": {
        "symbol": "JPYC",
        "decimals": 18
      }
    }
  ]
}
```

**Common Errors:**

| Error | HTTP Status | Meaning |
|-------|-------------|---------|
| `payment_required` | 402 | No payment provided |
| `nonce_already_used` | 402 | Payment already settled |
| `invalid_signature` | 400 | Signature verification failed |
| `insufficient_balance` | 400 | User has insufficient funds |

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
} from '@secured-finance/sf-x402-next';

// Price formats
type Money = `$${number}`;

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

## Troubleshooting

### Issue: "Module not found" in Edge Runtime

**Cause:** Some dependencies may not be compatible with Edge runtime

**Solution:** Use Node.js runtime in route handler:

```typescript
export const runtime = 'nodejs'; // Add this line
export async function GET(request: NextRequest) {
  // ...
}
```

---

### Issue: Environment variables not defined

**Cause:** Next.js doesn't load `.env.local` in all contexts

**Solution:** Use `process.env` and ensure variables are defined:

```typescript
const merchantWallet = process.env.MERCHANT_WALLET;
if (!merchantWallet) {
  throw new Error('MERCHANT_WALLET not configured');
}
```

---

## Related Resources

* [🚀 Quick Start](../quick-start.md) - Get started in 10 minutes
* [📦 Core Package](core.md) - Core library
* [📦 Express Package](express.md) - Express middleware
* [🌍 Network Guide](../guides/network-guide.md) - Choose the right network
* [💡 Use Cases](../guides/use-cases.md) - Real-world examples
