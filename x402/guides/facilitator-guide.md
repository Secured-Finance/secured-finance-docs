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
pnpm init
pnpm add @secured-finance/sf-x402 express dotenv express-rate-limit
pnpm add -D typescript @types/express @types/node tsx
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

**Full example code:** See [X402 GitHub repository](https://github.com/Secured-Finance/x402/tree/main/examples/typescript/facilitator) for complete implementation.

**Basic structure:**

```typescript
import express from 'express';
import { verify, settle } from '@secured-finance/sf-x402/facilitator';
import { createConnectedClient, createSigner } from '@secured-finance/sf-x402/shared/evm';

const app = express();
app.use(express.json());

// Health check
app.get('/health', (req, res) => {
  res.json({ status: 'healthy' });
});

// Verify payment signature
app.post('/verify', async (req, res) => {
  const { paymentPayload, paymentRequirements } = req.body;
  const client = createConnectedClient(paymentRequirements.network);
  const result = await verify(client, paymentPayload, paymentRequirements);
  res.json(result);
});

// Settle payment on-chain
app.post('/settle', async (req, res) => {
  const { paymentPayload, paymentRequirements } = req.body;
  const signer = await createSigner(
    paymentRequirements.network,
    process.env.EVM_PRIVATE_KEY!
  );
  const result = await settle(signer, paymentPayload, paymentRequirements);
  res.json(result);
});

app.listen(3000);
```

### 4. Run

```bash
pnpm tsx index.ts
```

---

## Fee Mechanism

The SettlementRouter contract tracks your earned fees:

```typescript
// Fee calculation (from @secured-finance/sf-x402)
import { calculateFee } from '@secured-finance/sf-x402';

const totalAmount = BigInt(1000000); // 1.00 USDC (6 decimals)
const { feeAmount, merchantAmount } = calculateFee(totalAmount, 6);
// feeAmount: 10000n (0.01 USDC - minimum fee)
// merchantAmount: 990000n (0.99 USDC)
```

**Fee Examples:**

| Payment | Total Amount | Your Fee (0.3%, min $0.01) | Merchant Gets |
|---------|--------------|---------------------------|---------------|
| $1.00 | 1.00 | $0.01 | $0.99 |
| $10.00 | 10.00 | $0.03 | $9.97 |
| $100.00 | 100.00 | $0.30 | $99.70 |

### Claiming Fees

Fees accumulate in the SettlementRouter contract. You can claim them anytime:

```typescript
import { claimFees } from '@secured-finance/sf-x402/facilitator';

// Claim accumulated fees for multiple tokens
const txHash = await claimFees(
  ['0xTokenAddress1', '0xTokenAddress2'],
  'sepolia',
  wallet
);
```

Check pending fees:

```typescript
import { getPendingFees } from '@secured-finance/sf-x402/facilitator';

const fees = await getPendingFees(
  facilitatorAddress,
  ['0xUSDC', '0xJPYC'],
  'sepolia',
  wallet
);
// Returns: Map<tokenAddress, feeAmount>
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
- **Cloud platforms**: Railway, Render, AWS
- **See full deployment guide**: [GitHub repository](https://github.com/Secured-Finance/x402)

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

Use the SDK to query pending fees:

```typescript
import { getPendingFees } from '@secured-finance/sf-x402/facilitator';

const pendingFees = await getPendingFees(
  yourFacilitatorAddress,
  [usdcAddress, jpycAddress],
  'sepolia',
  wallet
);

console.log('Pending USDC:', pendingFees.get(usdcAddress));
console.log('Pending JPYC:', pendingFees.get(jpycAddress));
```

Or view on block explorers:
- Sepolia: https://sepolia.etherscan.io
- Filecoin Calibration: https://calibration.filfox.info

---

## Next Steps

- **[Example Code](https://github.com/Secured-Finance/x402/tree/main/examples/typescript/facilitator)** - Full implementation
- **[Network Guide](network-guide.md)** - Network details and contract addresses
- **[Core Package](../packages/core.md)** - API reference

---

Need help? [Join our Discord](https://discord.gg/securedfinance)
