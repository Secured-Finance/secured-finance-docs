---
description: Traction, security, and technology — the three-minute read for investors, researchers, and partners
---

# Protocol at a Glance

## What Secured Finance is

Secured Finance operates two complementary DeFi protocols with a third product line built on top:

| Product | What it does | Networks |
| --- | --- | --- |
| **Fixed-Rate Lending** | Fully on-chain order book for fixed-rate, fixed-term lending via Zero-Coupon bonds | Ethereum, Arbitrum, Filecoin |
| **USDFC Stablecoin** | The first decentralized stablecoin fully collateralized by FIL | Filecoin (FVM) |
| **SF Yield Vault** | Curated yield strategies, including a JPYC fixed-income strategy | Ethereum |

## Traction

* **$50M+ cumulative volume** on the Fixed-Rate Lending apps (as of July 2026) — verified on [DefiLlama](https://defillama.com/protocol/dexs/secured-finance)
* Quarterly market launches (Itayose auctions + Auto-Roll) running continuously since mainnet, with [public reports every quarter](https://medium.com/secured-finance)
* **RWA collateral live**: the tokenized money-market fund uMINT is accepted as on-chain collateral on Ethereum (partnership with DigiFT, February 2026 — [announcement](https://medium.com/secured-finance/umint-as-eligible-on-chain-collateral-bringing-tokenized-money-markets-into-defi-financing-edfb46bf8346))
* **JPYC markets**: the first fixed-rate JPY-stablecoin lending markets, live on Ethereum (November 2025), plus a Yearn V3 JPYC strategy vault (2026 Q1)
* **x402-ready USDFC**: community-contributed EIP-3009 support merged and audited (2025 Q3), enabling x402 / HTTP 402 payment flows — gateway launch TBD

See the [Roadmap](roadmap/README.md) for the full delivery history.

## Why fixed rates matter

Most DeFi lending is variable-rate: yields change block by block, which makes planning impossible for treasuries, funds, and storage providers. Secured Finance brings the market structure of traditional fixed income on-chain — order-book price discovery, standardized quarterly maturities, and tradable Zero-Coupon bonds — so both sides of a loan know their exact rate for the entire term, and a genuine crypto yield curve emerges.

## Technical differentiation

* **Full on-chain order book** — made economical with Red-Black Trees, lazy evaluation, and Genesis Value accounting. [Deep dive](../fixed-rate-lending/advanced-topics/orderbook-deep-dive/README.md)
* **Composability** — lending positions can be tokenized as ERC-20 [ZC Tokens](../fixed-rate-lending/core-concepts/tokenization.md) and used across DeFi
* **Exchange-grade market safety** — [Itayose opening auctions](../fixed-rate-lending/advanced-topics/itayose.md), [circuit breakers](../fixed-rate-lending/advanced-topics/circuit-breaker.md), and [mark-to-market valuation](../fixed-rate-lending/core-concepts/liquidation/mark-to-market.md)

## Security

* **Audits**: Quantstamp (Fixed-Rate Lending, 2023 & 2024), Hexens and Decurity (USDFC, 2025) — reports in [Contracts & Security](../fixed-rate-lending/contracts-and-security.md)
* Active [Bug Bounty](../developer-portal/bug-bounty.md) program
* [Emergency Global Settlement](../fixed-rate-lending/advanced-topics/emergency-global-settlement.md) as a last-resort safeguard for user funds

## Where next

| You are… | Start here |
| --- | --- |
| New to the protocol | [Quick Start: Lend](../fixed-rate-lending/getting-started/quick-start-lend.md) |
| A borrower | [Quick Start: Borrow](../fixed-rate-lending/getting-started/quick-start-borrow.md) |
| Looking for passive yield | [SF Yield Vault: Getting Started](../yield-vault/getting-started/README.md) |
| A developer | [Developer Portal](../developer-portal/introduction.md) |
| A researcher or investor | [Research & Papers](../fixed-rate-lending/research-and-papers.md) · [Roadmap](roadmap/README.md) |
| Running a liquidation bot | [Liquidator's Guide](../fixed-rate-lending/core-concepts/liquidation/liquidators-guide.md) |
