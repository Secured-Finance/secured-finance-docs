---
description: Network details and deployed contracts
---

# Network Guide

x402x supports multiple blockchain networks with deployed SettlementRouter contracts for production and testing.

---

## Supported Networks

| Network | Token | Type | Finality | Deployed Contracts |
|---------|-------|------|----------|-------------------|
| **Base** | USDC | Mainnet | ~2s | 🎉 Live |
| **X-Layer** | USDC | Mainnet | ~2s | 🎉 Live |
| **Base Sepolia** | USDC | Testnet | ~2s | ✅ Active |
| **X-Layer Testnet** | USDC | Testnet | ~2s | ✅ Active |
| **Sepolia** | JPYC, USDC | Testnet | ~2min | ✅ Active |
| **Filecoin Calibration** | USDFC | Testnet | ~60s | ✅ Active |
| Ethereum | JPYC, USDC | Mainnet | ~2min | 🚧 Planned |
| Polygon | JPYC, USDC | Mainnet | ~5s | 🚧 Planned |
| Avalanche | USDC | Mainnet | ~2s | 🚧 Planned |
| Filecoin | USDFC | Mainnet | ~60s | 🚧 Planned |

---

## Base (Mainnet) 

### Overview
- **Purpose**: Production payments on Base network
- **Block Time**: ~2 seconds
- **Finality**: ~2 seconds
- **Gas**: Low cost
- **Token**: USDC (6 decimals)
- **Status**: Live in production

### Deployed Contracts

**SettlementRouter**: `0x73fc659Cd5494E69852bE8D9D23FE05Aab14b29B`
- Handles payment settlement and fee tracking
- Accumulates facilitator fees in `pendingFees` mapping

**TransferHook**: `0x081258287F692D61575387ee2a4075f34dd7Aef7`
- Default hook for transferring payments to merchants
- Supports simple and distributed transfers

### Block Explorer
https://basescan.org

### Example Usage

```typescript
import { X402Client } from '@secured-finance/x402-client';
import { TransferHook, parseDefaultAssetAmount } from '@secured-finance/x402-core';

const client = new X402Client({
  wallet: extendedWallet,
  network: 'base'
});

const amount = parseDefaultAssetAmount('1', 'base'); // 1 USDC
await client.execute({
  hook: TransferHook.getAddress('base'),
  hookData: TransferHook.encode(),
  amount,
  payTo: merchantAddress
});
```

---

## X-Layer (Mainnet) 

### Overview
- **Purpose**: Production payments on X-Layer network
- **Block Time**: ~2 seconds
- **Finality**: ~2 seconds
- **Gas**: Low cost
- **Token**: USDC (6 decimals)
- **Status**: Live in production

### Deployed Contracts

**SettlementRouter**: `0x73fc659Cd5494E69852bE8D9D23FE05Aab14b29B`
- Handles payment settlement and fee tracking
- Accumulates facilitator fees in `pendingFees` mapping

**TransferHook**: `0x081258287F692D61575387ee2a4075f34dd7Aef7`
- Default hook for transferring payments to merchants
- Supports simple and distributed transfers

### Block Explorer
https://www.oklink.com/xlayer

### Example Usage

```typescript
import { X402Client } from '@secured-finance/x402-client';
import { TransferHook, parseDefaultAssetAmount } from '@secured-finance/x402-core';

const client = new X402Client({
  wallet: extendedWallet,
  network: 'x-layer'
});

const amount = parseDefaultAssetAmount('1', 'x-layer'); // 1 USDC
await client.execute({
  hook: TransferHook.getAddress('x-layer'),
  hookData: TransferHook.encode(),
  amount,
  payTo: merchantAddress
});
```

---

## Base Sepolia (Testnet)

### Overview
- **Purpose**: Development and testing on Base network
- **Block Time**: ~2 seconds
- **Finality**: ~2 seconds
- **Gas**: Free (testnet)
- **Token**: USDC (6 decimals)

### Deployed Contracts

**SettlementRouter**: `0x817e4f0ee2fbdaac426f1178e149f7dc98873ecb`
- Handles payment settlement and fee tracking
- Accumulates facilitator fees in `pendingFees` mapping

**TransferHook**: `0x4DE234059C6CcC94B8fE1eb1BD24804794083569`
- Default hook for transferring payments to merchants
- Supports simple and distributed transfers

### Block Explorer
https://sepolia.basescan.org

### Get Testnet Tokens
- ETH: https://www.coinbase.com/faucets/base-ethereum-goerli-faucet
- USDC: Use Base Sepolia faucets

### Example Usage

```typescript
import { X402Client } from '@secured-finance/x402-client';
import { TransferHook, parseDefaultAssetAmount } from '@secured-finance/x402-core';

const client = new X402Client({
  wallet: extendedWallet,
  network: 'base-sepolia'
});

const amount = parseDefaultAssetAmount('0.01', 'base-sepolia');
await client.execute({
  hook: TransferHook.getAddress('base-sepolia'),
  hookData: TransferHook.encode(),
  amount,
  payTo: merchantAddress
});
```

---

## X-Layer Testnet

### Overview
- **Purpose**: Development and testing on X-Layer network
- **Block Time**: ~2 seconds
- **Finality**: ~2 seconds
- **Gas**: Free (testnet)
- **Token**: USDC (6 decimals)

### Deployed Contracts

**SettlementRouter**: `0xba9980fb08771e2fd10c17450f52d39bcb9ed576`
- Handles payment settlement and fee tracking
- Accumulates facilitator fees in `pendingFees` mapping

**TransferHook**: `0xD4b98dd614c1Ea472fC4547a5d2B93f3D3637BEE`
- Default hook for transferring payments to merchants
- Supports simple and distributed transfers

### Block Explorer
https://www.oklink.com/xlayer-test

### Get Testnet Tokens
- OKB: Use X-Layer testnet faucet
- USDC: Use X-Layer testnet faucets

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
import { paymentMiddleware } from '@secured-finance/x402-express';

app.get('/api/data', paymentMiddleware(
  merchantWallet,
  {
    'GET /api/data': {
      price: '$0.01',
      network: 'sepolia'
    }
  },
  { url: 'https://facilitator.x402x.dev' }
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
https://filecoin.blockscout.com

### Get Testnet Tokens
- tFIL: https://faucet.calibnet.chainsafe-fil.io
- USDFC: Use Calibration testnet faucet

### Example Usage

```typescript
import { paymentMiddleware } from '@secured-finance/x402-express';

app.post('/store-data', paymentMiddleware(
  merchantWallet,
  {
    'POST /store-data': {
      price: '$9.99',
      network: 'filecoin-calibration'
    }
  },
  { url: 'https://facilitator.x402x.dev' }
), async (req, res) => {
  const cid = await storeToFilecoin(req.body.data);
  res.json({ cid, status: 'stored' });
});
```

---

## Planned Networks

The following networks will be supported after security audits:

### Ethereum Mainnet
- **Tokens**: JPYC, USDC
- **Best for**: High-value B2B payments
- **Finality**: ~2 minutes
- **Status**: Planned after audit

### Polygon
- **Tokens**: JPYC, USDC
- **Best for**: Fast, low-cost micropayments
- **Finality**: ~5 seconds
- **Status**: Planned after audit

### Avalanche
- **Token**: USDC
- **Best for**: DeFi integrations
- **Finality**: ~2 seconds
- **Status**: Planned after audit

### Filecoin Mainnet
- **Token**: USDFC
- **Best for**: Storage payments, subscriptions
- **Finality**: ~60 seconds
- **Status**: Planned after audit

---

## Choosing a Network

**For development:**
- Use **Base Sepolia** or **X-Layer Testnet** for fast, low-cost testing
- Use **Sepolia** for Ethereum-compatible testing
- Use **Filecoin Calibration** for Filecoin-specific features

**For production:**
- Use **Base** or **X-Layer** for fast, low-cost payments
- Both networks offer ~2 second finality and low gas costs

**Network characteristics:**

| Characteristic | Base/X-Layer (Mainnet) | Base Sepolia | X-Layer Testnet | Sepolia | Filecoin Cal |
|----------------|----------------------|--------------|-----------------|---------|--------------|
| **Speed** | ~2s | ~2s | ~2s | ~2min | ~60s |
| **Token** | USDC | USDC | USDC | JPYC, USDC | USDFC |
| **Gas cost** | Low | Free | Free | Free | Low |
| **Best for** | Production | Fast testing | Fast testing | ETH testing | Storage |

---

## Network Configuration

The x402x packages automatically handle network configuration. Just specify the network name:

```typescript
import { getNetworkConfig } from '@secured-finance/x402-core';

// Get configuration for a network
const config = getNetworkConfig('base-sepolia');
console.log(config.settlementRouter); // '0x817e4f0ee2fbdaac426f1178e149f7dc98873ecb'
console.log(config.chainId); // 84532

// Or use in client
import { X402Client } from '@secured-finance/x402-client';

const client = new X402Client({
  wallet: extendedWallet,
  network: 'base-sepolia' // or 'base', 'x-layer', 'x-layer-testnet', etc.
});
```

Contract addresses, chain IDs, and default assets are built into `@secured-finance/x402-core`.

---

## Custom RPC Endpoints

For production facilitators, use custom RPC endpoints for better reliability:

```bash
# .env
BASE_RPC_URL=https://mainnet.base.org
X_LAYER_RPC_URL=https://rpc.xlayer.tech
BASE_SEPOLIA_RPC_URL=https://sepolia.base.org
X_LAYER_TESTNET_RPC_URL=https://testrpc.xlayer.tech
SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY
FILECOIN_CALIBRATION_RPC_URL=https://api.calibration.node.glif.io/rpc/v1
```

RPC providers:
- **Base**: Public RPC available at https://mainnet.base.org
- **X-Layer**: Public RPC available at https://rpc.xlayer.tech
- **Alchemy**: https://www.alchemy.com (for Ethereum networks)
- **Infura**: https://www.infura.io (for Ethereum networks)
- **Ankr**: https://www.ankr.com (multi-chain support)

---

## Related Resources

* **[Quick Start](../quick-start.md)** - Build your first paid API
* **[Facilitator Guide](facilitator-guide.md)** - Run your own facilitator
* **[Use Cases](use-cases.md)** - Example implementations
