---
description: Enable blockchain payments for APIs without gas fees
---

# 📢 What is X402?

## The Problem: Gas Fees Kill Micropayments

Traditional blockchain payments require users to pay gas fees for every transaction. For a $0.01 API call, you might pay $0.50 in gas fees. This makes micropayments completely impractical.

**Example without X402:**
- User wants premium weather data: $0.01
- Gas fee to send USDC: $0.50
- Total cost: $0.51 (5000% markup!)
- Result: ❌ Users give up

## The Solution: Users Sign, Facilitators Pay Gas

X402 is a payment protocol that allows users to pay for API access by signing messages in their wallet - **no gas fees, no blockchain complexity**. A facilitator service handles the on-chain settlement and earns a 0.3% fee automatically.

**Example with X402:**
- User wants premium weather data: $0.01
- User signs message in wallet (free)
- Facilitator pays gas fee and settles on-chain
- Facilitator earns: $0.00003 (0.3% fee)
- User pays: $0.01 total
- Result: ✅ Seamless payment

---

## How It Works

### Simple 6-Step Flow

```
1. User requests /weather API
   ↓
2. Server returns: "402 Payment Required"
   ↓
3. User's wallet prompts: "Sign payment for $0.01"
   ↓
4. User signs message (free, instant)
   ↓
5. Facilitator verifies signature & settles on-chain
   ↓
6. Server returns weather data
```

### Architecture Diagram

```
┌─────────┐         ┌──────────────┐         ┌─────────────┐         ┌────────────┐
│  User   │────────▶│  Middleware  │────────▶│ Facilitator │────────▶│ Blockchain │
│ Wallet  │         │ (Your Server)│         │   Service   │         │   (USDC)   │
└─────────┘         └──────────────┘         └─────────────┘         └────────────┘
    │                      │                        │                       │
    │ Signs payment        │ Verifies payment       │ Settles on-chain      │
    │ (EIP-712)            │ with facilitator       │ (pays gas)            │
    │                      │                        │                       │
    └──────────────────────┴────────────────────────┴───────────────────────┘
                          Payment confirmed, content delivered
```

---

## Key Benefits

### For Users
- ✅ **No gas fees** - Just sign a message in your wallet
- ✅ **Instant payments** - No waiting for blockchain confirmations
- ✅ **Any wallet works** - MetaMask, Coinbase Wallet, WalletConnect
- ✅ **Micropayments enabled** - Pay $0.01 for API calls

### For Developers
- ✅ **Easy integration** - One line of middleware code
- ✅ **Easy integration** - Express, Next.js, or build custom
- ✅ **Flexible pricing** - Static or dynamic pricing based on usage
- ✅ **Multiple networks** - Filecoin, Polygon, Ethereum, Base

### For Facilitator Operators
- ✅ **Earn 0.3% fees** - Automatic revenue on every payment
- ✅ **Fully automated** - On-chain fee splitting via FeeReceiver contract
- ✅ **Scalable** - Process thousands of payments per day
- ✅ **Open ecosystem** - Anyone can run a facilitator

---

## Core Concepts

### Payment Payload
A signed message containing payment details (amount, recipient, deadline, signature). This is what users sign in their wallet.

```typescript
{
  from: "0xUserWallet",
  to: "0xMerchantWallet",
  value: "1000000", // 1.00 USDC (6 decimals)
  validAfter: 0,
  validBefore: 1700000000,
  nonce: "random123",
  signature: "0xSignedByUser..."
}
```

### Payment Requirements
What the API endpoint requires for access (price, network, token).

```typescript
{
  price: "$0.01",
  network: "polygon",
  token: "JPYC"
}
```

### Facilitator
A service that verifies payment signatures and settles transactions on-chain. Facilitators pay gas fees and earn 0.3% fees automatically.

### FeeReceiver Contract
Smart contract that automatically splits payments:
- 99.7% → Merchant (your wallet)
- 0.3% → Facilitator (gas coverage + profit)

**Example:**
- User pays: $10.00 USDC
- Merchant receives: $9.97
- Facilitator receives: $0.03
- All automatic, on-chain, trustless

---

## Supported Networks & Tokens

### Primary Tokens

| Network | Token | Decimals | Finality | Best For |
|---------|-------|----------|----------|----------|
| **Sepolia** (testnet) | JPYC | 18 | ~2min | Development & testing |
| **Ethereum/Polygon** | JPYC | 18 | ~5s-2min | E-commerce, games, instant payments |
| **Filecoin Calibration** (testnet) | USDFC | 18 | ~60s | Development & testing |
| **Filecoin** (mainnet) | USDFC | 18 | ~60s | Subscriptions, storage, AI jobs |

### Additional Networks

| Network | Token | Decimals | Finality | Best For |
|---------|-------|----------|----------|----------|
| **Base** | USDC | 6 | ~2s | Creator tips, onchain apps |
| **Ethereum** | USDC | 6 | ~2min | B2B, high-value settlements |

📖 **See [Network Guide](network-guide.md)** for detailed use cases

---

## When to Use X402

### ✅ Perfect For:
- **Micropayments** - Payments under $10
- **Pay-per-use APIs** - Weather, AI, data feeds
- **Content paywalls** - Premium articles, videos
- **Subscription billing** - Monthly/weekly recurring
- **In-app purchases** - Game items, virtual goods
- **Storage payments** - Filecoin storage deals

### ❌ Not Ideal For:
- **Free APIs** - No payment needed
- **Very high-value B2C** - Credit cards may offer better UX
- **Traditional banks** - Require fiat on/off ramps
- **Non-EIP-3009 tokens** - X402 requires transferWithAuthorization

---

## Technical Foundation

### EIP-3009: transferWithAuthorization
X402 uses [EIP-3009](https://eips.ethereum.org/EIPS/eip-3009) which allows users to sign payment authorizations off-chain. The facilitator then executes the transfer on-chain.

**Key advantages:**
- Users don't need ETH/FIL for gas
- Gasless for end users
- Nonce-based replay protection
- Supports USDC, JPYC, USDFC (all EIP-3009 compatible)

### Security Features
- ✅ **Signature verification** - Only valid signatures accepted
- ✅ **Nonce replay protection** - Each payment used once
- ✅ **Deadline enforcement** - Payments expire after timeout
- ✅ **Balance checks** - Users must have sufficient funds
- ✅ **On-chain settlement** - Trustless, auditable payments

---

## Quick Start

Ready to integrate X402? Choose your path:

### For Developers (Add Payments to Your API)
1. **Install package**: `pnpm add @secured-finance/sf-x402-express`
2. **Add middleware**: One line of code
3. **Test locally**: Make your first paid API call

👉 **[Quick Start Guide](quick-start.md)**

### For Facilitator Operators (Earn Fees)
1. **Deploy facilitator**: 15-minute setup
2. **Configure networks**: Sepolia, Polygon, Filecoin
3. **Start earning**: 0.3% on every payment

👉 **[Facilitator Guide](guides/facilitator-guide.md)**

### For Users (Make Payments)
1. **Connect wallet**: MetaMask or Coinbase Wallet
2. **Sign payment**: Click "Confirm" in wallet popup
3. **Access content**: Instant delivery after payment

---


---

## Published Packages

| Package | Description | Use Case |
|---------|-------------|----------|
| `@secured-finance/sf-x402` | Core library | Build facilitators, verify & settle payments |
| `@secured-finance/sf-x402-express` | Express middleware | Express.js applications |
| `@secured-finance/sf-x402-next` | Next.js middleware | Next.js applications (App/Pages Router) |

📦 **[Package Documentation](packages/README.md)**

---

## Related Resources

* [Network Guide](guides/network-guide.md) - Choose the right network
* [Quick Start](quick-start.md) - Build your first paid API
* [Use Cases](guides/use-cases.md) - Real-world examples
* [Facilitator Guide](guides/facilitator-guide.md) - Deploy and earn fees
* [Package Documentation](packages/README.md) - Complete package docs

## Community & Support

* 💬 [Discord](https://discord.gg/securedfinance) - Get help from the community
* 🐛 [GitHub Issues](https://github.com/Secured-Finance/x402/issues) - Report bugs
* 📖 [Examples](https://github.com/Secured-Finance/x402/tree/main/examples) - See working code
* 🐦 [Twitter](https://twitter.com/securedfinance) - Stay updated

---

**Ready to get started?** Head to the [Quick Start Guide](quick-start.md) →
