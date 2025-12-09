---
description: Build your first paid API in 10 minutes
---

# Quick Start

Build a simple weather API that charges $0.01 per request using X402.

## Prerequisites

- Node.js 18+
- A wallet (MetaMask, Coinbase Wallet)
- Testnet tokens (see [Network Guide](guides/network-guide.md))

---

## Step 1: Install

Choose your framework:

**Express.js**
```bash
mkdir my-paid-api && cd my-paid-api
pnpm init
pnpm add @secured-finance/sf-x402-express express dotenv
pnpm add -D typescript @types/express @types/node tsx
```

**Next.js**
```bash
npx create-next-app@latest my-paid-api
cd my-paid-api
pnpm add @secured-finance/sf-x402-next
```

---

## Step 2: Configure

Create `.env`:

```bash
MERCHANT_WALLET=0xYourWalletAddress
FACILITATOR_URL=https://x402.org/facilitator
```

The facilitator verifies signatures and settles payments on-chain. Use Secured Finance's public facilitator for testing.

---

## Step 3: Add Payment Middleware

### Express.js

Create `server.ts`:

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/sf-x402-express';
import dotenv from 'dotenv';

dotenv.config();
const app = express();

app.get('/weather/:city', paymentMiddleware(
  process.env.MERCHANT_WALLET!,
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'sepolia',
      token: 'JPYC'
    }
  },
  { url: process.env.FACILITATOR_URL! }
), (req, res) => {
  res.json({
    city: req.params.city,
    temperature: 72,
    condition: 'sunny'
  });
});

app.listen(4000, () => {
  console.log('API running on http://localhost:4000');
});
```

### Next.js

Create `app/api/weather/[city]/route.ts`:

```typescript
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
    temperature: 72,
    condition: 'sunny'
  });
}
```

---

## Step 4: Run

```bash
# Express
pnpm tsx server.ts

# Next.js
pnpm dev
```

---

## Step 5: Test

### Without payment (returns 402):
```bash
curl http://localhost:4000/weather/tokyo
```

### With payment (in browser):
1. Open `http://localhost:4000/weather/tokyo`
2. Connect wallet (MetaMask)
3. Sign payment message (free, no gas)
4. View weather data

The middleware handles verification and settlement through the facilitator automatically.

---

## What Happened?

1. Browser requests `/weather/tokyo`
2. Middleware returns 402 with payment form
3. User signs payment in wallet
4. Facilitator verifies signature
5. Facilitator settles on-chain (pays gas)
6. Middleware allows request through
7. API returns data

---

## Next Steps

* **[Using the Facilitator](guides/using-facilitator.md)** - Learn more about the default facilitator
* **[Network Guide](guides/network-guide.md)** - Get testnet tokens and contract addresses
* **[Run Your Own Facilitator](guides/facilitator-guide.md)** - Earn fees on payments you process
* **[Use Cases](guides/use-cases.md)** - See more examples
* **[Package Docs](packages/README.md)** - Complete API reference

---

Need help? [Join our Discord](https://discord.gg/securedfinance)
