---
description: Network details and deployed contracts
---

# Network Guide

X402 supports multiple blockchain networks. Currently, **Sepolia** and **Filecoin Calibration** have deployed settlement contracts for testing.

---

## Supported Networks

| Network | Token | Type | Finality | Deployed Contracts |
|---------|-------|------|----------|-------------------|
| **Sepolia** | JPYC, USDC | Testnet | ~2min | ✅ Yes |
| **Filecoin Calibration** | USDFC | Testnet | ~60s | ✅ Yes |
| Ethereum | JPYC, USDC | Mainnet | ~2min | ❌ Not yet |
| Polygon | JPYC, USDC | Mainnet | ~5s | ❌ Not yet |
| Base | USDC | Mainnet | ~2s | ❌ Not yet |
| Avalanche | USDC | Mainnet | ~2s | ❌ Not yet |
| Filecoin | USDFC | Mainnet | ~60s | ❌ Not yet |

---

## Sepolia (Testnet)

### Overview
- **Purpose**: Development and testing
- **Block Time**: ~12 seconds
- **Finality**: ~2 minutes
- **Gas**: Free (testnet)
- **Tokens**: JPYC, USDC

### Deployed Contracts

**SettlementRouter**: `0x876308C01deCdbae46E353C81d869f102Ec1DFB3`
- Handles payment settlement and fee tracking
- Accumulates facilitator fees in `pendingFees` mapping

**TransferHook**: `0x884B29Ee0BdDdFD262990f720D7387611a1be50c`
- Default hook for transferring payments to merchants
- Supports simple and distributed transfers

**Tokens:**
- JPYC: `0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29` (18 decimals)
- USDC: `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238` (6 decimals)

### Block Explorer
https://sepolia.etherscan.io

### Get Testnet Tokens
- ETH: https://sepoliafaucet.com
- JPYC: Contact JPYC team or use testnet contract
- USDC: Use Sepolia faucets

### Example Usage

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.get('/api/data', paymentMiddleware(
  merchantWallet,
  {
    'GET /api/data': {
      price: '$0.01',
      network: 'sepolia',
      token: 'JPYC'
    }
  },
  { url: facilitatorUrl }
), (req, res) => {
  res.json({ data: 'premium content' });
});
```

---

## Filecoin Calibration (Testnet)

### Overview
- **Purpose**: Development and testing for Filecoin use cases
- **Block Time**: ~30 seconds
- **Finality**: ~60 seconds
- **Gas**: Low (testnet)
- **Token**: USDFC (USD for Filecoin Community)

### Deployed Contracts

**SettlementRouter**: `0xf9EF447517d15c503cfE3328b841441b878672A3`
- Handles payment settlement and fee tracking
- Accumulates facilitator fees in `pendingFees` mapping

**TransferHook**: `0xcab270aD54C7ACc89F2545e4E29e1FDa2Ee0651f`
- Default hook for transferring payments to merchants
- Supports simple and distributed transfers

**Token:**
- USDFC: `0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0` (18 decimals)

### Block Explorer
https://calibration.filfox.info

### Get Testnet Tokens
- tFIL: https://faucet.calibnet.chainsafe-fil.io
- USDFC: Use Calibration testnet faucet

### Example Usage

```typescript
import { paymentMiddleware } from '@secured-finance/sf-x402-express';

app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$9.99',
      network: 'filecoin-calibration',
      token: 'USDFC'
    }
  },
  { url: facilitatorUrl }
), async (req, res) => {
  const cid = await storeToFilecoin(req.body.data);
  res.json({ cid, status: 'stored' });
});
```

---

## Other Supported Networks

The following networks are supported by the protocol but **don't have settlement contracts deployed yet**:

### Ethereum Mainnet
- **Tokens**: JPYC, USDC
- **Best for**: High-value B2B payments
- **Finality**: ~2 minutes
- **Status**: Protocol support only

### Polygon
- **Tokens**: JPYC, USDC
- **Best for**: Fast, low-cost micropayments
- **Finality**: ~5 seconds
- **Status**: Protocol support only

### Base
- **Token**: USDC
- **Best for**: Consumer apps, creator tips
- **Finality**: ~2 seconds
- **Status**: Protocol support only

### Avalanche
- **Token**: USDC
- **Best for**: DeFi integrations
- **Finality**: ~2 seconds
- **Status**: Protocol support only

### Filecoin Mainnet
- **Token**: USDFC
- **Best for**: Storage payments, subscriptions
- **Finality**: ~60 seconds
- **Status**: Protocol support only

---

## Choosing a Network

**For development:**
- Use **Sepolia** for most testing
- Use **Filecoin Calibration** for Filecoin-specific features

**Network characteristics:**

| Characteristic | Sepolia | Filecoin Calibration |
|----------------|---------|---------------------|
| **Speed** | ~2min | ~60s |
| **Tokens** | JPYC, USDC | USDFC |
| **Gas cost** | Free | Low |
| **Best for** | General testing | Storage use cases |

---

## Network Configuration

The X402 packages automatically handle network configuration. Just specify the network name:

```typescript
{
  price: '$0.01',
  network: 'sepolia',              // or 'filecoin-calibration'
  token: 'JPYC'                    // or 'USDFC'
}
```

Contract addresses and RPC endpoints are built into the packages.

---

## Custom RPC Endpoints

For better reliability, configure custom RPC endpoints:

```bash
# .env
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY
FILECOIN_CALIBRATION_RPC_URL=https://api.calibration.node.glif.io/rpc/v1
```

Free RPC providers:
- **Alchemy**: https://www.alchemy.com
- **Infura**: https://www.infura.io
- **Ankr**: https://www.ankr.com

---

## Related Resources

* **[Quick Start](../quick-start.md)** - Build your first paid API
* **[Facilitator Guide](facilitator-guide.md)** - Run your own facilitator
* **[Use Cases](use-cases.md)** - Example implementations
