---
description: Payment middleware for Express.js and Next.js
---

# Payment Middleware

Drop-in middleware for Express.js and Next.js that adds payment requirements to your API routes.

---

## Installation

### Express.js
```bash
pnpm add @secured-finance/sf-x402-express express dotenv
```

### Next.js
```bash
pnpm add @secured-finance/sf-x402-next
```

---

## Quick Start

### Express.js

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

const app = express();

app.get('/weather/:city', paymentMiddleware(
  '0xYourWallet',
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

### Next.js (App Router)

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
  if (paymentResponse) return paymentResponse;

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

```typescript
function paymentMiddleware(
  payTo: Address,
  routes: RoutesConfig,
  facilitator?: FacilitatorConfig,
  paywall?: PaywallConfig
): Middleware
```

**Parameters:**

1. **`payTo`** (required) - Merchant wallet address where payments are sent
2. **`routes`** (required) - Route patterns and payment requirements
3. **`facilitator`** (optional) - Facilitator service configuration
4. **`paywall`** (optional) - Custom paywall HTML

---

## Configuration

### Route Configuration

```typescript
const routes = {
  'GET /api/data': {
    price: '$0.01',              // USD price
    network: 'sepolia',          // Network name
    token: 'JPYC',               // Token symbol (optional)
    config: {
      description: 'Premium data'
    }
  },
  'POST /api/store': {
    price: '$9.99',
    network: 'filecoin-calibration',
    token: 'USDFC'
  }
};
```

**Route Config Options:**
- `price` (string) - USD amount (e.g., `'$0.01'`, `'$9.99'`)
- `network` (string) - `'sepolia'` or `'filecoin-calibration'`
- `token` (string) - `'JPYC'`, `'USDC'`, or `'USDFC'`
- `config.description` (string) - Optional payment description

### Facilitator Configuration

```typescript
{
  url: 'https://x402.org/facilitator'  // Facilitator endpoint
}
```

Use Secured Finance's default facilitator for testing, or [run your own](../guides/facilitator-guide.md).

### Paywall Configuration

Customize the payment UI:

```typescript
{
  customPaywallHtml: `
    <html>
      <body>
        <h1>Premium Content</h1>
        <p>Pay $0.01 to access this content</p>
        <!-- X402 payment button injected automatically -->
      </body>
    </html>
  `
}
```

---

## Multiple Routes

Protect multiple endpoints with different prices:

### Express.js

```typescript
const routes = {
  'GET /api/weather/:city': {
    price: '$0.01',
    network: 'sepolia',
    token: 'JPYC'
  },
  'GET /api/premium-weather/:city': {
    price: '$0.10',
    network: 'sepolia',
    token: 'JPYC'
  },
  'POST /api/store-data': {
    price: '$9.99',
    network: 'filecoin-calibration',
    token: 'USDFC'
  }
};

app.use(paymentMiddleware(merchantWallet, routes, facilitator));

// Route handlers
app.get('/api/weather/:city', (req, res) => {
  res.json({ temp: 72 });
});

app.get('/api/premium-weather/:city', (req, res) => {
  res.json({ temp: 72, humidity: 45, wind: 10 });
});

app.post('/api/store-data', (req, res) => {
  res.json({ cid: 'bafy...' });
});
```

### Next.js

Create separate route handlers for each endpoint:

```typescript
// app/api/weather/[city]/route.ts
export async function GET(request: NextRequest, { params }) {
  // ... payment middleware
}

// app/api/premium-weather/[city]/route.ts
export async function GET(request: NextRequest, { params }) {
  // ... payment middleware with higher price
}
```

---

## Dynamic Pricing

Calculate prices based on request data:

### Express.js

```typescript
app.post('/translate', (req, res, next) => {
  const wordCount = req.body.text.split(' ').length;
  const price = `$${(wordCount * 0.001).toFixed(2)}`;

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /translate': {
        price,
        network: 'sepolia',
        token: 'JPYC'
      }
    },
    { url: facilitatorUrl }
  );

  middleware(req, res, next);
}, (req, res) => {
  res.json({ translation: translateText(req.body.text) });
});
```

### Next.js

```typescript
export async function POST(request: NextRequest) {
  const body = await request.json();
  const wordCount = body.text.split(' ').length;
  const price = `$${(wordCount * 0.001).toFixed(2)}`;

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /api/translate': { price, network: 'sepolia', token: 'JPYC' }
    },
    { url: facilitatorUrl }
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse;

  return Response.json({ translation: translateText(body.text) });
}
```

---

## Payment Flow

1. **User requests protected endpoint** without payment
2. **Middleware returns 402** with payment form
3. **User signs payment** in wallet (free, no gas)
4. **Middleware verifies** signature with facilitator
5. **Facilitator settles** payment on-chain
6. **Middleware allows request** through to handler
7. **API returns** protected content

All handled automatically by the middleware.

---

## Error Handling

The middleware handles common errors automatically:

- **Insufficient balance** - Returns 402 with error message
- **Invalid signature** - Returns 402 with error
- **Payment expired** - Returns 402 with error
- **Settlement failed** - Returns 502 with error

---

## TypeScript Types

Both packages include full TypeScript definitions:

```typescript
import type {
  RoutesConfig,
  FacilitatorConfig,
  PaywallConfig
} from '@secured-finance/sf-x402-express';
// or '@secured-finance/sf-x402-next'
```

---

## Next Steps

- **[Quick Start Guide](../quick-start.md)** - Complete tutorial
- **[Using the Facilitator](../guides/using-facilitator.md)** - Learn about facilitator nodes
- **[Network Guide](../guides/network-guide.md)** - Network details and contracts
- **[Core Package](core.md)** - Advanced usage and utilities
