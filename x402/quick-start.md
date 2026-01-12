---
description: Build your first paid API in 10 minutes
---

# Quick Start

Build a simple weather API that charges $0.01 per request using x402-exec.

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
npm init -y
npm install @secured-finance/x402-express express dotenv
npm install -D typescript @types/express @types/node tsx
```

**Hono (Edge/Workers)**
```bash
mkdir my-paid-api && cd my-paid-api
npm init -y
npm install @secured-finance/x402-hono @secured-finance/x402-core hono
npm install -D typescript @types/node tsx
```

---

## Step 2: Configure

Create `.env`:

```bash
MERCHANT_WALLET=0xYourWalletAddress
FACILITATOR_URL=https://facilitator.x402x.dev
```

The facilitator verifies signatures and settles payments on-chain via SettlementRouter. Use the public facilitator for testing.

---

## Step 3: Add Payment Middleware

### Express.js

Create `server.ts`:

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/x402-express';
import dotenv from 'dotenv';

dotenv.config();
const app = express();

app.get('/weather/:city', paymentMiddleware(
  process.env.MERCHANT_WALLET!,
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'base-sepolia'
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

### Hono (Edge/Workers)

Create `server.ts`:

```typescript
import { Hono } from 'hono';
import { paymentMiddleware } from '@secured-finance/x402-hono';

const app = new Hono();

app.use('/weather/:city',
  paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      price: '$0.01',
      network: 'base-sepolia'
    },
    { url: 'https://facilitator.x402x.dev' }
  )
);

app.get('/weather/:city', (c) => {
  const city = c.req.param('city');
  return c.json({
    city,
    temperature: 72,
    condition: 'sunny'
  });
});

export default app;
```

---

## Step 4: Run

```bash
# Express
npx tsx server.ts

# Hono
npx tsx server.ts
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
3. User signs payment in wallet (free, no gas)
4. Facilitator verifies signature
5. Facilitator settles on-chain via SettlementRouter (pays gas, earns 0.3% fee)
6. Hook executes (TransferHook transfers payment to merchant)
7. Middleware allows request through
8. API returns data

---

## Next Steps

* **[Live Demo](https://demo.x402x.dev)** - See working examples with revenue splits, NFT minting, and rewards
* **[Using the Facilitator](guides/using-facilitator.md)** - Learn more about the default facilitator
* **[Network Guide](guides/network-guide.md)** - Base and X-Layer are live on mainnet!
* **[Run Your Own Facilitator](guides/facilitator-guide.md)** - Earn fees (0.3%) on payments you process
* **[Use Cases](guides/use-cases.md)** - See more examples
* **[Package Docs](packages/README.md)** - Complete API reference for all x402x packages

---

Need help? [Join our Discord](https://discord.gg/securedfinance)
