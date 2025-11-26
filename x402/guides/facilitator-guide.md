---
description: Build and deploy your own X402 facilitator to earn 0.3% fees
---

# 🏦 Facilitator Guide

A facilitator is a payment gateway for blockchain APIs. It verifies payment signatures and settles transactions on-chain, earning 0.3% fees automatically.

---

## What is a Facilitator?

Think of a facilitator as the **payment processor** in the X402 ecosystem:

```
User → Signs payment (free)
  ↓
Middleware → Asks facilitator "Is this valid?"
  ↓
Facilitator → Verifies signature & checks balance
  ↓
Facilitator → Settles on blockchain (pays gas)
  ↓
Merchant → Receives 99.7% of payment
Facilitator → Receives 0.3% fee
```

---

## Why Run a Facilitator?

### 1. Earn Revenue

With the FeeReceiver contract, you earn **0.3% on every transaction**:

| Daily Volume | Daily Revenue | Monthly Revenue |
|--------------|---------------|-----------------|
| $5,000 | $15 | $450 |
| $25,000 | $75 | $2,250 |
| $100,000 | $300 | $9,000 |

**Fee structure:**
- **0.3%** platform fee on all transactions
- **Minimum fee**: $0.01 (token equivalent)
- **Automatic splitting** via on-chain FeeReceiver contract

**Example:**
- User pays: $10.00 USDC
- Merchant receives: $9.97
- Facilitator receives: $0.03
- All automatic, trustless, on-chain

---

### 2. Control Your Infrastructure

Running your own facilitator means:
- ✅ No dependency on third-party services
- ✅ Custom RPC endpoints for better uptime
- ✅ Your own rate limits and policies
- ✅ Full control over supported networks

---

### 3. Support Your Ecosystem

Public facilitators enable:
- Open payment infrastructure
- Permissionless integration
- Decentralized access to X402 payments

---

## Building a Facilitator

### Prerequisites

- Node.js 18 or higher
- A wallet with ETH/FIL for gas fees (~$50-100 to start)
- 15 minutes of your time

---

### Step 1: Install Dependencies

```bash
mkdir my-facilitator
cd my-facilitator
pnpm init
pnpm add @secured-finance/sf-x402 express dotenv express-rate-limit
pnpm add -D typescript @types/express @types/node tsx
```

---

### Step 2: Set Up Environment

Create `.env` file:

```bash
# Your private key (this wallet pays gas fees and receives 0.3% fees)
EVM_PRIVATE_KEY=0x1234567890abcdef...

# Optional: Custom RPC endpoints for better reliability
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_API_KEY
POLYGON_RPC_URL=https://polygon-mainnet.g.alchemy.com/v2/YOUR_API_KEY

# Server port
PORT=3000
```

⚠️ **Security Warning**:
- Never commit `.env` to git
- This wallet will pay gas for all transactions
- Start with testnet funds (~$10 worth)
- Monitor gas balance daily

---

### Step 3: Create Facilitator Server

Create `index.ts`:

```typescript
import express from 'express';
import rateLimit from 'express-rate-limit';
import dotenv from 'dotenv';
import { verify, settle, getSupportedKinds } from '@secured-finance/sf-x402/facilitator';
import { createConnectedClient, createSigner } from '@secured-finance/sf-x402/shared/evm';

dotenv.config();

const app = express();
app.use(express.json());

// Rate limiting: 100 requests per 15 minutes per IP
app.use(rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 100,
  message: 'Too many requests, please try again later'
}));

// Health check
app.get('/health', (req, res) => {
  res.json({
    status: 'healthy',
    timestamp: new Date().toISOString()
  });
});

// Show supported payment types
app.get('/supported', (req, res) => {
  const kinds = getSupportedKinds();
  res.json({ kinds });
});

// Verify payment signature
app.post('/verify', async (req, res) => {
  try {
    const { paymentPayload, paymentRequirements } = req.body;

    // Create read-only client for the network
    const client = createConnectedClient(paymentRequirements.network);

    const result = await verify(client, paymentPayload, paymentRequirements);

    if (result.isValid) {
      res.json(result);
    } else {
      res.status(400).json(result);
    }
  } catch (error: any) {
    console.error('Verification error:', error);
    res.status(500).json({
      isValid: false,
      error: error.message
    });
  }
});

// Settle payment on blockchain
app.post('/settle', async (req, res) => {
  try {
    const { paymentPayload, paymentRequirements } = req.body;

    // Create signer wallet (this pays gas and receives fees)
    const signer = await createSigner(
      paymentRequirements.network,
      process.env.EVM_PRIVATE_KEY!
    );

    const result = await settle(signer, paymentPayload, paymentRequirements);

    if (result.success) {
      console.log('Payment settled:', result.transaction);
      res.json(result);
    } else {
      res.status(400).json(result);
    }
  } catch (error: any) {
    console.error('Settlement error:', error);
    res.status(500).json({
      success: false,
      error: error.message
    });
  }
});

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Facilitator running on port ${PORT}`);
  console.log(`Health: http://localhost:${PORT}/health`);
  console.log(`Supported: http://localhost:${PORT}/supported`);
});
```

---

### Step 4: Run Your Facilitator

```bash
pnpm tsx index.ts
```

You should see:

```
✅ Facilitator running on port 3000
📊 Health: http://localhost:3000/health
🔍 Supported: http://localhost:3000/supported
```

---

### Step 5: Test the Facilitator

#### Test 1: Health Check

```bash
curl http://localhost:3000/health
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2024-11-17T12:00:00.000Z"
}
```

#### Test 2: Check Supported Networks

```bash
curl http://localhost:3000/supported
```

**Response:**
```json
{
  "kinds": [
    { "x402Version": 1, "scheme": "exact", "network": "sepolia" },
    { "x402Version": 1, "scheme": "exact", "network": "polygon" },
    { "x402Version": 1, "scheme": "exact", "network": "filecoin-calibration" },
    { "x402Version": 1, "scheme": "exact", "network": "base" }
  ]
}
```

---

## FeeReceiver: Automatic Revenue

### How FeeReceiver Works

The FeeReceiver smart contract automatically splits every payment:

```
User pays $100.00 USDC
     ↓
FeeReceiver.settleWithAuthorization()
     ↓
  Splits payment:
     ├─ $99.70 → Merchant wallet
     └─ $0.30  → Facilitator wallet (you!)
```

**Deployed on:**
- ✅ Sepolia (JPYC): `0x8F35dfEC24944b5f87A97D38402dfA9117110d77`
- ✅ Filecoin Calibration (USDFC): `0x0f7A0E7942d1b7a60921Ec99E655402Bd014FDC2`

---

### Fee Calculation

```typescript
// From FeeReceiver.sol
function calculateFee(uint256 totalAmount) public pure returns (uint256) {
  uint256 percentFee = (totalAmount * 3) / 1000; // 0.3%
  uint256 minFee = 10 ** 4; // 0.01 USDC (6 decimals)

  return percentFee > minFee ? percentFee : minFee;
}
```

**Examples:**

| Payment | Fee (0.3%) | Min Fee | Actual Fee | Merchant Gets |
|---------|------------|---------|------------|---------------|
| $1.00 | $0.003 | $0.01 | **$0.01** | $0.99 |
| $10.00 | $0.03 | $0.01 | **$0.03** | $9.97 |
| $100.00 | $0.30 | $0.01 | **$0.30** | $99.70 |
| $1,000.00 | $3.00 | $0.01 | **$3.00** | $997.00 |

---

### Checking Your Earned Fees

Your facilitator wallet automatically receives fees. Check balance:

```bash
# Sepolia JPYC balance (18 decimals)
cast balance YOUR_FACILITATOR_WALLET \
  --erc20 0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29

# Filecoin Calibration USDFC balance (18 decimals)
cast balance YOUR_FACILITATOR_WALLET \
  --erc20 0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0 \
  --rpc-url https://api.calibration.node.glif.io/rpc/v1
```

Or check on block explorers:
- Sepolia (JPYC): https://sepolia.etherscan.io/address/YOUR_WALLET
- Filecoin Calibration (USDFC): https://calibration.filfox.info/en/address/YOUR_WALLET
- Polygon (JPYC): https://polygonscan.com/address/YOUR_WALLET

---

## Deployment to Production

### Option 1: Docker Container

Create `Dockerfile`:

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package.json pnpm-lock.yaml ./
RUN npm install -g pnpm && pnpm install --frozen-lockfile

COPY . .

RUN pnpm build

EXPOSE 3000

CMD ["node", "dist/index.js"]
```

Build and run:

```bash
docker build -t x402-facilitator .
docker run -d \
  --name facilitator \
  -p 3000:3000 \
  -e EVM_PRIVATE_KEY=$EVM_PRIVATE_KEY \
  x402-facilitator
```

---

### Option 2: PM2 Process Manager

Install PM2:

```bash
npm install -g pm2
```

Create `ecosystem.config.js`:

```javascript
module.exports = {
  apps: [{
    name: 'x402-facilitator',
    script: 'dist/index.js',
    instances: 1,
    autorestart: true,
    watch: false,
    max_memory_restart: '500M',
    env: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }]
};
```

Deploy:

```bash
pnpm build
pm2 start ecosystem.config.js
pm2 save
pm2 startup  # Auto-restart on reboot
```

---

### Option 3: Cloud Platforms

#### Railway

1. Create `railway.toml`:

```toml
[build]
builder = "NIXPACKS"

[deploy]
startCommand = "pnpm start"
healthcheckPath = "/health"
healthcheckTimeout = 100
```

2. Deploy:

```bash
railway up
railway variables set EVM_PRIVATE_KEY=0x...
```

#### Render

1. Create `render.yaml`:

```yaml
services:
  - type: web
    name: x402-facilitator
    env: node
    buildCommand: pnpm install && pnpm build
    startCommand: pnpm start
    healthCheckPath: /health
    envVars:
      - key: EVM_PRIVATE_KEY
        sync: false
```

2. Deploy via Render dashboard or CLI

---

### HTTPS Setup with Nginx

Create `/etc/nginx/sites-available/facilitator`:

```nginx
server {
  listen 443 ssl;
  server_name facilitator.yourdomain.com;

  ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;

  location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```

Enable and restart:

```bash
sudo ln -s /etc/nginx/sites-available/facilitator /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

---

## Monitoring & Alerts

### Key Metrics to Track

1. **Gas Balance**

```bash
# Check ETH balance for gas
cast balance YOUR_FACILITATOR_WALLET --rpc-url https://eth-sepolia.g.alchemy.com/v2/KEY
```

Set up alert when balance < $10

2. **Payment Volume**

Track daily:
- Payments verified
- Payments settled
- Total USD volume
- Fee revenue earned

3. **Error Rates**

Monitor:
- Verification failures (should be < 5%)
- Settlement failures (should be < 1%)
- RPC timeouts

4. **Response Times**

- `/verify` endpoint: < 500ms
- `/settle` endpoint: < 5s (blockchain dependent)

---

### Logging Best Practices

Add structured logging:

```typescript
import winston from 'winston';

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});

// Log successful settlements
logger.info('Payment settled', {
  txHash: result.transaction,
  amount: paymentRequirements.maxAmountRequired,
  network: paymentRequirements.network,
  merchant: paymentRequirements.payTo
});
```

---

## Troubleshooting

### Issue: "Insufficient gas balance"

**Cause**: Facilitator wallet has no ETH/FIL for gas

**Solution**:
```bash
# Check balance
cast balance YOUR_WALLET

# Send gas funds
# ETH: Use MetaMask/Coinbase to send ETH
# FIL: Use Filecoin wallet to send FIL
```

**Prevention**: Set up alerts for low gas balance

---

### Issue: "Nonce already used"

**Cause**: User tried to reuse the same payment signature

**Solution**: This is normal! The error means replay protection is working correctly. User needs to make a new payment.

---

### Issue: "Transaction timeout"

**Cause**: RPC endpoint is slow or unresponsive

**Solution**: Use custom RPC endpoints:

```bash
# .env
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY
POLYGON_RPC_URL=https://polygon-mainnet.g.alchemy.com/v2/YOUR_KEY
```

Get free RPCs from:
- Alchemy: https://www.alchemy.com/
- Infura: https://www.infura.io/
- Ankr: https://www.ankr.com/

---

### Issue: "Invalid signature"

**Cause**: Clock skew, wrong network, or tampered payment

**Solution**:
1. Check system time is accurate (NTP)
2. Verify network matches (sepolia vs polygon)
3. Check signature format

---

## Security Checklist

Before going to production:

- [ ] **Secure private key**: Use secrets manager (AWS Secrets, HashiCorp Vault)
- [ ] **Rate limiting**: Prevent DoS attacks (100 req/15min)
- [ ] **HTTPS only**: Never run HTTP in production
- [ ] **Gas monitoring**: Alert when balance < $10
- [ ] **Error logging**: Track all failures
- [ ] **Regular updates**: Keep dependencies updated
- [ ] **Backup strategy**: Have backup RPC endpoints
- [ ] **Access logs**: Monitor for suspicious activity

---

## Related Resources

* [Overview](../overview.md) - What is X402?
* [Quick Start](../quick-start.md) - Build your first paid API
* [Network Guide](network-guide.md) - Choose the right network
* [Use Cases](use-cases.md) - Real-world examples
* [Core Package](../packages/core.md) - Core library documentation

---

**Need help?** Join [Discord](https://discord.gg/securedfinance) or [open an issue](https://github.com/Secured-Finance/x402/issues)
