---
description: Enable blockchain payments for APIs without gas fees
---

# What is X402?

## The Problem: Gas Fees Kill Micropayments

Traditional blockchain payments require users to pay gas fees for every transaction. For a $0.01 API call, you might pay $0.50 in gas fees.

**Without X402:**
- API call: $0.01
- Gas fee: $0.50
- Total: $0.51 (5000% markup)

## The Solution: Users Sign, Facilitators Pay Gas

X402 lets users pay for APIs by signing messages in their wallet—**no gas fees, no complexity**. A facilitator handles on-chain settlement and earns fees for each transaction they process.

**With X402:**
- API call: $0.01
- User signs (free, instant)
- Facilitator settles on-chain (pays gas, earns fee)
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
User Wallet → Middleware → Facilitator → Blockchain
   (signs)    (verifies)   (settles)    (confirms)
```

---

## Key Benefits

**For Users:**
- No gas fees—just sign a message
- Instant payments—no waiting for confirmations
- Works with any wallet (MetaMask, Coinbase Wallet, etc.)

**For Developers:**
- Easy integration—one line of middleware
- Flexible pricing—static or dynamic
- Multi-network support

**For Facilitators:**
- Earn fees on payments you process
- Set your own fee structure
- Claim accumulated fees anytime
- Open ecosystem—anyone can run one

---

## Supported Networks

X402 currently supports **Sepolia** and **Filecoin Calibration** testnets with deployed contracts.

| Network | Token | Type | Purpose |
|---------|-------|------|---------|
| **Sepolia** | JPYC, USDC | Testnet | Development & testing |
| **Filecoin Calibration** | USDFC | Testnet | Development & testing |

Other networks (Ethereum, Polygon, Base, Avalanche) are supported by the protocol but don't have settlement contracts deployed yet.

📖 **[See Network Guide](guides/network-guide.md) for details**

---

## Deployed Contracts

### Sepolia (Chain ID: 11155111)
- **SettlementRouter**: `0x876308C01deCdbae46E353C81d869f102Ec1DFB3`
- **TransferHook**: `0x884B29Ee0BdDdFD262990f720D7387611a1be50c`
- **JPYC Token**: `0xE7C3D8C9a439feDe00D2600032D5dB0Be71C3c29`
- **USDC Token**: `0x1c7D4B196Cb0C7B01d743Fbc6116a902379C7238`

### Filecoin Calibration (Chain ID: 314159)
- **SettlementRouter**: `0xf9EF447517d15c503cfE3328b841441b878672A3`
- **TransferHook**: `0xcab270aD54C7ACc89F2545e4E29e1FDa2Ee0651f`
- **USDFC Token**: `0xb3042734b608a1B16e9e86B374A3f3e389B4cDf0`

---

## Get Started

### Add Payments to Your API
Install the middleware package for your framework:

```bash
pnpm add @secured-finance/sf-x402-express  # Express.js
pnpm add @secured-finance/sf-x402-next     # Next.js
```

👉 **[Quick Start Guide](quick-start.md)**

### Use a Facilitator Node
Use Secured Finance's default facilitator to verify and settle payments—no setup required.

👉 **[Using the Facilitator](guides/using-facilitator.md)**

### Run Your Own Facilitator
Deploy your own facilitator node to earn fees on payments you process.

👉 **[Facilitator Guide](guides/facilitator-guide.md)**

---

## Resources

* **[Quick Start](quick-start.md)** - Build your first paid API
* **[Network Guide](guides/network-guide.md)** - Network details and contract info
* **[Use Cases](guides/use-cases.md)** - Example implementations
* **[Package Docs](packages/README.md)** - Complete API reference

---

**Ready to start?** → [Quick Start Guide](quick-start.md)
