---
description: Real-world X402 implementation examples
---

# Use Cases

Real-world examples showing how to use X402 for different payment scenarios.

---

## 1. Micropayments: Pay-Per-Request API

**Best for:** Weather APIs, data feeds, AI services, translation

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/x402-express';

const app = express();

app.get('/weather/:city', paymentMiddleware(
  process.env.MERCHANT_WALLET!,
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'base-sepolia'
    }
  },
  { url: 'https://facilitator.x402x.dev' }
), (req, res) => {
  res.json({
    city: req.params.city,
    temperature: 72,
    condition: 'sunny'
  });
});

app.listen(4000);
```

**Why x402x?**
- $0.01 is too small for credit cards (fees would be higher than payment)
- Users pay only for what they use (no gas fees!)
- No subscription required
- Instant confirmation via facilitator
- Programmable settlement through hooks

---

## 2. Subscriptions: Monthly Billing

**Best for:** SaaS platforms, storage services, membership sites

```typescript
import { paymentMiddleware } from '@secured-finance/x402-express';

app.post('/subscribe', paymentMiddleware(
  merchantWallet,
  {
    'POST /subscribe': {
      price: '$9.99',
      network: 'base'
    }
  },
  { url: 'https://facilitator.x402x.dev' }
), async (req, res) => {
  // Activate subscription
  const userId = req.body.userId;
  await activateSubscription(userId, 30); // 30 days

  res.json({
    subscriptionId: generateId(),
    expiresAt: addDays(new Date(), 30),
    status: 'active'
  });
});
```

**Why x402x?**
- Global payments without credit card processors
- Lower fees than traditional payment processors (0.3% facilitator fee)
- Instant settlement via SettlementRouter
- Blockchain-native users already have wallets
- No gas fees for users

---

## 3. Storage Payments: Filecoin Deals

**Best for:** IPFS hosting, archival storage, data preservation

```typescript
import { paymentMiddleware } from '@secured-finance/x402-express';

app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$120.00',
      network: 'filecoin-calibration'
    }
  },
  { url: 'https://facilitator.x402x.dev' }
), async (req, res) => {
  // Store data to Filecoin
  const cid = await storeToFilecoin(req.body.data);

  res.json({
    cid,
    dealId: 'f01234567',
    expiresAt: addYears(new Date(), 1)
  });
});
```

**Why x402x?**
- Native integration with Filecoin ecosystem
- USDFC token aligns with storage pricing
- 60-second settlement perfect for storage workflows
- Filecoin users already have FIL wallets
- Programmable hooks can automate deal setup

---

## Dynamic Pricing Example

Calculate prices based on usage:

```typescript
app.post('/translate', async (req, res) => {
  const wordCount = req.body.text.split(' ').length;
  const pricePerWord = 0.001;
  const price = `$${Math.max(0.01, wordCount * pricePerWord).toFixed(2)}`;

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /translate': {
        price,
        network: 'base-sepolia',
        token: 'USDC'
      }
    },
    { url: 'https://facilitator.x402x.dev' }
  );

  middleware(req, res, async () => {
    const translation = await translateText(req.body.text);
    res.json({ translation });
  });
});
```

---

## When to Use x402x

**Good fit:**
- Micropayments under $10
- Pay-per-use APIs and services
- Blockchain-native applications
- Global audience (no geographic restrictions)
- Recurring billing and subscriptions
- Programmable payments (revenue splits, NFTs, rewards)

**Not ideal:**
- Free APIs (no payment needed)
- Very high-value B2C payments (credit cards may offer better UX)
- Traditional fiat-only businesses
- Applications where users don't have crypto wallets

---

## More Examples

### Live Demo
Visit https://demo.x402x.dev to see working examples:
- **Referral revenue split** - Automatic payment splitting via TransferHook
- **NFT minting** - Atomic NFT mint with payment via NFTMintHook
- **Loyalty rewards** - Automatic points distribution via RewardHook

### GitHub Examples
See the [x402-exec repository](https://github.com/Secured-Finance/x402-exec/tree/main/examples/showcase) for complete source code:

- **Showcase application** - Full-stack demo with React + TypeScript
- **Custom hooks** - Example hook implementations
- **Facilitator** - Production-ready facilitator service

---

## Next Steps

- **[Quick Start](../quick-start.md)** - Build your first paid API
- **[Express Middleware](../packages/express.md)** - Complete API reference
- **[Network Guide](network-guide.md)** - Choose the right network
