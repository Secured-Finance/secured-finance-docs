---
description: How ZC bond positions are valued for P&L and LTV
---

# ⚖️ Mark to Market

Positions are valued at current market prices — not book value — for both P\&L display and [liquidation](./) LTV calculations. The reference price is called the **Mark Price**.

## How Mark Price is computed

The Mark Price is a **volume-weighted average price (VWAP) per block**, computed on a **Future Value basis**: each trade's contribution is weighted by what it will be worth at maturity, not just its present value. This matches the economics of discount instruments.

**Example** — two trades in one block:

| Trade     | PV amount | Price | FV amount    |
| --------- | --------- | ----- | ------------ |
| A         | 1,000     | 94.00 | 1,063.83     |
| B         | 1,000     | 92.00 | 1,086.96     |
| **Total** | **2,000** |       | **2,150.79** |

$$
\text{Mark Price} = \frac{\text{Total PV}}{\text{Total FV}} \times 100 = \frac{2{,}000}{2{,}150.79} \times 100 = 92.99
$$

(A naive price-weighted average would give 93.00 — the FV basis corrects for the discount structure.)

## Manipulation protection: minimum volume threshold

A block's trades only update the Mark Price if their volume meets a **minimum threshold** (currently 100 USD equivalent, reviewed periodically — see [Protocol Parameters](../../protocol-parameters.md)). Below the threshold, the previous valid Mark Price carries forward. This prevents dust trades from moving valuations that drive liquidations.

## Fallback waterfall

When no VWAP-eligible trades exist, the protocol falls back in strict order:

1. **Itayose opening price** — when a market has just opened
2. **Auto-roll price** — when no block price exists since the last roll
3. **Last traded price / VWAP without the volume threshold** — when no Mark Price has ever been set

This guarantees a valid valuation exists in every market at all times.

## Related

* [Liquidation](./) — where Mark Price is consumed
* [Auto-Roll Price Discovery](../auto-roll-price-discovery.md) — a related but distinct pricing process
* [Circuit Breaker](../../advanced-topics/circuit-breaker.md) — bounds the trades that feed the VWAP
