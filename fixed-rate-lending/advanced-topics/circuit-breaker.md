---
description: Per-block price limits that blunt manipulation and flash-loan attacks
---

# Circuit Breaker

The Circuit Breaker limits how far prices can move **within a single block**, for both market and limit orders. Order volume that would execute outside the allowed range is [blocked](../core-concepts/order-life-cycle.md) rather than filled — an order executes up to the boundary and the remainder is killed. Because the limit binds per block, a flash-loan attacker cannot move the price dramatically inside one transaction — the core defense this mechanism provides.

## The three thresholds

| Rule | Value |
| --- | --- |
| Maximum **downward** move | 5% below the moving average of the last **5** reliable block prices |
| Maximum **upward** move | 10% above the moving average of the last **3** reliable block prices |
| Minimum allowance | The market may always move at least **2.00 down / 7.00 up** in absolute price, regardless of percentages |

Formally:

```text
Upper bound = Max( MA3 × 1.10, MA3 + 7.00 )   — capped at the maximum price of 100.00
Lower bound = Min( MA5 × 0.95, MA5 − 2.00 )
```

A taker order executes only at prices within these bounds. An order priced beyond a bound is not rejected outright — it fills **up to** the bound, and any remainder that would cross it is killed (shown as **Blocked** in the app).

The asymmetry (tighter downside) is deliberate: ZC bonds naturally drift **up** toward par as maturity approaches, so sharp downward moves are more likely to be anomalous — and downward spikes are what trigger unjust liquidations.

A **reliable block price** is a block VWAP that met the [minimum volume threshold](../core-concepts/liquidation/mark-to-market.md); low-volume blocks don't contaminate the moving averages.

## Worked examples

**Standard case:** last 5 reliable block prices 80.60, 80.40, 80.30, 80.10, 79.60.

* MA5 = 80.20 → lower bound = 80.20 × 0.95 = **76.19**
* MA3 = (80.30 + 80.10 + 79.60)/3 = 80.00 → upper bound = 80.00 × 1.10 = **88.00**
* Next block, orders execute only within 76.19–88.00.

**Low-price market (allowance kicks in):** MA5 = 16.00. The 5% rule would allow only −0.80, but the minimum downward allowance guarantees the market can move to 16.00 − 2.00 = **14.00**. Percentage limits never choke a low-priced book.

## What you'll see as a trader

* Typical orders execute normally — most users never notice the mechanism.
* A very large order may **partially fill** up to the boundary; the remainder is killed and shown as **Blocked** (or *Partially Filled & Blocked*) in the app.
* Blocked orders can simply be retried in a later block, or replaced with limit orders inside the range.

## Related

* [Order Life Cycle](../core-concepts/order-life-cycle.md) — Blocked/Killed states with examples
* [Mark to Market](../core-concepts/liquidation/mark-to-market.md) — reliable block prices
* [Protocol Parameters](../protocol-parameters.md) — current values
