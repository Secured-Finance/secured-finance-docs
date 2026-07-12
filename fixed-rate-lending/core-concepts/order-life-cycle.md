---
description: Every state an order can be in, and how transitions happen
---

# Order Life Cycle

Track your orders' states in the **Order History** tab of the [Portfolio](../getting-started/platform-guide/portfolio.md) page. An order passes through one or more of seven states:

| State | Applies to | Meaning |
| --- | --- | --- |
| **Open** | Limit | Resting on the book, waiting for a match |
| **Partially Filled** | Both | Part executed; remainder open (limit) or terminated (market) |
| **Filled** *(final)* | Both | Fully executed — now a position |
| **Killed** *(final)* | Market | Could not fully execute due to insufficient liquidity |
| **Blocked** *(final)* | Market | Execution stopped by the [Circuit Breaker](../advanced-topics/circuit-breaker.md) price range |
| **Canceled** *(final)* | Limit | Canceled by you before full execution |
| **Expired** *(final)* | Limit | Reached its expiry or the market's maturity unfilled; allocated funds return to your deposit balance |

Combined states such as *Partially Filled & Killed* or *Partially Filled & Canceled* record that part of an order executed before the remainder terminated.

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
* *Buy 15 at 93* → fills 10; remaining 5 rest at 93 until the circuit-breaker range moves → **Partially Filled**, then later Filled / Canceled / Expired

**Limit orders (non-overlapping)**

* *Buy 10 at 89* → **Open**, waiting for a counterparty
* Market matures with the order unfilled → **Expired**, funds returned

## Common questions

<details>

<summary>What's the difference between Killed and Blocked?</summary>

**Killed** = not enough liquidity to fill the remainder. **Blocked** = the remainder would have executed outside the circuit breaker's allowed price range. Both are final states for market orders; the filled portion (if any) remains as a position.

</details>

<details>

<summary>What happens to open orders when the market matures?</summary>

They expire automatically and the allocated funds return to your deposit balance. Filled portions became positions and are subject to [Auto-Roll](fixed-maturity-and-auto-roll.md).

</details>

<details>

<summary>Can I modify an order?</summary>

No. Cancel the order and place a new one — this preserves fair price-time priority for everyone.

</details>
