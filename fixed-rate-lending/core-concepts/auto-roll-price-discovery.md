---
description: >-
  How the quarterly roll price is determined — fairly, in any liquidity
  condition
---

# 💰 Auto-Roll Price Discovery

The auto-roll price determines the rate at which matured positions roll into the nearest 3-month market. It is calculated by a **waterfall** designed to produce a fair, manipulation-resistant price whatever the liquidity conditions:

| Condition                                 | Price source                                                                            |
| ----------------------------------------- | --------------------------------------------------------------------------------------- |
| **Normal liquidity**                      | Volume-weighted average price (VWAP) of trades in the **6-hour window** before maturity |
| **No trades in the window**               | Current **Mark Price**, adjusted for duration                                           |
| **No trades for 3 months**                | The **previous roll price**                                                             |
| **First roll of a new market, no trades** | The market's **opening price**, adjusted for duration                                   |

## Example (normal conditions)

Trades in the 6-hour window before a market matures:

| Volume (USDC) | Price |
| ------------- | ----- |
| 10,000        | 99.20 |
| 25,000        | 99.15 |
| 15,000        | 99.25 |

$$
\text{VWAP} = \frac{10{,}000 \times 99.20 + 25{,}000 \times 99.15 + 15{,}000 \times 99.25}{50{,}000} = 99.19
$$

Positions roll at 99.19 (before the roll fee — see [Fees](fees.md)).

## Manipulation resistance

* The **6-hour window** makes it expensive to hold prices at an artificial level long enough to matter.
* **Volume weighting** means influencing the price requires real size, at real risk.
* The fallbacks (Mark Price, previous roll) are themselves protected by the [minimum volume threshold](liquidation/mark-to-market.md) and the [Circuit Breaker](../advanced-topics/circuit-breaker.md).

## Related

* [Fixed Maturity & Auto-Roll](fixed-maturity-and-auto-roll.md) — the roll mechanism itself
* [Mark to Market](liquidation/mark-to-market.md) — how Mark Price is computed
* [Genesis Value & Compound Factor](../advanced-topics/orderbook-deep-dive/genesis-value-and-compound-factor.md) — how rolls are applied without per-position gas costs
