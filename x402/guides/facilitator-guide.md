---
description: Run your own X402 facilitator to earn fees on payments
---

# Running Your Own Facilitator

Deploy your own facilitator node to verify and settle payments, earn fees on transactions you process, and control your payment infrastructure.

---

## What is a Facilitator?

A facilitator:
- Verifies payment signatures from users
- Settles payments on-chain (pays gas fees)
- Earns fees (0.3%, minimum $0.01) on payments they process
- Claims accumulated fees from the SettlementRouter contract

```
User signs → Facilitator verifies → Facilitator settles → Merchant receives payment → Facilitator claims accumulated fees
```

---

## How Fees Work

When you call `settleAndExecute()`:
1. **Fee calculated**: 0.3% of payment amount (minimum $0.01 USD)
2. **User pays total**: merchantAmount + facilitatorFee
3. **Payment settled**:
   - Merchant receives merchantAmount via TransferHook
   - Your fee accumulates in `pendingFees[yourAddress][token]`
4. **Claim fees**: Call `claimFees([tokens])` to withdraw accumulated fees anytime

**Example:** $10,000 daily volume = $30/day = $900/month in fees (at 0.3%)

---

## Why Run Your Own?

**Earn Fees:**
- 0.3% on every payment you process (minimum $0.01)
- Claim accumulated fees anytime
- Set your own fee structure if desired

**Control Infrastructure:**
- No dependency on third-party services
- Custom RPC endpoints for reliability
- Your own rate limits and policies

---

## Prerequisites

- Node.js 18+
- Wallet with testnet ETH/FIL for gas (~$10 to start)
- Basic knowledge of Express.js

---

## Quick Setup

### 1. Install Dependencies

```bash
mkdir my-facilitator && cd my-facilitator
npm init -y
npm install @secured-finance/x402-core express dotenv express-rate-limit
npm install -D typescript @types/express @types/node tsx
```

### 2. Configure Environment

Create `.env`:

```bash
EVM_PRIVATE_KEY=0x...  # Your facilitator wallet (pays gas, receives fees)
PORT=3000
```

⚠️ **Never commit your private key to git**

### 3. Create Server

The facilitator needs three endpoints: `/health`, `/verify`, and `/settle`.

**Full example code:** See [x402-exec GitHub repository](https://github.com/Secured-Finance/x402-exec/tree/main/facilitator) for complete production-ready implementation.

**Basic structure:**

```typescript
import express from 'express';
import { createPublicClient, createWalletClient, http } from 'viem';
import { privateKeyToAccount } from 'viem/accounts';
import { baseSepolia } from 'viem/chains';

const app = express();
app.use(express.json());

// Initialize blockchain clients
const account = privateKeyToAccount(process.env.EVM_PRIVATE_KEY as `0x${string}`);
const publicClient = createPublicClient({
  chain: baseSepolia,
  transport: http()
});
const walletClient = createWalletClient({
  account,
  chain: baseSepolia,
  transport: http()
});

// Health check
app.get('/health', (req, res) => {
  res.json({ status: 'healthy' });
});

// Verify payment signature (off-chain validation)
app.post('/verify', async (req, res) => {
  const { paymentPayload, paymentRequirements } = req.body;
  
  // Implement signature verification logic
  // Validate commitment, check balances, verify signatures
  
  res.json({
    isValid: true,
    payer: paymentPayload.from
  });
});

// Settle payment on-chain via SettlementRouter
app.post('/settle', async (req, res) => {
  const { paymentPayload, paymentRequirements } = req.body;
  
  // Call SettlementRouter.settleAndExecute()
  // This pays gas and earns facilitator fee
  
  res.json({
    success: true,
    transaction: txHash,
    network: paymentRequirements.network,
    payer: paymentPayload.from
  });
});

app.listen(3000);
```

For a complete, production-ready facilitator implementation with all features, see the [facilitator directory](https://github.com/Secured-Finance/x402-exec/tree/main/facilitator) in the x402-exec repository.

### 4. Run

```bash
npm run dev
# or
npx tsx index.ts
```

---

## Fee Mechanism

The SettlementRouter contract tracks your earned fees. Fees are automatically calculated and deducted during settlement:

```typescript
// Fee calculation example
const paymentAmount = 1000000n; // 1.00 USDC (6 decimals)
const feePercentage = 30n; // 0.3% = 30 basis points
const minFeeUSD = 10000n; // 0.01 USDC minimum

// Calculate fee
const calculatedFee = (paymentAmount * feePercentage) / 10000n;
const facilitatorFee = calculatedFee > minFeeUSD ? calculatedFee : minFeeUSD;
const merchantAmount = paymentAmount - facilitatorFee;

// feeAmount: 10000n (0.01 USDC - minimum fee applied)
// merchantAmount: 990000n (0.99 USDC)
```

**Fee Examples:**

| Payment | Total Amount | Your Fee (0.3%, min $0.01) | Merchant Gets |
|---------|--------------|---------------------------|---------------|
| $1.00 | 1.00 | $0.01 | $0.99 |
| $10.00 | 10.00 | $0.03 | $9.97 |
| $100.00 | 100.00 | $0.30 | $99.70 |

### Claiming Fees

Fees accumulate in the SettlementRouter contract. You can claim them anytime by calling the contract directly:

```typescript
import { getContract } from 'viem';
import { getNetworkConfig } from '@secured-finance/x402-core';

// Get SettlementRouter address for your network
const config = getNetworkConfig('base-sepolia');
const settlementRouter = getContract({
  address: config.settlementRouter,
  abi: settlementRouterAbi,
  client: walletClient
});

// Claim accumulated fees for multiple tokens
const txHash = await settlementRouter.write.claimFees([
  ['0xTokenAddress1', '0xTokenAddress2']
]);
```

Check pending fees:

```typescript
// Query pending fees from the contract
const pendingFee = await settlementRouter.read.pendingFees([
  facilitatorAddress,
  tokenAddress
]);

console.log(`Pending fees: ${pendingFee}`);
```

---

## Deployment

### Docker (Recommended)

Create `Dockerfile`:

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm && pnpm install
COPY . .
RUN pnpm build
EXPOSE 3000
CMD ["node", "dist/index.js"]
```

Run:

```bash
docker build -t x402-facilitator .
docker run -d -p 3000:3000 -e EVM_PRIVATE_KEY=$EVM_PRIVATE_KEY x402-facilitator
```

### Other Options

- **PM2**: Process manager for Node.js apps
- **Cloud platforms**: Railway, Render, AWS, Cloudflare Workers
- **See full deployment guide**: [x402-exec repository](https://github.com/Secured-Finance/x402-exec)

---

## Security Checklist

Before production:

- [ ] Secure private key (use secrets manager)
- [ ] Enable rate limiting
- [ ] Use HTTPS only
- [ ] Monitor gas balance
- [ ] Set up error logging
- [ ] Use custom RPC endpoints for reliability

---

## Monitoring

**Key metrics:**
- Gas balance (alert when < $10)
- Payment volume and fee revenue
- Error rates (verification/settlement)
- Response times

**Check your earned fees:**

Query pending fees from the SettlementRouter contract:

```typescript
import { getContract } from 'viem';
import { getNetworkConfig } from '@secured-finance/x402-core';

const config = getNetworkConfig('base-sepolia');
const settlementRouter = getContract({
  address: config.settlementRouter,
  abi: settlementRouterAbi,
  client: publicClient
});

// Check fees for each token
const usdcFees = await settlementRouter.read.pendingFees([
  yourFacilitatorAddress,
  usdcAddress
]);

console.log(`Pending USDC fees: ${usdcFees}`);
```

Or view on block explorers:
- Base: https://basescan.org
- X-Layer: https://www.oklink.com/xlayer
- Base Sepolia: https://sepolia.basescan.org
- X-Layer Testnet: https://www.oklink.com/xlayer-test
- Sepolia: https://sepolia.etherscan.io
- Filecoin Calibration: https://calibration.filfox.info

---

## Next Steps

- **[Production Facilitator](https://github.com/Secured-Finance/x402-exec/tree/main/facilitator)** - Full production implementation
- **[Network Guide](network-guide.md)** - Network details and contract addresses
- **[Core Package](../packages/core.md)** - API reference
- **[Live Demo](https://demo.x402x.dev)** - See it in action

---

Need help? [Join our Discord](https://discord.gg/securedfinance)
