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
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

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

app.listen(4000);
```

**Why X402?**
- $0.01 is too small for credit cards (fees would be higher than payment)
- Users pay only for what they use
- No subscription required
- Instant confirmation

---

## 2. Subscriptions: Monthly Billing

**Best for:** SaaS platforms, storage services, membership sites

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.post('/subscribe', paymentMiddleware(
  merchantWallet,
  {
    'POST /subscribe': {
      price: '$9.99',
      network: 'filecoin-calibration',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
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

**Why X402?**
- Global payments without credit card processors
- Lower fees than traditional payment processors
- Instant settlement
- Blockchain-native users already have wallets

---

## 3. Storage Payments: Filecoin Deals

**Best for:** IPFS hosting, archival storage, data preservation

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$120.00',
      network: 'filecoin-calibration',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
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

**Why X402?**
- Native integration with Filecoin ecosystem
- USDFC token aligns with storage pricing
- 60-second settlement perfect for storage workflows
- Filecoin users already have FIL wallets

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
        network: 'sepolia',
        token: 'JPYC'
      }
    },
    { url: facilitatorUrl }
  );

  middleware(req, res, async () => {
    const translation = await translateText(req.body.text);
    res.json({ translation });
  });
});
```

---

## When to Use X402

**Good fit:**
- Micropayments under $10
- Pay-per-use APIs
- Blockchain-native applications
- Global audience
- Recurring billing

**Not ideal:**
- Free APIs
- Very high-value B2C payments (credit cards may be better UX)
- Traditional fiat-only businesses

---

## More Examples

See the [GitHub repository](https://github.com/Secured-Finance/x402/tree/main/examples) for complete working examples:

- **E-commerce checkout** - Shopping cart with dynamic pricing
- **AI image generation** - Pay per image generated
- **Video streaming** - Pay per video watched
- **Game items** - In-game purchases

---

## Next Steps

- **[Quick Start](../quick-start.md)** - Build your first paid API
- **[Middleware Docs](../packages/middleware.md)** - Complete API reference
- **[Network Guide](network-guide.md)** - Choose the right network
