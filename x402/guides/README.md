---
description: In-depth guides for implementing x402x payments
---

# 📖 Guides

Comprehensive guides to help you implement, optimize, and operate x402x payment infrastructure.

---

## Available Guides

### [🌍 Network Guide](network-guide.md)
**Choose the right blockchain network for your use case**

Different networks are optimized for different payment scenarios. Learn about:
- **Mainnet deployments**: Base and X-Layer (Live!)
- **Testnet networks**: Base Sepolia, X-Layer Testnet, SKALE, Sepolia, Filecoin Calibration
- SettlementRouter and TransferHook contract addresses
- Transaction finality and settlement speed
- Gas costs and economics
- Token support (USDC, JPYC, USDFC)

[**Read Network Guide →**](network-guide.md)

---

### [💡 Use Cases](use-cases.md)
**Real-world examples and implementation patterns**

Learn from complete, production-ready examples:
- Micropayments (pay-per-request APIs, content paywalls)
- Subscriptions (monthly billing, storage payments)
- Programmable settlements (revenue splits, NFT minting, rewards)
- Dynamic pricing (usage-based calculations)

**Live demo**: https://demo.x402x.dev

[**View Use Cases →**](use-cases.md)

---

### [🏦 Facilitator Guide](facilitator-guide.md)
**Build and operate your own facilitator service**

Facilitators verify and settle payments via SettlementRouter, earning fees on transactions they process. Learn how to:
- Build a facilitator service with @secured-finance/x402-core
- Integrate with SettlementRouter
- Deploy to production
- Claim accumulated fees from SettlementRouter
- Monitor and maintain

[**Read Facilitator Guide →**](facilitator-guide.md)

---

## Getting Started

New to x402x? Start here:

1. **Understand the basics** - [What is x402x?](../overview.md)
2. **Build your first API** - [Quick Start Guide](../quick-start.md)
3. **Choose your network** - [Network Guide](network-guide.md) (Base & X-Layer live!)
4. **See live demo** - https://demo.x402x.dev
5. **Explore examples** - [Use Cases](use-cases.md)

---

## Need Help?

* [📦 Package Documentation](../packages/README.md) - API reference for all x402x packages
* [🚀 Quick Start](../quick-start.md) - Get started in 10 minutes
* [🎉 Live Demo](https://demo.x402x.dev) - See working examples
* [💬 Discord](https://discord.gg/securedfinance) - Community support
* [🐛 GitHub Issues](https://github.com/Secured-Finance/x402-exec/issues) - Report bugs
