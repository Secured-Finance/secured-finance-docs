---
description: The order book interface for lending and borrowing
---

# Fixed Income (Trading)

The **Fixed Income** tab is the trading interface where you lend and borrow by trading Zero-Coupon bonds. If the terms *buy/sell* and *lend/borrow* feel interchangeable here, that's because they are:

| Action | Order book side | What it means |
| --- | --- | --- |
| **Lend** | Buy a ZC bond | Pay a discounted price now, hold a claim on face value (100) at maturity |
| **Borrow** | Sell a ZC bond | Receive funds now (requires collateral), owe face value at maturity |

<!-- screenshot: trading-interface -->

## Layout

* **Market selector** — currency and quarterly maturity (e.g. USDC DEC2026)
* **Order book** — live lend and borrow orders by price, with depth
* **Yield curve** — rates across all maturities for the selected currency
* **Order form** — side, order type, amount, price
* **Open Orders / Positions panel** — your resting orders and filled positions

## Placing an order

1. Choose the market (currency + maturity).
2. Choose **Lend** or **Borrow**. Borrowing requires deposited [collateral](../../core-concepts/collateral.md).
3. Choose the order type:
   * **Market order** — executes immediately at the best available price; pays the taker fee ([Fees](../../core-concepts/fees.md))
   * **Limit order** — executes only at your price or better. Volume that rests on the book pays **no fee**; if your price crosses existing orders, the part that fills immediately pays the taker fee ([Fees](../../core-concepts/fees.md))
4. Enter the amount. The form shows the implied APR, estimated fee, and (for borrows) collateral usage.
5. **Place Order** → confirm in your wallet.

Orders are matched by price-time priority, fully on-chain. Execution prices are bounded each block by the [Circuit Breaker](../../advanced-topics/circuit-breaker.md).

## Managing open orders

Unfilled or partially filled limit orders sit in **Open Orders**. You can cancel them anytime; funds allocated to unfilled orders return to your deposit balance. Order states (Open, Partially Filled, Filled, Killed, Blocked, Cancelled, Expired) are explained in [Order Life Cycle](../../core-concepts/order-life-cycle.md).

## Exiting a position

Use **Unwind** in the [Portfolio](portfolio.md) tab — see [Managing Your Positions](../managing-positions.md). At maturity, positions [auto-roll](../../core-concepts/fixed-maturity-and-auto-roll.md) into the nearest 3-month market; Auto-Roll is protocol-wide and has no user settings.

## Troubleshooting

* **Order not executing** — uncompetitive limit price or thin liquidity; adjust price or switch to a market order.
* **Insufficient collateral** — deposit more, reduce size, or check asset haircuts in [Protocol Parameters](../../protocol-parameters.md).
* **Order shows "Blocked"** — execution would breach the circuit breaker's per-block price range; retry in the next block or use a limit order.
