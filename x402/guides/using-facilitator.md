---
description: Use Secured Finance's facilitator node to handle payment verification and settlement
---

# Using the Facilitator

The X402 payment middleware requires a **facilitator node** to verify signatures and settle payments on-chain. This guide explains how to use Secured Finance's default facilitator.

## What is a Facilitator?

A facilitator is a service that:
1. **Verifies** payment signatures from users
2. **Settles** payments on-chain (pays gas fees)
3. **Earns** fees on payments they process (can claim anytime)

Think of it as a payment processor that handles the blockchain complexity for you.

---

## Using the Default Facilitator

Secured Finance operates a public facilitator at `https://x402.org/facilitator` for testing and development.

### Express.js Integration

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.get('/api/data', paymentMiddleware(
  '0xYourMerchantWallet',
  {
    'GET /api/data': {
      price: '$0.01',
      network: 'sepolia',
      token: 'JPYC'
    }
  },
  { url: 'https://x402.org/facilitator' }  // Facilitator URL
), (req, res) => {
  res.json({ data: 'premium content' });
});
```

### Next.js Integration

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

export async function GET(request: NextRequest) {
  const middleware = paymentMiddleware(
    process.env.MERCHANT_WALLET!,
    {
      'GET /api/data': {
        price: '$0.01',
        network: 'sepolia',
        token: 'JPYC'
      }
    },
    { url: 'https://x402.org/facilitator' }  // Facilitator URL
  );

  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse;

  return Response.json({ data: 'premium content' });
}
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
- Facilitator calculates fee (0.3%, min $0.01) using `calculateFee()`
- Facilitator submits transaction on-chain via `settleAndExecute()`:
  - User's total amount transferred to SettlementRouter
  - Facilitator's fee accumulates in `pendingFees` mapping
  - Merchant receives merchantAmount via TransferHook

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
  { url: 'https://x402.org/facilitator' }
)
```

### Advanced Configuration

```typescript
paymentMiddleware(
  merchantWallet,
  routes,
  {
    url: 'https://x402.org/facilitator',
    timeout: 30000,              // Request timeout (ms)
    retries: 3                    // Retry failed requests
  }
)
```

---

## Multiple Networks

The middleware and facilitator support multiple networks. Simply specify the network in your route configuration:

```typescript
const routes = {
  'GET /sepolia-data': {
    price: '$0.01',
    network: 'sepolia',
    token: 'JPYC'
  },
  'GET /filecoin-data': {
    price: '$9.99',
    network: 'filecoin-calibration',
    token: 'USDFC'
  }
};
```

The facilitator handles verification and settlement on the appropriate network.

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
{ url: 'https://x402.org/facilitator' }
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
