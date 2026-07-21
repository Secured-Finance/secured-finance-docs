---
description: Monitor, adjust, and exit your lending and borrowing positions
---

# Managing Your Positions

## Viewing your positions

1. Open the [Portfolio](https://app.secured.finance/portfolio/) tab with your wallet connected.
2. **Active Positions** shows each position's asset, size, maturity, present value, and P&L.
3. **Open Orders**, **Order History**, and **My Transactions** cover everything that hasn't become (or is no longer) a position.

<!-- screenshot: portfolio-active-positions -->

## For borrowers: watch your collateral coverage

* Check the **collateral utilization / liquidation risk indicator** regularly — it moves from green to red as your Loan-to-Value ratio approaches the liquidation threshold ([current values](../protocol-parameters.md)).
* Remember that ZC bond prices move with interest rates: your debt's present value changes even when spot prices don't.
* To reduce risk, deposit more collateral, or reduce the borrow — unwind it, or place an opposite (lend) order for part of the amount. Details: [Liquidation](../core-concepts/liquidation/README.md).

## Adding to a position

1. Open the **Fixed Income** tab and select the same currency, maturity, and side (Lend/Borrow) as the existing position.
2. Place a new order for the additional amount — it merges into the same position.

## Reducing or closing a position

**Closing (Unwind)**

1. In **Portfolio → Active Positions**, click **Unwind** on the position.
2. The position is closed against the order book at the best available price. Review the estimated price and fee, then confirm — a taker fee applies ([Fees](../core-concepts/fees.md)).

**Reducing a position partially**

The Unwind action closes the whole position. To reduce it partially, place an **opposite order** for the amount you want to reduce (e.g. a lend order against a borrow position) in the same currency and maturity — filled amounts net against your position.

{% hint style="info" %}
Unwinding before maturity realizes the position at the *current* market price, which may be better or worse than holding to maturity, depending on how rates have moved.
{% endhint %}

## What happens at maturity

At maturity, every position is handled the same way — this is protocol-wide behavior, not a setting:

1. **Auto-Roll**: the position is automatically rolled into the nearest 3-month market at the [auto-roll price](../core-concepts/auto-roll-price-discovery.md). A roll fee applies ([Fees](../core-concepts/fees.md)).
2. **No automatic settlement**: the protocol never pushes funds back to your wallet. To exit, unwind the position (before or after maturity) and then withdraw.
3. **Liquidity note**: unwinding requires counterparties on the order book. In thin markets an unwind may only partially fill ([Order Life Cycle](../core-concepts/order-life-cycle.md)); you can retry later, or place an opposite limit order at your acceptable price.

More on the mechanics: [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md).

## Troubleshooting

* **Unwind not executing or only partially filling** — insufficient order-book liquidity within the allowed price range; retry in a later block, wait for liquidity, or place an opposite limit order at your acceptable price.
* **Values look stale** — refresh the page and confirm your wallet is on the right network.
* **Position missing after maturity** — it has rolled into the next maturity; look for the new maturity date in Active Positions.

## Related

* [Quick Start: Lend](quick-start-lend.md) · [Quick Start: Borrow](quick-start-borrow.md)
* [Tokenization](../core-concepts/tokenization.md) — move a position out as an ERC-20 token
* [Liquidation](../core-concepts/liquidation/README.md) — risk management for borrowers
