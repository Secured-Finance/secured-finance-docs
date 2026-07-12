---
description: How the Fixed-Rate Lending Protocol works
---

# Core Concepts

This section explains the mechanics of the protocol. If you read the pages in order, each builds on the last:

1. [**Zero-Coupon Bonds**](zero-coupon-bonds.md) — the instrument everything is built on: how a discounted price becomes a fixed rate
2. [**Order Book & Order Types**](order-book.md) — how lend and borrow orders meet, and when to use limit vs. market orders
3. [**Fixed Maturity & Auto-Roll**](fixed-maturity-and-auto-roll.md) — quarterly markets, and what happens to positions at maturity
4. [**Collateral**](collateral.md) — accepted assets per network, and how collateral secures loans
5. [**Liquidation**](liquidation/README.md) — what happens when collateral coverage falls short
6. [**Tokenization**](tokenization.md) — turning positions into transferable ERC-20 ZC Tokens
7. [**Fees**](fees.md) — the complete fee structure

## Terminology used throughout

| Term | Meaning |
| --- | --- |
| **Lend / Buy** | Buying a ZC bond at a discount — you are the lender |
| **Borrow / Sell** | Selling a ZC bond against collateral — you are the borrower |
| **Face value / Par** | 100 — the value every ZC bond reaches at maturity |
| **Unwind** | Closing a position by taking the opposite side in the same market |
| **Auto-Roll** | The protocol-wide mechanism that rolls matured positions into the nearest 3-month market |
| **Itayose** | The opening auction that sets a fair price when a new market starts |

All numeric parameters (fees, thresholds, limits) live in one place: [Protocol Parameters](../protocol-parameters.md).
