---
description: Fixed-rate, fixed-term lending and borrowing — fully on-chain
---

# Overview

## Why fixed rates?

In most DeFi lending markets, interest rates float block by block. That works for short-term liquidity, but it makes real financial planning impossible: a treasury can't budget borrowing costs, and an investor can't lock in a yield.

The **Fixed-Rate Lending Protocol** solves this with an instrument that traditional finance has used for centuries: the **Zero-Coupon (ZC) bond**. You buy a bond at a discount today and it is worth its full face value at maturity — the discount *is* your interest, fixed at the moment of the trade.

* **Lending = buying a ZC bond.** Pay 97.50 today, hold a claim worth 100 at maturity.
* **Borrowing = selling a ZC bond.** Receive 97.50 today against collateral, repay 100 at maturity.

All trades are matched on a **fully on-chain order book** — a rarity in DeFi, made economical by our gas-optimization architecture — with standardized quarterly maturities from 3 months to 2 years. The result is transparent price discovery and a genuine yield curve for crypto assets, live on **Ethereum, Arbitrum, and Filecoin**.

## How it works in five steps

1. **Deposit** assets into the protocol from the [app](https://app.secured.finance/).
2. **Choose a market**: a currency and a quarterly maturity (e.g. USDC DEC2026).
3. **Place an order**: Lend (buy) or Borrow (sell), as a limit or market order. Borrowers post [collateral](core-concepts/collateral.md) first.
4. **Hold or trade** your position. Positions can be unwound anytime, or tokenized as ERC-20 [ZC Tokens](core-concepts/tokenization.md).
5. **At maturity**, positions [auto-roll](core-concepts/fixed-maturity-and-auto-roll.md) into the next quarterly market — or unwind to withdraw your funds.

## Key advantages

* **Predictable returns** — rates are fixed for the full term at execution
* **On-chain transparency** — order matching, pricing, and settlement all happen in smart contracts
* **Capital efficiency** — multi-asset collateral, ZC bonds usable as collateral, partial liquidations
* **Composability** — tokenized positions travel across the DeFi ecosystem

## Where to go next

| Goal | Page |
| --- | --- |
| Lend and earn fixed yield | [Quick Start: Lend](getting-started/quick-start-lend.md) |
| Borrow at a fixed cost | [Quick Start: Borrow](getting-started/quick-start-borrow.md) |
| Understand the mechanics | [Core Concepts](core-concepts/README.md) |
| Look up any protocol number | [Protocol Parameters](protocol-parameters.md) |
| Study the architecture | [Advanced Topics](advanced-topics/README.md) |
| Verify contracts and audits | [Contracts & Security](contracts-and-security.md) |

{% hint style="info" %}
Secured Finance began at a 2020 hackathon with the goal of building an order-book-based rates market for DeFi. Read the background in [Research & Papers](research-and-papers.md).
{% endhint %}
