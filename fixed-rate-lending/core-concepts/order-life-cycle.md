---
description: Every state an order can be in, and how transitions happen
---

# Order Life Cycle

Track your orders' states in the **Order History** tab of the [Portfolio](../getting-started/platform-guide/portfolio.md) page. An order passes through one or more of seven states:

| State | Applies to | Meaning |
| --- | --- | --- |
| **Open** | Limit | Resting on the book, waiting for a match |
| **Partially Filled** | Both | Part executed; remainder rests (limit priced inside the circuit-breaker range) or is terminated (market, or limit priced beyond the range) |
| **Filled** *(final)* | Both | Fully executed — now a position |
| **Killed** *(final)* | Market / crossing limit | Could not fully execute due to insufficient liquidity |
| **Blocked** *(final)* | Market / crossing limit | Execution stopped by the [Circuit Breaker](../advanced-topics/circuit-breaker.md) price range |
| **Cancelled** *(final)* | Limit | Cancelled by you before full execution |
| **Expired** *(final)* | Limit | Still unfilled when the market reached maturity; allocated funds return to your deposit balance |

Combined states such as *Partially Filled & Killed* or *Partially Filled & Cancelled* record that part of an order executed before the remainder terminated.

<figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption><p>Order status transitions</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption><p>Behind the scenes: a filled order becomes a position (Future Value), and an auto-rolled position is tracked in <a href="../advanced-topics/orderbook-deep-dive/genesis-value-and-compound-factor.md">Genesis Value</a> terms</p></figcaption></figure>

## Scenario walkthrough

Consider this order book (last price 90; circuit-breaker range for the next block: 88–92, simplified for illustration):

```
Price | Amount
---------------
  93  |  0
  92  |  0     <- upper limit (this block)
  91  |  10
  90  -- last price
  89  |  5
  88  |  0     <- lower limit (this block)
  87  |  10
```

**Market orders**

* *Buy 10 at market* → fills 10 at 91 → **Filled**
* *Buy 20 at market* → fills 10 at 91; no more liquidity within the limit → **Partially Filled & Killed**
* *Sell 10 at market* → fills 5 at 89; the rest would execute below the lower limit → **Partially Filled & Blocked**

**Limit orders (overlapping — price crosses existing orders)**

* *Buy 10 at 91* → **Filled** immediately
* *Buy 15 at 92* (at the upper limit) → fills 10 at 91; the remaining 5 rest on the book at 92 → **Partially Filled**, then later Filled / Cancelled / Expired
* *Buy 15 at 93* (beyond the upper limit) → fills 10 at 91; the remaining 5 would execute beyond the circuit-breaker limit, so they are **blocked** and the allocated funds return to your deposit balance → **Partially Filled & Blocked**

**Limit orders (non-overlapping)**

* *Buy 10 at 89* → **Open**, waiting for a counterparty
* Market matures with the order unfilled → **Expired**, funds returned

## Common questions

<details>

<summary>What's the difference between Killed and Blocked?</summary>

**Killed** = not enough liquidity to fill the remainder. **Blocked** = the remainder would have executed outside the circuit breaker's allowed price range. Both are final states for the taker side of an execution — market orders, or limit orders that cross the book; the filled portion (if any) remains as a position.

</details>

<details>

<summary>What happens to open orders when the market matures?</summary>

They expire automatically and the allocated funds return to your deposit balance. Filled portions become positions and are subject to [Auto-Roll](fixed-maturity-and-auto-roll.md).

</details>

<details>

<summary>Can I modify an order?</summary>

No. Cancel the order and place a new one — this preserves fair price-time priority for everyone.

</details>
