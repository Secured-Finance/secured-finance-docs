---
description: Choose the right blockchain network for your X402 payments
---

# 🌍 Network Guide: Choosing the Right Blockchain

Different networks are optimized for different payment scenarios. Choose based on **transaction value**, **settlement speed**, and **use case type**.

---

## Quick Decision Guide

### Primary Tokens (JPYC & USDFC)

| If you need... | Use this network | Token | Finality |
|----------------|------------------|-------|----------|
| **Development & testing** | Sepolia | JPYC | ~2min |
| **Instant checkout** (e-commerce, games) | Polygon | JPYC | ~5s |
| **API micropayments** (< $1) | Sepolia/Polygon | JPYC | ~5s-2min |
| **Development (Filecoin)** | Filecoin Calibration | USDFC | ~60s |
| **Subscriptions** (monthly billing) | Filecoin | USDFC | ~60s |
| **Storage payments** (Filecoin deals) | Filecoin | USDFC | ~60s |

### Additional Options (USDC)

| If you need... | Use this network | Token | Finality |
|----------------|------------------|-------|----------|
| **Creator tips** (< $50) | Base | USDC | ~2s |
| **B2B invoices** ($10K+) | Ethereum | USDC | ~2min |

---

## 🇯🇵 Sepolia (JPYC) - Development

### Network Characteristics
- **Block Time**: ~12 seconds
- **Finality**: ~2 minutes
- **Gas Costs**: Free (testnet)
- **Token**: JPYC (Japanese Yen Coin - 18 decimals)
- **Contract**: `0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29`

### Best For: Development & Testing

Sepolia is the **recommended testnet** for developing X402 integrations with JPYC. Test your payment flows before deploying to mainnet.

---

### Use Case: Testing Weather API

**Perfect for**: Development, testing, CI/CD pipelines

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.get('/weather/:city', paymentMiddleware(
  merchantWallet,
  {
    'GET /weather/:city': {
      price: '$0.01',
      network: 'sepolia',     // Testnet for development
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), (req, res) => {
  res.json({ temp: 72, condition: 'sunny' });
});
```

**Why it works:**
- Free gas fees for testing
- Real payment flow simulation
- Same code works on mainnet (just change network)

---

### ❌ When NOT to Use Sepolia
- Production deployments
- Real payments (use Polygon or Ethereum mainnet)

---

## 🪙 Filecoin (USDFC)

### Network Characteristics
- **Block Time**: ~30 seconds
- **Finality**: ~60 seconds
- **Gas Costs**: Low
- **Token**: USDFC (USD for Filecoin Community)

### Best For: Long-Running Workflows

Filecoin's ~60-second finality is **perfect for use cases where the workflow duration far exceeds settlement time**. If your use case takes minutes, hours, or is recurring, Filecoin is ideal.

---

### Use Case 1: Monthly Subscription Billing

**Perfect for**: SaaS, storage platforms, membership services

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.use(paymentMiddleware(
  merchantWallet,
  {
    'POST /subscribe': {
      price: '$9.99',              // Monthly fee
      network: 'filecoin-mainnet',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
));
```

**Why it works:**
- User expects processing time for subscription setup
- 60-second settlement feels instant compared to monthly billing cycle
- Low gas fees keep costs down

**Real example:**
- User subscribes to 100GB decentralized storage
- Pays $9.99/month
- Payment confirms in 60 seconds
- Service activates immediately

---

### Use Case 2: Filecoin Storage Deal Payments

**Perfect for**: IPFS hosting, archival storage, data preservation

```typescript
app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$120.00',            // Annual storage cost
      network: 'filecoin-mainnet',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const cid = await storeToFilecoin(req.body.data);
  res.json({
    cid,
    dealId: 'f01234567',
    expiresAt: '2026-11-17'
  });
});
```

**Why it works:**
- Storage deals take 15-30 minutes to negotiate
- Payment settlement (60s) is negligible
- USDFC is native to Filecoin ecosystem

**Real example:**
- User uploads 500GB dataset for 1-year archival
- Pays $120 in USDFC
- Payment settles in 60 seconds
- Storage deal negotiation takes 20 minutes
- Data is sealed and stored

---

### Use Case 3: AI Model Training Payments

**Perfect for**: ML compute, GPU rentals, batch processing

```typescript
app.post('/train-model', paymentMiddleware(
  merchantWallet,
  {
    'POST /train-model': {
      price: '$50.00',             // Training job cost
      network: 'filecoin-mainnet',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const jobId = await queueTrainingJob(req.body.modelConfig);
  res.json({
    jobId,
    estimatedCompletion: '2 hours',
    status: 'queued'
  });
});
```

**Why it works:**
- Training jobs run for hours or days
- Payment settlement (60s) is instant relative to job duration
- Lower gas fees for high-value compute purchases

**Real example:**
- ML engineer trains vision model on 4xH100 GPUs
- Pays $50 for 2-hour job
- Payment settles in 60 seconds
- Training completes in 2 hours
- Model weights delivered

---

### Use Case 4: Recurring Automation (Cron Jobs)

**Perfect for**: Scheduled reports, data pipelines, automated workflows

```typescript
app.post('/schedule-report', paymentMiddleware(
  merchantWallet,
  {
    'POST /schedule-report': {
      price: '$5.00',              // Weekly report
      network: 'filecoin-mainnet',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const scheduleId = await scheduleWeeklyReport(req.body.config);
  res.json({
    scheduleId,
    nextRun: 'Monday 9:00 AM UTC'
  });
});
```

**Why it works:**
- Recurring workflows run on schedules (weekly, monthly)
- 60-second payment delay is acceptable for setup
- Cost-effective for recurring small payments

---

### ❌ When NOT to Use Filecoin
- Real-time checkout flows (users won't wait 60 seconds)
- Instant access APIs (pay-per-request weather data)
- Interactive applications (games, live feeds)
- High-frequency microtransactions (< 1 minute intervals)

---

## 🇯🇵 Polygon (JPYC)

### Network Characteristics
- **Block Time**: ~2 seconds
- **Finality**: ~5 seconds (practical)
- **Gas Costs**: Very low ($0.001-0.01)
- **Token**: JPYC (Japanese Yen Coin - JPY stablecoin)
- **Target Market**: Japanese consumers and businesses

### Best For: Instant Consumer Payments

Polygon's ~5-second finality **feels instant to users**, making it perfect for consumer-facing checkout flows and interactive applications.

---

### Use Case 1: E-Commerce Checkout

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
        network: 'polygon',         // Fast finality
        token: 'JPYC'               // Japanese Yen Coin
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

**Why it works:**
- Users expect instant feedback during checkout
- 5-second finality keeps cart abandonment low
- JPYC is familiar for Japanese market (¥500 = ~$3.50 USD)

**Real example:**
- Customer buys ¥5,000 ($35) of electronics
- Payment confirms in 5 seconds
- Order sent to fulfillment immediately
- Customer receives confirmation email
- Much lower abandonment vs. 60-second wait

---

### Use Case 2: In-App Purchases (Games)

**Perfect for**: Virtual goods, game currency, premium features

```typescript
app.post('/buy-coins', paymentMiddleware(
  merchantWallet,
  {
    'POST /buy-coins': {
      price: '$4.99',              // 500 gems
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

**Why it works:**
- Gamers expect instant gratification
- Waiting 60 seconds would break immersion
- 5-second confirmation maintains game flow

**Real example:**
- Player runs out of gems mid-game
- Pays ¥500 ($3.50) for 500 gems
- Payment confirms in 5 seconds
- Gems appear immediately
- Player continues without friction

---

### Use Case 3: Content Paywalls

**Perfect for**: News articles, videos, premium blogs

```typescript
app.get('/article/:id', paymentMiddleware(
  merchantWallet,
  {
    'GET /article/:id': {
      price: '$0.50',              // Per-article fee
      network: 'polygon',
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const article = await getArticle(req.params.id);
  res.json({
    title: article.title,
    content: article.fullContent // Full access
  });
});
```

**Why it works:**
- Readers won't wait 60 seconds for an article
- Instant access is critical for content consumption
- Low price point (¥75 = $0.50) suits per-article pricing

**Real example:**
- Reader wants premium article
- Pays ¥75 ($0.50)
- Payment confirms in 5 seconds
- Full article appears
- Reader continues browsing

---

### Use Case 4: API Micropayments

**Perfect for**: Pay-per-request APIs, high-frequency calls

```typescript
app.get('/weather/:city', paymentMiddleware(
  merchantWallet,
  {
    'GET /weather/:city': {
      price: '$0.01',              // 1 cent per request
      network: 'polygon',
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const weather = await fetchWeather(req.params.city);
  res.json(weather);
});
```

**Why it works:**
- Developers may make hundreds of test requests
- Fast settlement enables rapid iteration
- Low gas fees make micropayments viable

**Real example:**
- Developer tests weather API integration
- Makes 50 requests in 5 minutes
- Each costs ¥1.5 ($0.01)
- All payments confirm in ~5 seconds
- Total cost: ¥75 ($0.50) for testing

---

### ❌ When NOT to Use Polygon
- Large-value B2B settlements (use Ethereum for max security)
- Storage or compute payments (use Filecoin for better economics)
- Non-urgent workflows where cost > speed

---

## 🔷 Ethereum Mainnet (USDC)

### Network Characteristics
- **Block Time**: ~12 seconds
- **Finality**: ~2 minutes (strong)
- **Gas Costs**: High ($1-10 depending on congestion)
- **Token**: USDC (most liquid stablecoin)
- **Security**: Maximum decentralization

### Best For: High-Value B2B Settlements

Ethereum's **maximum security** justifies the 2-minute finality and higher gas fees for large-value transactions.

---

### Use Case 1: B2B Invoice Automation

**Perfect for**: Supplier payments, contractor invoices, procurement

```typescript
app.post('/pay-invoice', paymentMiddleware(
  merchantWallet,
  {
    'POST /pay-invoice': {
      price: '$50000.00',          // Large B2B payment
      network: 'ethereum',         // Maximum security
      token: 'USDC'
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

**Why it works:**
- For $50K+ payments, 2-minute finality is acceptable
- Ethereum's security guarantees justify higher gas fees
- Strong finality prevents disputes

**Real example:**
- Company pays quarterly vendor invoice
- $50,000 USDC payment
- Settles in 2 minutes on Ethereum
- Gas fee: ~$5 (0.01% of transaction)
- Auditable on-chain record

---

### Use Case 2: Enterprise API Licenses

**Perfect for**: Data feeds, analytics platforms, compliance tools

```typescript
app.post('/enterprise-license', paymentMiddleware(
  merchantWallet,
  {
    'POST /enterprise-license': {
      price: '$25000.00',          // Annual license
      network: 'ethereum',
      token: 'USDC'
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

**Why it works:**
- Enterprise sales cycles take weeks/months
- 2-minute payment confirmation is negligible
- Maximum security for sensitive access

---

### ❌ When NOT to Use Ethereum
- Small transactions < $10 (fees eat into value)
- High-frequency microtransactions
- Consumer-facing instant checkout (too slow)

---

## 🔵 Base (USDC)

### Network Characteristics
- **Block Time**: ~2 seconds
- **Finality**: ~2 seconds (L2 speed)
- **Gas Costs**: Very low ($0.001-0.01)
- **Token**: USDC (native to Base)
- **Integration**: Seamless Coinbase wallet support

### Best For: Coinbase Ecosystem & Creator Economy

Base offers **fast L2 speed with native Coinbase integration**, perfect for onchain apps and creator monetization.

---

### Use Case 1: Onchain App Stores

**Perfect for**: Smart contract templates, developer tools

```typescript
app.post('/buy-template', paymentMiddleware(
  merchantWallet,
  {
    'POST /buy-template': {
      price: '$29.99',
      network: 'base',
      token: 'USDC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const template = await purchaseContractTemplate(req.body.templateId);
  res.json({
    sourceCode: template.code,
    license: 'MIT'
  });
});
```

**Why it works:**
- Developers with Coinbase wallets get seamless checkout
- Fast L2 speed, low fees
- Instant code delivery

---

### Use Case 2: Creator Monetization

**Perfect for**: Tips, donations, supporter payments

```typescript
app.post('/tip-creator', paymentMiddleware(
  creatorWallet,
  {
    'POST /tip-creator': {
      price: '$5.00',
      network: 'base',
      token: 'USDC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  await recordTip(req.body.creatorId, 5.00);
  res.json({ message: 'Tip sent!' });
});
```

**Why it works:**
- Instant settlement feels immediate
- 99.8% of tip reaches creator (only 0.3% fee + minimal gas)
- Coinbase wallet users get native experience

---

## Network Comparison Table

### Primary Networks (JPYC & USDFC)

| Network | Token | Decimals | Finality | Gas Cost | Best For |
|---------|-------|----------|----------|----------|----------|
| **Sepolia** | JPYC | 18 | ~2min | Free | Development, testing |
| **Polygon** | JPYC | 18 | ~5s | Very Low | E-commerce, games, content, APIs |
| **Ethereum** | JPYC | 18 | ~2min | Medium | Production JPYC payments |
| **Filecoin Calibration** | USDFC | 18 | ~60s | Free | Development, testing |
| **Filecoin** | USDFC | 18 | ~60s | Low | Subscriptions, storage, AI |

### Additional Networks (USDC)

| Network | Token | Decimals | Finality | Gas Cost | Best For |
|---------|-------|----------|----------|----------|----------|
| **Base** | USDC | 6 | ~2s | Very Low | Onchain apps, creator tips |
| **Ethereum** | USDC | 6 | ~2min | High | B2B invoices, enterprise |

---

## Multi-Network Support

You can let users choose their preferred network:

```typescript
app.post('/flexible-payment', (req, res, next) => {
  const { preferredNetwork } = req.body;

  const networkConfig = {
    'polygon': { token: 'JPYC', finality: '~5s' },
    'filecoin-mainnet': { token: 'USDFC', finality: '~60s' },
    'ethereum': { token: 'USDC', finality: '~2min' },
    'base': { token: 'USDC', finality: '~2s' }
  };

  const middleware = paymentMiddleware(
    merchantWallet,
    {
      'POST /flexible-payment': {
        price: '$10.00',
        network: preferredNetwork,
        token: networkConfig[preferredNetwork].token
      }
    },
    { url: facilitatorUrl }
  );

  middleware(req, res, next);
});
```

---

## Testnet Resources

Practice on testnets before going live:

### Primary Testnets (JPYC & USDFC)

| Testnet | Token | Faucet | Explorer | Token Contract |
|---------|-------|--------|----------|----------------|
| **Sepolia** | JPYC | [Sepolia Faucet](https://sepoliafaucet.com/) | [Etherscan](https://sepolia.etherscan.io/) | `0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29` |
| **Filecoin Calibration** | USDFC | [Calibration Faucet](https://faucet.calibnet.chainsafe-fil.io/) | [Filfox](https://calibration.filfox.info/) | `0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0` |

### Additional Testnets (USDC)

| Testnet | Token | Faucet | Explorer |
|---------|-------|--------|----------|
| **Polygon Amoy** | USDC | [Polygon Faucet](https://faucet.polygon.technology/) | [PolygonScan](https://amoy.polygonscan.com/) |
| **Base Sepolia** | USDC | [Base Faucet](https://www.coinbase.com/faucets/base-ethereum-goerli-faucet) | [BaseScan](https://sepolia.basescan.org/) |

---

## Related Resources

* [Overview](../overview.md) - What is X402?
* [Quick Start](../quick-start.md) - Build your first paid API
* [Use Cases](use-cases.md) - Real-world examples
* [Facilitator Guide](facilitator-guide.md) - Deploy and earn fees
* [Package Documentation](../packages/README.md) - API reference

---

**Ready to integrate?** → [Quick Start Guide](../quick-start.md)
