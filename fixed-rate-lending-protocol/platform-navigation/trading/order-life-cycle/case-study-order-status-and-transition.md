---
description: A Practical Walkthrough
---

# 💫 Case Study: Order Status & Transition

We'll explore the entire spectrum of order statuses through a detailed example, incorporating our platform's price range limit mechanism, [the Circuit Breaker](../../../protocol-security-and-safety/circuit-breaker/), for practical understanding.&#x20;

{% hint style="info" %}
For an in-depth understanding of the loan lifecycle, please visit the '[Order Life Cycle](./)' section.
{% endhint %}

## Order Status and Order Types

| Status \ Order Type   | Market Order                                                                        | Overlapping Limit Order                                                                           | Limit Order                                                                                                |
| --------------------- | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Open**              | <mark style="color:red;">Not applicable</mark>; enters immediate execution          | Rare; unless no overlapping order                                                                 | Waits for the market to reach the limit price                                                              |
| **Partially Filled**  | Only used as a combined state; no remaining orders (ex. Partially Filled & Blocked) | Partial execution if not enough liquidity; remains until further filled or terminated             | If the market reaches the limit price but not fully executable due to liquidity, stays until more activity |
| **Filled (Final)**    | Immediately fully executed at current market prices with sufficient liquidity       | Fully executed once the market fully meets the limit price                                        | Fully executed once the market fully meets the limit price                                                 |
| **Killed (Final)**    | Removed if cannot be fully executed due to lack of liquidity                        | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open          |
| **Blocked (Final)**   | Removed if cannot be fully executed due to circuit breakers                         | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open | <mark style="color:red;">Not applicable</mark>; remains in the market as Partially Filled or Open          |
| **Cancelled (Final)** | <mark style="color:red;">Not applicable</mark> as they are executed immediately     | Can be canceled before execution or after being Partially Filled                                  | Can be canceled at any point before being fully executed                                                   |
| **Expired (Final)**   | <mark style="color:red;">Not applicable</mark> as they are executed immediately     | Expires if not executed within a specific timeframe after being Partially Filled                  | Expires if the set timing (ex. maturity) passes without full execution                                     |

## Orderbook Scenario:

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

## Market Orders:

### Filled

* **Example**: Buy 10 at market.
* **Transition**: Order is **Filled** purchasing 10 units at 91.

### Partially Filled & Killed

* **Example**: Buy 20 at market.
* **Transition**: Order is **Partially Filled** with 10 units at 91, remaining 10 units are **Killed** due to lack of liquidity up to the upper limit.

### Partially Filled & Blocked

* **Example**: Sell 10 at market.
* **Transition**: Order is **Partially Filled** with 5 units at 89, remaining 5 units are **Blocked** then **Killed** due to no liquidity at the lower limit.

## Overlapping Limit Orders:

### Filled

* **Example**: Buy 10 at 91.
* **Transition**: Order is **Filled** with 10 units at 91.

### Partially Filled

* **Example**: Buy 15 at 93.
* **Transition**: Order is **Partially Filled** with 10 units at 93. Remaining 5 units are kept open at 93 but cannot be executed until the market moves and the circuit breaker price is adjusted to allow execution.

### Canceled

* **Example**: After being partially filled, cancel the remaining order.
* **Transition**: Remaining order is **Canceled**.

### Expired

* **Example**: Buy 15 at 91; remaining 5 units are kept open. Then no fill and lending market matures.
* **Transition**: Order **Expires** after the maturity time passes.

## Non-Overlapping Limit Orders:

### Open

* **Example**: Buy 10 at 89.
* **Transition**: Order is **Open**, awaiting a match.

### Partially Filled

* **Example**: Buy 10 at 89 (total 15 **Open** on the orderbook), then another trader sells 10 at 89.
* **Transition**: Order is **Partially Filled** with 5 units at 89, 5 units remain open.

### Canceled

* **Example**: After being partially filled, cancel the remaining order.
* **Transition**: Remaining order is **Canceled**.

### Expired

* **Example**: Buy 10 at 89, no fill and lending market matures.
* **Transition**: Order **Expires** after the maturity time passes.

