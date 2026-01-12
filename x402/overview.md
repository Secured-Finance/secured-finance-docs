---
description: Enable blockchain payments for APIs without gas fees
---

# What is x402-exec?

## The Problem: Gas Fees Kill Micropayments

Traditional blockchain payments require users to pay gas fees for every transaction. For a $0.01 API call, you might pay $0.50 in gas fees.

**Without x402-exec:**
- API call: $0.01
- Gas fee: $0.50
- Total: $0.51 (5000% markup)

## The Solution: Users Sign, Facilitators Pay Gas

x402-exec is a settlement framework that lets users pay for APIs by signing messages in their wallet—**no gas fees, no complexity**. A facilitator handles on-chain settlement through the SettlementRouter and earns fees for each transaction they process.

**With x402-exec:**
- API call: $0.01
- User signs (free, instant)
- Facilitator settles via SettlementRouter (pays gas, earns 0.3% fee)
- Hook executes business logic (transfer, mint NFT, distribute rewards)
- Merchant receives payment instantly

---

## How It Works

```
1. User requests /weather API
   ↓
2. Server returns: "402 Payment Required"
   ↓
3. User signs payment in wallet (free)
   ↓
4. Facilitator verifies & settles on-chain
   ↓
5. Server returns weather data
```

**Architecture:**
```
User Wallet → Middleware → Facilitator → SettlementRouter → Hook → Merchant
   (signs)    (verifies)   (settles)    (routes payment)  (logic)  (receives)
```

---

## Key Benefits

**For Users:**
- No gas fees—just sign a message
- Instant payments—no waiting for confirmations
- Works with any wallet (MetaMask, Coinbase Wallet, etc.)

**For Developers:**
- Easy integration—packages for Express, Hono, React, and more
- Flexible pricing—static or dynamic
- Multi-network support (Base, X-Layer live!)
- Programmable settlements through hooks

**For Facilitators:**
- Earn fees (0.3%, min $0.01) on payments you process
- Fees accumulate in SettlementRouter
- Claim accumulated fees anytime
- Open ecosystem—anyone can run one

---

## Supported Networks

x402-exec supports multiple networks with deployed SettlementRouter contracts for production and testing.

| Network | Token | Type | Purpose | Status |
|---------|-------|------|---------|--------|
| **Base** | USDC | Mainnet | Production payments | 🎉 Live |
| **X-Layer** | USDC | Mainnet | Production payments | 🎉 Live |
| **Base Sepolia** | USDC | Testnet | Development & testing | ✅ Active |
| **X-Layer Testnet** | USDC | Testnet | Development & testing | ✅ Active |
| **Sepolia** | JPYC, USDC | Testnet | Development & testing | ✅ Active |
| **Filecoin Calibration** | USDFC | Testnet | Development & testing | ✅ Active |

Other networks (Ethereum, Polygon, Avalanche, Filecoin) are planned after security audits.

📖 **[See Network Guide](guides/network-guide.md) for details**

---

## Deployed Contracts

### Base (Mainnet) 🎉
- **SettlementRouter**: `0x73fc659Cd5494E69852bE8D9D23FE05Aab14b29B`
- **TransferHook**: `0x081258287F692D61575387ee2a4075f34dd7Aef7`

### X-Layer (Mainnet) 🎉
- **SettlementRouter**: `0x73fc659Cd5494E69852bE8D9D23FE05Aab14b29B`
- **TransferHook**: `0x081258287F692D61575387ee2a4075f34dd7Aef7`

### Base Sepolia (Testnet)
- **SettlementRouter**: `0x817e4f0ee2fbdaac426f1178e149f7dc98873ecb`
- **TransferHook**: `0x4DE234059C6CcC94B8fE1eb1BD24804794083569`

### X-Layer Testnet
- **SettlementRouter**: `0xba9980fb08771e2fd10c17450f52d39bcb9ed576`
- **TransferHook**: `0xD4b98dd614c1Ea472fC4547a5d2B93f3D3637BEE`

### Sepolia (Testnet)
- **SettlementRouter**: `0x876308C01deCdbae46E353C81d869f102Ec1DFB3`
- **TransferHook**: `0x884B29Ee0BdDdFD262990f720D7387611a1be50c`
- **JPYC Token**: `0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29`
- **USDC Token**: `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238`

### Filecoin Calibration (Testnet)
- **SettlementRouter**: `0xf9EF447517d15c503cfE3328b841441b878672A3`
- **TransferHook**: `0xcab270aD54C7ACc89F2545e4E29e1FDa2Ee0651f`
- **USDFC Token**: `0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0`

---

## Get Started

### Add Payments to Your API
Install packages for your framework:

```bash
npm install @secured-finance/x402-express  # Express.js
npm install @secured-finance/x402-hono     # Hono (Edge/Workers)
npm install @secured-finance/x402-client   # Client SDK (React, Vue, etc.)
npm install @secured-finance/x402-react    # React hooks
```

👉 **[Quick Start Guide](quick-start.md)**

### Try the Live Demo
See working examples with revenue splits, NFT minting, and loyalty rewards:

👉 **[Live Demo](https://demo.x402x.dev)**

### Use a Facilitator Node
Use the default facilitator to verify and settle payments—no setup required.

👉 **[Using the Facilitator](guides/using-facilitator.md)**

### Run Your Own Facilitator
Deploy your own facilitator node to earn fees (0.3%) on payments you process.

👉 **[Facilitator Guide](guides/facilitator-guide.md)**

---

## Resources

* **[Quick Start](quick-start.md)** - Build your first paid API
* **[Live Demo](https://demo.x402x.dev)** - See working examples
* **[Network Guide](guides/network-guide.md)** - Network details and contract addresses
* **[Use Cases](guides/use-cases.md)** - Example implementations
* **[Package Docs](packages/README.md)** - Complete API reference
* **[GitHub](https://github.com/Secured-Finance/x402-exec)** - Full source code

---

**Ready to start?** → [Quick Start Guide](quick-start.md) or [Try the Demo](https://demo.x402x.dev)
