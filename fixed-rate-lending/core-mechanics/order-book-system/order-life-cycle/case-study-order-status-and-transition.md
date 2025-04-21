---
description: Understanding order statuses and transitions through practical examples in the Fixed-Rate Lending Protocol
icon: 💫
---

# 💫 Case Study: Order Status & Transition

## Overview

This case study explores the entire spectrum of order statuses through detailed examples, incorporating our platform's price range limit mechanism, [the Circuit Breaker](../../../../advanced-topics/safety-measures/circuit-breaker/README.md), for practical understanding.



## How It Works

{% hint style="info" %}
For an in-depth understanding of the loan lifecycle, please visit the '[Order Life Cycle](./README.md)' section.
{% endhint %}

### Order Status and Order Types

| Status \ Order Type   | Market Order                                                                        | Overlapping Limit Order                                                                           | Limit Order                                                                                                |
| --------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Open**              | <mark style="color:red;">Not applicable</mark>; enters immediate execution          | Rare; unless no overlapping order                                                                 | Waits for the market to reach the limit price                                                              |
| **Partially Filled**  | Only used as a combined state; no remaining orders (ex. Partially Filled & Blocked) | Partial execution if not enough liquidity; remains until further filled or terminated             | If the market reaches the limit price but not fully executable due to liquidity, stays until more activity |
| **Filled (Final)**    | Immediately fully executed at current market prices with sufficient liquidity       | Fully executed once the market fully meets the limit price                                        | Fully executed once the market fully meets the limit price                                                 |
| **Killed (Final)**    | Removed if cannot be fully executed due to lack of liquidity                        | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open          |
| **Blocked (Final)**   | Removed if cannot be fully executed due to circuit breakers                         | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open          |
| **Cancelled (Final)** | <mark style="color:red;">Not applicable</mark> as they are executed immediately     | Can be canceled before execution or after being Partially Filled                                  | Can be canceled at any point before being fully executed                                                   |
| **Expired (Final)**   | <mark style="color:red;">Not applicable</mark> as they are executed immediately     | Expires if not executed within a specific timeframe after being Partially Filled                  | Expires if the set timing (ex. maturity) passes without full execution                                     |

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Order Statuses | Possible states an order can be in | Open, Partially Filled, Filled, Killed, Blocked, Cancelled, Expired |
| Final Statuses | Order states that cannot transition further | Filled, Killed, Blocked, Cancelled, Expired |
| Circuit Breaker Range | Price range within which orders can be executed | ±2% from last price (in example) |
| Order Types | Types of orders that can be placed | Market, Limit (Overlapping and Non-Overlapping) |
| Order Sides | Sides of the orderbook | Buy (Lend), Sell (Borrow) |

### Orderbook Scenario

Our scenario unfolds within the bounds of an order book, structured around three key order types: 'Market Order', 'Overlapping Limit Order', and 'Non-Overlapping Limit Order'. Let's consider the following order book setup:

<pre><code><strong>Price | Amount
</strong>-------------
  93  |  0
  92  |  0     &#x3C;- Upper Circuit Breaker Limit
  91  |  10
  90  -- Last Price
  89  |  5
  88  |  0     &#x3C;- Lower Circuit Breaker Limit
  87  |  10
</code></pre>

## Examples

### Market Orders

#### Filled
* **Example**: Buy 10 at market.
* **Transition**: Order is **Filled** purchasing 10 units at 91.

#### Partially Filled & Killed
* **Example**: Buy 20 at market.
* **Transition**: Order is **Partially Filled** with 10 units at 91, remaining 10 units are **Killed** due to lack of liquidity up to the upper limit.

#### Partially Filled & Blocked
* **Example**: Sell 10 at market.
* **Transition**: Order is **Partially Filled** with 5 units at 89, remaining 5 units are **Blocked** then **Killed** due to no liquidity at the lower limit.

### Overlapping Limit Orders

#### Filled
* **Example**: Buy 10 at 91.
* **Transition**: Order is **Filled** with 10 units at 91.

#### Partially Filled
* **Example**: Buy 15 at 93.
* **Transition**: Order is **Partially Filled** with 10 units at 93. Remaining 5 units are kept open at 93 but cannot be executed until the market moves and the circuit breaker price is adjusted to allow execution.

#### Canceled
* **Example**: After being partially filled, cancel the remaining order.
* **Transition**: Remaining order is **Canceled**.

#### Expired
* **Example**: Buy 15 at 91; remaining 5 units are kept open. Then no fill and lending market matures.
* **Transition**: Order **Expires** after the maturity time passes.

### Non-Overlapping Limit Orders

#### Open
* **Example**: Buy 10 at 89.
* **Transition**: Order is **Open**, awaiting a match.

#### Partially Filled
* **Example**: Buy 10 at 89 (total 15 **Open** on the orderbook), then another trader sells 10 at 89.
* **Transition**: Order is **Partially Filled** with 5 units at 89, 5 units remain open.

#### Canceled
* **Example**: After being partially filled, cancel the remaining order.
* **Transition**: Remaining order is **Canceled**.

#### Expired
* **Example**: Buy 10 at 89, no fill and lending market matures.
* **Transition**: Order **Expires** after the maturity time passes.

## FAQ

### What happens to my order if it's partially filled?

When an order is partially filled, the filled portion becomes a position, while the unfilled portion remains in the orderbook as an open order. You can choose to leave it open, cancel it, or wait for it to be filled. For market orders, the unfilled portion may be killed or blocked depending on market conditions and circuit breaker limits.

### Why would my market order get blocked?

Market orders can be blocked when they would execute at a price outside the circuit breaker limits. This is a safety mechanism to prevent extreme price movements and protect the market from manipulation. When a market order is blocked, the unfilled portion is killed and removed from the orderbook.

### Can I modify an order that's already in the orderbook?

No, you cannot modify an existing order. If you want to change the price or amount, you'll need to cancel your existing order and place a new one with the updated parameters. This ensures price-time priority is maintained fairly in the orderbook.

### What's the difference between an order being killed versus blocked?

- **Killed**: An order is killed when there's insufficient liquidity to fill it completely. This typically happens with market orders when there are no more matching orders in the orderbook.
- **Blocked**: An order is blocked when its execution would violate the circuit breaker price limits. This is a safety mechanism to prevent extreme price volatility.

### What happens to my orders when a market matures?

Any open or partially filled orders in a market that reaches maturity will automatically expire. This means they are removed from the orderbook and will not be executed. Any filled portions of orders have already become positions and will be subject to the auto-rolling mechanism.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Order Statuses | Possible states an order can be in | Open, Partially Filled, Filled, Killed, Blocked, Cancelled, Expired |
| Final Statuses | Order states that cannot transition further | Filled, Killed, Blocked, Cancelled, Expired |
| Circuit Breaker Range | Price range within which orders can be executed | ±2% from last price (in example) |
| Order Types | Types of orders that can be placed | Market, Limit (Overlapping and Non-Overlapping) |
| Order Sides | Sides of the orderbook | Buy (Lend), Sell (Borrow) |

## Related Resources

- [Order Life Cycle](./README.md)
- [Order Types](../order-type.md)
- [Orderbook Mechanics](../../order-book-system.md)
- [Circuit Breaker](../../../../advanced-topics/safety-measures/circuit-breaker/README.md)
