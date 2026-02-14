---
description: Use Secured Finance's facilitator node to handle payment verification and settlement
---

# Using the Facilitator

The x402x payment system requires a **facilitator node** to verify signatures and settle payments on-chain through the SettlementRouter. This guide explains how to use the default facilitator.

## What is a Facilitator?

A facilitator is a service that:
1. **Verifies** payment signatures from users (off-chain)
2. **Settles** payments on-chain via SettlementRouter (pays gas fees)
3. **Earns** fees (0.3%, min $0.01) on payments they process
4. **Claims** accumulated fees from SettlementRouter anytime

Think of it as a payment processor that handles the blockchain complexity and gas fees for you.

---

## Using the Default Facilitator

Secured Finance operates a public facilitator at `https://facilitator.x402x.dev` for testing and development.

### Express.js Integration

```typescript
import { paymentMiddleware } from '@secured-finance/x402-express';

app.get('/api/data', paymentMiddleware(
  '0xYourMerchantWallet',
  {
    'GET /api/data': {
      price: '$0.01',
      network: 'base-sepolia'
    }
  },
  { url: 'https://facilitator.x402x.dev' }  // Facilitator URL
), (req, res) => {
  res.json({ data: 'premium content' });
});
```

### Hono Integration

```typescript
import { Hono } from 'hono';
import { paymentMiddleware } from '@secured-finance/x402-hono';

const app = new Hono();

app.use('/api/data',
  paymentMiddleware(
    '0xYourMerchantWallet',
    {
      price: '$0.01',
      network: 'base-sepolia'
    },
    { url: 'https://facilitator.x402x.dev' }
  )
);

app.get('/api/data', (c) => {
  return c.json({ data: 'premium content' });
});
```

---

## How the Middleware Works

When a user makes a request to your protected API:

**1. First request (no payment):**
- Middleware checks for `X-PAYMENT` header
- Not found → returns HTTP 402 with payment form
- User sees paywall with "Connect Wallet" button

**2. User signs payment:**
- User clicks "Pay"
- Wallet prompts for signature (free, no gas)
- Browser retries request with `X-PAYMENT` header

**3. Middleware verification:**
- Middleware sends signature to facilitator's `/verify` endpoint
- Facilitator validates signature, amount, recipient, deadline
- Returns verification result

**4. Settlement:**
- Facilitator's `/settle` endpoint is called
- Facilitator calculates fee (0.3%, min $0.01)
- Facilitator submits transaction on-chain via SettlementRouter's `settleAndExecute()`:
  - User's signed payment authorization is executed
  - Payment flows through SettlementRouter
  - Hook is executed (e.g., TransferHook transfers to merchant)
  - Facilitator's fee accumulates in `pendingFees[facilitatorAddress][token]`
  - Merchant receives payment

**5. Response:**
- Middleware allows request through to your handler
- Your API returns the protected content

All of this happens automatically—you just add the middleware!

---

## Configuration Options

### Basic Configuration

```typescript
paymentMiddleware(
  merchantWallet,
  routes,
  { url: 'https://facilitator.x402x.dev' }
)
```

### Advanced Configuration

```typescript
paymentMiddleware(
  merchantWallet,
  routes,
  {
    url: 'https://facilitator.x402x.dev',
    timeout: 30000,              // Request timeout (ms)
  }
)
```

---

## Multiple Networks

The middleware and facilitator support multiple networks. Simply specify the network in your configuration:

```typescript
// Express.js
const routes = {
  'GET /base-data': {
    price: '$0.01',
    network: 'base-sepolia',
    token: 'USDC'
  },
  'GET /xlayer-data': {
    price: '$0.05',
    network: 'xlayer-testnet',
    token: 'USDC'
  },
  'GET /filecoin-data': {
    price: '$9.99',
    network: 'filecoin-calibration',
    token: 'USDFC'
  }
};
```

The facilitator automatically handles verification and settlement on the appropriate network via the deployed SettlementRouter.

---

## When to Use the Default Facilitator

**Good for:**
- Development and testing
- Quick prototypes
- Small projects

**Not recommended for:**
- Production applications
- High-volume APIs
- Mission-critical services

For production, [run your own facilitator](facilitator-guide.md) to:
- Control uptime and performance
- Earn fees on payments you process
- Avoid dependency on third-party services

---

## Troubleshooting

### "Facilitator connection failed"

Check that the facilitator URL is correct:
```typescript
{ url: 'https://facilitator.x402x.dev' }
```

### "Payment verification failed"

Ensure:
- User has sufficient token balance
- Payment signature is valid
- Transaction deadline hasn't expired

### "Settlement timeout"

The facilitator may be experiencing high load or network congestion. Try:
- Increasing timeout in configuration
- Using a custom RPC provider
- Running your own facilitator

---

## Next Steps

- **[Run Your Own Facilitator](facilitator-guide.md)** - Deploy your own node
- **[Network Guide](network-guide.md)** - Learn about supported networks
- **[Package Docs](../packages/README.md)** - Complete API reference
