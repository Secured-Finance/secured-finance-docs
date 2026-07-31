---
description: Frequently asked questions about the Fixed-Rate Lending Protocol
---

# FAQs

## Platform basics

<details>

<summary>What is Secured Finance?</summary>

A DeFi platform for **fixed-rate, fixed-term lending and borrowing**, built on a fully on-chain order book and Zero-Coupon bonds, live on Ethereum, Arbitrum, and Filecoin. Secured Finance also operates the [USDFC stablecoin](../usdfc-stablecoin/overview.md) on Filecoin.

</details>

<details>

<summary>What is a Zero-Coupon (ZC) bond?</summary>

A debt instrument sold at a discount and worth its full face value (100) at maturity. Buy at 95, hold to maturity, receive 100 — the 5-point discount is your fixed interest. Details: [Zero-Coupon Bonds](core-concepts/zero-coupon-bonds.md).

</details>

<details>

<summary>What asset underlies each ZC bond?</summary>

The specific currency of that market: lending ETH in the DEC2026 market gives you a claim denominated in ETH (*ZC ETH DEC2026*). Each bond is asset-specific, maturity-specific, and can be [tokenized as an ERC-20](core-concepts/tokenization.md) for use across DeFi.

</details>

## Trading

<details>

<summary>Is my money locked until maturity?</summary>

No — there is no lock-up. Positions can be **unwound** (closed at the current market price) 24/7, subject to order-book liquidity. Lending positions can also be tokenized and transferred. Note the flip side: **exiting requires an action** — the protocol never auto-settles at maturity. See [Managing Your Positions](getting-started/managing-positions.md).

</details>

<details>

<summary>What happens to my position at maturity?</summary>

It **auto-rolls** into the nearest 3-month market at a fair roll price. Auto-Roll is protocol-wide — there are no settings to enable or disable. To receive your funds instead, unwind manually before or after maturity. See [Fixed Maturity & Auto-Roll](core-concepts/fixed-maturity-and-auto-roll.md).

</details>

<details>

<summary>What happens to my open orders at maturity?</summary>

Unfilled orders **expire** automatically and the allocated funds return to your deposit balance, ready to withdraw or reuse. Filled portions became positions and follow the Auto-Roll rules above.

</details>

<details>

<summary>Why is my unwind order "Blocked" or "Partially Blocked"?</summary>

Either the order book lacks matching liquidity, or execution would fall outside the [Circuit Breaker](advanced-topics/circuit-breaker.md)'s allowed price range for this block. Wait for liquidity and retry, or place an opposite **limit order** at your acceptable price — filled amounts net against your position. See [Order Life Cycle](core-concepts/order-life-cycle.md).

</details>

<details>

<summary>What fees do I pay?</summary>

Market orders pay a taker fee (1% p.a. prorated — 0.25% for 3 months). **Limit orders pay nothing.** Auto-Rolls charge the same rate as the taker fee each quarter. Liquidated borrowers pay a 7% liquidation fee. Full details: [Fees](core-concepts/fees.md) and [Protocol Parameters](protocol-parameters.md).

</details>

## Collateral & risk

<details>

<summary>Why do borrowers need collateral?</summary>

Collateral replaces credit checks: it protects lenders from default because under-collateralized positions are liquidated before losses reach lenders. See [Collateral](core-concepts/collateral.md).

</details>

<details>

<summary>Which assets can be collateral?</summary>

It varies by network — WBTC, ETH, USDC, and uMINT (RWA) on Ethereum; WBTC, ETH, and USDC on Arbitrum; FIL, iFIL, wpFIL, and USDFC on Filecoin. The authoritative list, with haircuts: [Protocol Parameters](protocol-parameters.md).

</details>

<details>

<summary>What happens if my collateral value falls?</summary>

Your LTV rises. At the liquidation threshold (80%), up to 50% of your debt can be liquidated with a 7% fee taken from collateral. Watch the risk indicator in [Portfolio](getting-started/platform-guide/portfolio.md) and add collateral or reduce debt early. See [Liquidation](core-concepts/liquidation/README.md).

</details>

## Advanced

<details>

<summary>What is Itayose?</summary>

The opening auction that sets a fair price whenever a new quarterly market launches: pre-open orders are collected for 7 days and matched simultaneously at the volume-maximizing price — with zero fees for filled pre-orders. See [Itayose](advanced-topics/itayose.md).

</details>

<details>

<summary>How can the order book be fully on-chain? Isn't that too expensive?</summary>

It's economical thanks to three techniques: Red-Black Trees for O(log n) order management, lazy evaluation to defer storage writes, and Genesis Value accounting to roll all positions with one update. See the [Orderbook Deep Dive](advanced-topics/orderbook-deep-dive/README.md).

</details>

<details>

<summary>Can I run a liquidation bot?</summary>

Yes — liquidation is permissionless and pays a 5% fee to the liquidator. Start with the [Liquidator's Guide](core-concepts/liquidation/liquidators-guide.md).

</details>

## Still stuck?

* Guides: [Getting Started](getting-started/README.md)
* Developers: [Developer Portal](../developer-portal/introduction.md)
* Community support: [Support & Contacts](../community/support-and-contacts.md)
