---
description: How lend and borrow orders meet — fully on-chain
---

# 🧩 Order Book & Order Types

Secured Finance runs a **fully on-chain order book** for every market (currency × maturity). An order book lists buy (lend) and sell (borrow) orders by price level, giving transparent price discovery and depth — the market structure used by traditional exchanges, rarely achieved on-chain because of gas costs.

{% hint style="info" %}
**Why is an on-chain order book hard?** Order data grows with every order, and Solidity storage is expensive. Most DeFi protocols use liquidity pools instead, but pool rates lack the transparency and composability of an order book. Secured Finance made the order book economical with Red-Black Trees and lazy evaluation — see the [Orderbook Deep Dive](../advanced-topics/orderbook-deep-dive/).
{% endhint %}

## The two sides

| Side              | Equivalent                     | What happens                                                                                           |
| ----------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **Lend (Buy)**    | Buying a ZC bond at a discount | You pay the discounted amount now; hold a claim on par (100) at maturity                               |
| **Borrow (Sell)** | Selling a ZC bond              | You receive the discounted amount now (after posting [collateral](collateral.md)); owe par at maturity |

Orders are matched by **price-time priority**: the best-priced orders fill first; at the same price, earlier orders fill first.

## Order types

### Limit orders

You specify the price (rate). The order executes at your price or better. Any remainder that does not execute rests on the book until filled, cancelled, or the market matures (unfilled orders expire at maturity and the allocated funds return to your deposit balance). A remainder stopped by insufficient liquidity or the [Circuit Breaker](../advanced-topics/circuit-breaker.md) instead terminates immediately and the funds return to your deposit balance — see [Order Life Cycle](order-life-cycle.md).

* Volume that rests on the book makes you a **maker**, adding liquidity — it pays **no trading fee**
* If your price overlaps existing orders, the overlapping part executes immediately. That portion makes you a **taker** and pays the [taker fee](fees.md); only the remainder rests on the book
* Orders cannot be modified — cancel and re-place to change price or size

### Market orders

You specify only the amount; the order executes immediately at the best available prices.

* You act as a **taker**, consuming liquidity — the taker fee applies ([Fees](fees.md))
* Execution is bounded by the [Circuit Breaker](../advanced-topics/circuit-breaker.md); portions that can't execute inside the allowed price range are killed
* If liquidity is insufficient, the order fills partially and the remainder is killed

### Which should I use?

| Priority                                     | Use              |
| -------------------------------------------- | ---------------- |
| Exact rate control, willing to wait (resting volume pays no fee)  | **Limit order**  |
| Immediate execution, accepting current rates | **Market order** |

## Worked example

A lender wants 2,000 USDC to earn at least 4% APR for 6 months:

1. Target price: 100 / (1 + 0.04 × 0.5) ≈ **98.04**
2. They place a **limit lend order** at 98.04 for 2,000 USDC.
3. When matched, they lend 2,000 USDC and open a lending position with a face value of approximately 2,039.98 USDC.
4. Held to maturity, the position earns approximately 39.98 USDC in fixed interest, with no trading fee because it was a limit order.

## Related

* [Order Life Cycle](order-life-cycle.md) — every state an order can be in, with examples
* [Zero-Coupon Bonds](zero-coupon-bonds.md) — price ↔ APR conversion
* [Itayose](../advanced-topics/itayose.md) — how prices are discovered when a market opens
