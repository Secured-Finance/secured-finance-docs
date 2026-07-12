---
description: Quarterly markets, and exactly what happens to your position at maturity
---

# Fixed Maturity & Auto-Roll

## Quarterly markets

Each currency trades in **eight order books** at once, with maturities from 3 months to 2 years spaced 3 months apart. Maturity falls on the **last Friday of March, June, September, and December**, aligning with listed futures conventions so rates are easy to reference and hedge.

Markets are named by contract month: **DEC26** matures on the last Friday of December 2026.

Standardized maturities concentrate liquidity: instead of fragmenting orders across arbitrary dates, everyone trades the same eight points on the curve — which is also what makes a readable [yield curve](../getting-started/platform-guide/markets.md) possible.

<!-- screenshot/figure: fixed-maturity-orderbooks (redraw of former fixedmaturity.gif) -->

## The quarterly cycle

When the nearest market matures, three things happen at once:

1. The maturing order book is **deactivated** and recycled.
2. A **new 2-year order book** opens via the [Itayose](../advanced-topics/itayose.md) opening auction (pre-orders accepted for 7 days prior).
3. All positions in the matured market **Auto-Roll** into the nearest 3-month market.

Technical details of the rotation: [Orderbook Rotation](../advanced-topics/orderbook-deep-dive/orderbook-rotation.md).

## Auto-Roll

{% hint style="warning" %}
**Auto-Roll is protocol-wide.** Every matured position rolls automatically into the nearest 3-month market — it cannot be enabled, disabled, or configured per user. The protocol has **no automatic settlement**: to get funds back, [unwind](../getting-started/managing-positions.md) your position manually (possible before or after maturity).
{% endhint %}

### Why Auto-Roll exists

* **No reinvestment gap** — in traditional fixed income, a matured bond sits idle until you reinvest. Auto-Roll keeps capital working at a fair, close-to-mid price.
* **No counterparty hunt** — you don't need to find a new match on the order book at maturity.
* **Gas efficiency** — the roll is computed lazily via [Genesis Value accounting](../advanced-topics/orderbook-deep-dive/genesis-value-and-compound-factor.md), not per-position transactions.

### What it costs

Each roll charges the auto-roll fee (same rate as the taker fee, prorated — see [Fees](fees.md)), embedded in the roll price. The roll price itself is determined by a transparent waterfall — see [Auto-Roll Price Discovery](auto-roll-price-discovery.md).

### Worked example

1. In January, Alice lends 1,000 USDC in the MAR27 market (3-month maturity).
2. On the last Friday of March, MAR27 matures. Alice does nothing.
3. Her position rolls into **JUN27** — now the nearest 3-month market — at the auto-roll price, minus the roll fee.
4. If Alice wants her USDC instead, she unwinds the JUN27 position (or unwinds before the March maturity) and withdraws.

## Your choices at maturity

| You want to… | Action |
| --- | --- |
| Stay invested at the new market rate | Nothing — Auto-Roll continues each quarter |
| Exit | **Unwind** (before or after maturity), then withdraw |
| Choose a *different* maturity | Unwind, then place a new order in the market you prefer |
| Use the position elsewhere in DeFi | [Tokenize](tokenization.md) it as an ERC-20 ZC Token before maturity |

## Related

* [Auto-Roll Price Discovery](auto-roll-price-discovery.md) — how the roll price is set
* [Itayose](../advanced-topics/itayose.md) — how new markets open
* [Fees](fees.md) — roll fee details
