---
description: Real-world X402 implementation examples and use cases
---

# 💡 Use Cases

Real-world examples showing how to implement X402 for different payment scenarios. Each example includes complete code, rationale, and expected user experience.

---

## When to Use X402

### ✅ Perfect For:
- **Micropayments** - Payments under $10
- **Pay-per-use APIs** - Weather, AI, data feeds
- **Content paywalls** - Premium articles, videos
- **Subscription billing** - Monthly/weekly recurring
- **In-app purchases** - Game items, virtual goods
- **Storage payments** - Filecoin storage deals
- **B2B automation** - Invoices, API licensing

### ❌ Not Ideal For:
- **Free APIs** - No payment needed
- **Very high-value B2C** - Credit cards may offer better UX
- **Traditional banks** - Require fiat on/off ramps
- **Non-EIP-3009 tokens** - X402 requires transferWithAuthorization

---

## Micropayments

### Use Case: Pay-Per-Request Weather API

**Perfect for**: API services, data feeds, translation services

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

const app = express();

app.get('/weather/:city', paymentMiddleware(
  process.env.MERCHANT_WALLET!,
  {
    'GET /weather/:city': {
      price: '$0.01',      // 1 cent per request
      network: 'polygon',   // Fast finality (~5s)
      token: 'JPYC'        // Japanese Yen Coin
    }
  },
  { url: process.env.FACILITATOR_URL! }
), (req, res) => {
  res.json({
    city: req.params.city,
    temperature: 72,
    condition: 'sunny',
    humidity: 45
  });
});
```

**Why It Works:**
- Polygon's ~5-second finality feels instant
- $0.01 price point is too small for credit cards
- No gas fees for users enables true micropayments
- Pay-per-use is more flexible than subscriptions

**Real-World Scenario:**
- Developer makes 50 test requests in 5 minutes
- Each costs ¥1.5 ($0.01)
- All payments confirm in ~5 seconds
- Total cost: ¥75 ($0.50) for testing

---

### Use Case: Content Paywall

**Perfect for**: News sites, premium blogs, videos

```typescript
app.get('/article/:id', paymentMiddleware(
  merchantWallet,
  {
    'GET /article/:id': {
      price: '$0.50',
      network: 'polygon',
      token: 'JPYC',
      config: {
        description: 'Premium article access'
      }
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const article = await getArticle(req.params.id);
  res.json({
    title: article.title,
    content: article.fullContent
  });
});
```

**Why It Works:**
- Readers won't wait 60 seconds for an article
- Instant access is critical for content consumption
- Low price point (¥75 = $0.50) suits per-article pricing
- Better than subscription for casual readers

**Real-World Scenario:**
- Reader wants premium article
- Pays ¥75 ($0.50)
- Payment confirms in 5 seconds
- Full article appears
- Reader continues browsing

---

## Subscriptions & Storage

### Use Case: Monthly SaaS Subscription

**Perfect for**: SaaS platforms, membership services, storage

```typescript
app.post('/subscribe', paymentMiddleware(
  merchantWallet,
  {
    'POST /subscribe': {
      price: '$9.99',
      network: 'filecoin',  // 60s finality is fine for subscription
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const subscription = await createSubscription(req.body.userId);
  res.json({
    subscriptionId: subscription.id,
    storageLimit: '100GB',
    expiresAt: '2025-12-17',
    status: 'active'
  });
});
```

**Why It Works:**
- User expects processing time for subscription setup
- 60-second settlement feels instant compared to monthly billing cycle
- Lower gas fees on Filecoin keep costs down
- USDFC is native to Filecoin ecosystem

**Real-World Scenario:**
- User subscribes to 100GB decentralized storage
- Pays $9.99/month
- Payment confirms in 60 seconds
- Service activates immediately
- Renewal each month

---

### Use Case: Filecoin Storage Deal Payment

**Perfect for**: IPFS hosting, archival storage, data preservation

```typescript
app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$120.00',    // Annual storage cost
      network: 'filecoin',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const cid = await storeToFilecoin(req.body.data);
  res.json({
    cid,
    dealId: 'f01234567',
    expiresAt: '2026-11-17',
    size: '500GB'
  });
});
```

**Why It Works:**
- Storage deals take 15-30 minutes to negotiate
- Payment settlement (60s) is negligible
- USDFC is native to Filecoin ecosystem
- Perfect for long-term archival

**Real-World Scenario:**
- User uploads 500GB dataset for 1-year archival
- Pays $120 in USDFC
- Payment settles in 60 seconds
- Storage deal negotiation takes 20 minutes
- Data is sealed and stored

---

## Commerce

### Use Case: E-Commerce Checkout

**Perfect for**: Online stores, marketplaces, digital goods

```typescript
app.post('/checkout', (req, res, next) => {
  const { items } = req.body;
  const subtotal = calculateCartTotal(items);

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /checkout': {
        price: `$${subtotal.toFixed(2)}`,
        network: 'polygon',
        token: 'JPYC'
      }
    },
    { url: facilitatorUrl }
  );

  middleware(req, res, next);
}, (req, res) => {
  res.json({
    orderId: generateOrderId(),
    status: 'confirmed',
    estimatedDelivery: '3-5 business days'
  });
});
```

**Why It Works:**
- Users expect instant feedback during checkout
- 5-second finality keeps cart abandonment low
- Dynamic pricing based on cart contents
- JPYC is familiar for Japanese market

**Real-World Scenario:**
- Customer buys ¥5,000 ($35) of electronics
- Payment confirms in 5 seconds
- Order sent to fulfillment immediately
- Customer receives confirmation email
- Much lower abandonment vs. 60-second wait

---

### Use Case: In-App Purchases (Games)

**Perfect for**: Virtual goods, game currency, premium features

```typescript
app.post('/buy-coins', paymentMiddleware(
  merchantWallet,
  {
    'POST /buy-coins': {
      price: '$4.99',      // 500 gems
      network: 'polygon',
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  await creditUserAccount(req.user.id, 500);
  res.json({
    balance: 500,
    message: 'Gems added to your account!'
  });
});
```

**Why It Works:**
- Gamers expect instant gratification
- Waiting 60 seconds would break immersion
- 5-second confirmation maintains game flow
- Micropayments enable flexible pricing

**Real-World Scenario:**
- Player runs out of gems mid-game
- Pays ¥500 ($3.50) for 500 gems
- Payment confirms in 5 seconds
- Gems appear immediately
- Player continues without friction

---

## Enterprise

### Use Case: B2B Invoice Automation

**Perfect for**: Supplier payments, contractor invoices, procurement

```typescript
app.post('/pay-invoice', paymentMiddleware(
  merchantWallet,
  {
    'POST /pay-invoice': {
      price: '$50000.00',  // Large B2B payment
      network: 'mainnet',  // Maximum security
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const invoice = await markInvoicePaid(req.body.invoiceId);
  res.json({
    invoiceId: invoice.id,
    paidAt: new Date(),
    txHash: invoice.txHash
  });
});
```

**Why It Works:**
- For $50K+ payments, 2-minute finality is acceptable
- Ethereum's security guarantees justify higher gas fees
- Strong finality prevents disputes
- Auditable on-chain record

**Real-World Scenario:**
- Company pays quarterly vendor invoice
- $50,000 JPYC payment
- Settles in 2 minutes on Ethereum
- Gas fee: ~$5 (0.01% of transaction)
- Auditable on-chain record

---

### Use Case: API Licensing

**Perfect for**: Data feeds, analytics platforms, compliance tools

```typescript
app.post('/enterprise-license', paymentMiddleware(
  merchantWallet,
  {
    'POST /enterprise-license': {
      price: '$25000.00',  // Annual license
      network: 'mainnet',
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const apiKey = await provisionEnterpriseKey(req.body.organizationId);
  res.json({
    apiKey,
    rateLimit: 'unlimited',
    expiresAt: '2026-11-17',
    supportTier: 'enterprise'
  });
});
```

**Why It Works:**
- Enterprise sales cycles take weeks/months
- 2-minute payment confirmation is negligible
- Maximum security for sensitive access
- Transparent pricing and settlement

---

## AI & Compute

### Use Case: AI Model Training Payments

**Perfect for**: ML compute, GPU rentals, batch processing

```typescript
app.post('/train-model', paymentMiddleware(
  merchantWallet,
  {
    'POST /train-model': {
      price: '$50.00',     // Training job cost
      network: 'filecoin',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const jobId = await queueTrainingJob(req.body.modelConfig);
  res.json({
    jobId,
    estimatedCompletion: '2 hours',
    status: 'queued',
    gpus: '4xH100'
  });
});
```

**Why It Works:**
- Training jobs run for hours or days
- Payment settlement (60s) is instant relative to job duration
- Lower gas fees for high-value compute purchases
- Pay-per-job is more flexible than subscriptions

**Real-World Scenario:**
- ML engineer trains vision model on 4xH100 GPUs
- Pays $50 for 2-hour job
- Payment settles in 60 seconds
- Training completes in 2 hours
- Model weights delivered

---

### Use Case: Recurring Automation (Cron Jobs)

**Perfect for**: Scheduled reports, data pipelines, automated workflows

```typescript
app.post('/schedule-report', paymentMiddleware(
  merchantWallet,
  {
    'POST /schedule-report': {
      price: '$5.00',      // Weekly report
      network: 'filecoin',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const scheduleId = await scheduleWeeklyReport(req.body.config);
  res.json({
    scheduleId,
    nextRun: 'Monday 9:00 AM UTC',
    frequency: 'weekly'
  });
});
```

**Why It Works:**
- Recurring workflows run on schedules (weekly, monthly)
- 60-second payment delay is acceptable for setup
- Cost-effective for recurring small payments
- Automated billing without subscriptions

---

## Dynamic Pricing Examples

### Use Case: Translation Service (Pay-Per-Word)

```typescript
app.post('/translate', (req, res, next) => {
  const wordCount = req.body.text.split(' ').length;
  const pricePerWord = 0.001;
  const total = Math.max(0.01, wordCount * pricePerWord);

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /translate': {
        price: `$${total.toFixed(2)}`,
        network: 'polygon',
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

**Why It Works:**
- Fair pricing based on actual work
- Instant settlement enables rapid iteration
- Users only pay for what they use

---

## Network Selection Guide

| Use Case | Recommended Network | Token | Finality | Why |
|----------|---------------------|-------|----------|-----|
| **API micropayments** | Polygon | JPYC | ~5s | Instant for users |
| **Content paywalls** | Polygon | JPYC | ~5s | Fast access critical |
| **E-commerce checkout** | Polygon | JPYC | ~5s | Low cart abandonment |
| **Games (in-app)** | Polygon | JPYC | ~5s | Instant gratification |
| **Monthly subscriptions** | Filecoin | USDFC | ~60s | Setup time acceptable |
| **Storage payments** | Filecoin | USDFC | ~60s | Deal time >> payment time |
| **AI/ML compute** | Filecoin | USDFC | ~60s | Job time >> payment time |
| **B2B invoices ($10K+)** | Ethereum | JPYC | ~2min | Max security justified |
| **Enterprise licensing** | Ethereum | JPYC | ~2min | High-value transactions |

**See [Network Guide](network-guide.md) for detailed comparison →**

---

## Related Resources

* [📢 What is X402?](../overview.md) - Protocol overview
* [🚀 Quick Start](../quick-start.md) - Get started in 10 minutes
* [🌍 Network Guide](network-guide.md) - Choose the right network
* [📦 Express Package](../packages/express.md) - Express middleware docs
* [📦 Next.js Package](../packages/next.md) - Next.js middleware docs
* [🏦 Facilitator Guide](facilitator-guide.md) - Build your own facilitator

---

**Need inspiration?** Join our [Discord](https://discord.gg/securedfinance) to see what others are building with X402!
