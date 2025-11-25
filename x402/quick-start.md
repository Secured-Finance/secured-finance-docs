---
description: Build your first paid API in 10 minutes
---

# 🚀 Quick Start

This guide will walk you through creating your first X402-powered paid API. You'll build a simple weather API that charges $0.01 per request.

**Time to complete**: ~10 minutes

---

## Prerequisites

- Node.js 18 or higher
- A wallet (MetaMask, Coinbase Wallet)
- Basic knowledge of Express.js or Next.js

---

## Step 1: Install Packages

Choose your framework:

### Express.js

```bash
mkdir my-paid-api
cd my-paid-api
pnpm init
pnpm add @secured-finance/sf-x402-express express dotenv
pnpm add -D typescript @types/express @types/node tsx
```

### Next.js

```bash
npx create-next-app@latest my-paid-api
cd my-paid-api
pnpm add @secured-finance/sf-x402-next
```

---

## Step 2: Set Up Environment Variables

Create `.env` file:

```bash
# Your merchant wallet (where payments go)
MERCHANT_WALLET=0xYourWalletAddress

# Facilitator service (use hosted or run your own)
FACILITATOR_URL=https://x402.org/facilitator

# Optional: Custom RPC (for better reliability)
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_API_KEY
```

💡 **Tip**: Use the public facilitator (`https://x402.org/facilitator`) for testing. [Run your own](facilitator-guide.md) for production.

---

## Step 3: Create Your Paid API

### Express.js Example

Create `server.ts`:

```typescript
import express from 'express';
import { paymentMiddleware } from '@secured-finance/sf-x402-express';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
app.use(express.json());

const MERCHANT_WALLET = process.env.MERCHANT_WALLET!;
const FACILITATOR_URL = process.env.FACILITATOR_URL!;

// JPYC payment on Sepolia testnet - Pay $0.01 for weather data
app.get('/weather/:city', paymentMiddleware(
  MERCHANT_WALLET,
  {
    'GET /weather/:city': {
      price: '$0.01',       // USD price (converted to JPYC)
      network: 'sepolia',   // Sepolia testnet
      token: 'JPYC'         // Japanese Yen Coin (18 decimals)
    }
  },
  { url: FACILITATOR_URL }
), (req, res) => {
  // This code only runs after payment is verified
  const { city } = req.params;

  res.json({
    city,
    temperature: 72,
    condition: 'sunny',
    humidity: 45,
    wind: '10 mph'
  });
});

// USDFC payment on Filecoin Calibration testnet
app.post('/store-data', paymentMiddleware(
  MERCHANT_WALLET,
  {
    'POST /store-data': {
      price: '$9.99',                    // USD price
      network: 'filecoin-calibration',   // Filecoin testnet
      token: 'USDFC'                     // USD for Filecoin Community (18 decimals)
    }
  },
  { url: FACILITATOR_URL }
), (req, res) => {
  res.json({
    cid: 'bafy...',
    status: 'stored'
  });
});

// Free endpoint (no payment required)
app.get('/health', (req, res) => {
  res.json({ status: 'ok' });
});

app.listen(4000, () => {
  console.log('Paid API running on http://localhost:4000');
  console.log('Payments go to:', MERCHANT_WALLET);
  console.log('Using facilitator:', FACILITATOR_URL);
});
```

### Next.js Example

Create `app/api/weather/[city]/route.ts`:

```typescript
import { NextRequest } from 'next/server';
import { paymentMiddleware } from '@secured-finance/sf-x402-next';

const MERCHANT_WALLET = process.env.MERCHANT_WALLET!;
const FACILITATOR_URL = process.env.FACILITATOR_URL!;

export async function GET(
  request: NextRequest,
  { params }: { params: { city: string } }
) {
  // JPYC payment on Sepolia testnet
  const middleware = paymentMiddleware(
    MERCHANT_WALLET,
    {
      'GET /api/weather/:city': {
        price: '$0.01',
        network: 'sepolia',   // Use 'polygon' or 'mainnet' for production
        token: 'JPYC'         // Japanese Yen Coin (18 decimals)
      }
    },
    { url: FACILITATOR_URL }
  );

  // Check payment
  const paymentResponse = await middleware(request);
  if (paymentResponse) return paymentResponse; // Return 402 if not paid

  // Payment verified - return data
  return Response.json({
    city: params.city,
    temperature: 72,
    condition: 'sunny'
  });
}
```

---

## Step 4: Run Your API

```bash
# Express
pnpm tsx server.ts

# Next.js
pnpm dev
```

You should see:

```
✅ Paid API running on http://localhost:4000
💰 Payments go to: 0xYourWallet...
🔧 Using facilitator: https://facilitator.x402.org
```

---

## Step 5: Test the Payment Flow

### Test 1: Request Without Payment (402 Error)

```bash
curl http://localhost:4000/weather/tokyo
```

**Response:**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Payment Required</title>
  </head>
  <body>
    <h1>402 Payment Required</h1>
    <p>This resource requires payment of $0.01 JPYC on sepolia</p>
    <!-- Payment form will appear here in browser -->
  </body>
</html>
```

**HTTP Status**: `402 Payment Required`

---

### Test 2: Open in Browser (Make Payment)

1. Open `http://localhost:4000/weather/tokyo` in your browser
2. You'll see a payment prompt
3. Connect your MetaMask wallet
4. Click "Pay $0.01"
5. Sign the message in your wallet (free, no gas fee!)
6. See the weather data appear instantly

**What happened:**
1. Browser requested `/weather/tokyo` without payment
2. Server returned 402 with payment form
3. You signed payment authorization in wallet
4. Browser retried request with `X-PAYMENT` header
5. Middleware verified signature with facilitator
6. Server returned weather data
7. Facilitator settled payment on-chain (paid gas)

---

## Step 6: Check Payment on Blockchain

After successful payment, check the transaction:

1. Look at terminal logs - you'll see transaction hash
2. Open Sepolia Etherscan: `https://sepolia.etherscan.io/tx/TX_HASH`
3. Verify:
   - ✅ Transfer from user wallet to merchant wallet
   - ✅ Token: JPYC
   - ✅ Amount: 0.01 JPYC (in atomic units)
   - ✅ Paid by facilitator (gas fee ~$0.02)

---

## What You Built

Congratulations! You just built a paid API with:

✅ **User-friendly payments** - No gas fees for users
✅ **Instant settlement** - ~5 seconds on Sepolia
✅ **Automatic verification** - Middleware handles everything
✅ **Blockchain transparency** - All payments on-chain

---

## Next Steps

### 1. Customize Your Paywall

```typescript
app.use(paymentMiddleware(
  MERCHANT_WALLET,
  routes,
  { url: FACILITATOR_URL },
  {
    customPaywallHtml: `
      <html>
        <body>
          <h1>Premium Weather Data</h1>
          <p>Get accurate weather for any city for just $0.01</p>
          <!-- X402 injects payment button automatically -->
        </body>
      </html>
    `
  }
));
```

### 2. Add Dynamic Pricing

```typescript
app.post('/translate', (req, res, next) => {
  const wordCount = req.body.text.split(' ').length;
  const pricePerWord = 0.001;
  const total = Math.max(0.01, wordCount * pricePerWord);

  const middleware = paymentMiddleware(
    MERCHANT_WALLET,
    {
      'POST /translate': {
        price: `$${total.toFixed(2)}`,
        network: 'sepolia'
      }
    },
    { url: FACILITATOR_URL }
  );

  middleware(req, res, next);
}, (req, res) => {
  res.json({ translation: translateText(req.body.text) });
});
```

### 3. Support Multiple Networks

```typescript
app.get('/data', (req, res, next) => {
  const network = req.query.network || 'polygon';

  const middleware = paymentMiddleware(
    MERCHANT_WALLET,
    {
      'GET /data': {
        price: '$0.50',
        network: network as any,
        // Auto-select token based on network
      }
    },
    { url: FACILITATOR_URL }
  );

  middleware(req, res, next);
});
```

---

## Testing on Different Networks

### JPYC on Sepolia (Recommended for Development)

```typescript
{
  price: '$0.01',
  network: 'sepolia',       // Ethereum Sepolia testnet
  token: 'JPYC'             // Japanese Yen Coin (18 decimals)
}
```

**Get testnet tokens:**
- Sepolia ETH Faucet: https://sepoliafaucet.com/
- JPYC Sepolia: `0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29`

### USDFC on Filecoin Calibration (Storage Use Cases)

```typescript
{
  price: '$9.99',
  network: 'filecoin-calibration',  // Filecoin testnet
  token: 'USDFC'                     // USD for Filecoin Community (18 decimals)
}
```

**Get testnet tokens:**
- tFIL Faucet: https://faucet.calibnet.chainsafe-fil.io/
- USDFC Calibration: `0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0`

### Production Networks

For production, switch to mainnet networks:

```typescript
// JPYC on Polygon (fast, low fees)
{
  price: '$0.01',
  network: 'polygon',
  token: 'JPYC'
}

// USDFC on Filecoin (storage payments)
{
  price: '$9.99',
  network: 'filecoin',
  token: 'USDFC'
}
```

---

## Common Issues

### Issue: "Insufficient balance"

**Solution**: Get testnet tokens from faucets:
- Sepolia ETH: https://sepoliafaucet.com/
- JPYC on Sepolia: Contact the JPYC team or use the testnet contract
- USDFC on Filecoin Calibration: https://faucet.calibnet.chainsafe-fil.io/

### Issue: "Facilitator connection failed"

**Solution**: Check facilitator URL in `.env`:
```bash
FACILITATOR_URL=https://x402.org/facilitator  # Public facilitator
```

Or [run your own facilitator](facilitator-guide.md)

### Issue: "Transaction timeout"

**Solution**: Use custom RPC for better reliability:
```bash
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_API_KEY
```

Get free RPC from:
- Alchemy: https://www.alchemy.com/
- Infura: https://www.infura.io/
- Ankr: https://www.ankr.com/

---

## Production Checklist

Before going to production:

- [ ] **Switch to mainnet**: Change network from `sepolia` to `polygon`, `ethereum`, etc.
- [ ] **Run your own facilitator**: Don't rely on public facilitator (see [Facilitator Guide](facilitator-guide.md))
- [ ] **Set up monitoring**: Track payments, errors, revenue
- [ ] **Add rate limiting**: Prevent abuse
- [ ] **Use custom RPC**: For better uptime
- [ ] **Test error handling**: Ensure graceful failures
- [ ] **Document pricing**: Make it clear to users
- [ ] **Add support contact**: Help users with payment issues

---

## Example Projects

Check out complete examples:

* **Weather API** - Pay-per-request data
  * Code: `examples/typescript/servers/express/weather.ts`
  * Live demo: https://weather.x402.org

* **E-Commerce Store** - Dynamic cart pricing
  * Code: `examples/typescript/fullstack/next/`
  * Live demo: https://shop.x402.org

* **Content Paywall** - Premium articles
  * Code: `examples/typescript/servers/hono/blog.ts`
  * Live demo: https://blog.x402.org

---

## Related Resources

* [Network Guide](network-guide.md) - Choose the right network
* [Facilitator Guide](facilitator-guide.md) - Run your own & earn fees
* [API Reference](api-reference.md) - Complete package docs
* [GitHub Examples](https://github.com/Secured-Finance/x402/tree/main/examples) - Working code

---

**Questions?** Join our [Discord](https://discord.gg/securedfinance) or [open an issue](https://github.com/Secured-Finance/x402/issues)

---

**Ready to deploy your own facilitator?** → [Facilitator Guide](facilitator-guide.md)
