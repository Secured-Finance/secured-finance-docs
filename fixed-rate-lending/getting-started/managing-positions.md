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
* To reduce risk, deposit more collateral or partially unwind the borrow position. Details: [Liquidation](../core-concepts/liquidation/README.md).

## Adding to a position

1. Open the **Trading** tab and select the same currency, maturity, and side (Lend/Borrow) as the existing position.
2. Place a new order for the additional amount — it merges into the same position.

## Reducing or closing a position (Unwind)

1. In **Portfolio → Active Positions**, click **Unwind** on the position.
2. Choose **Full** or **Partial**, and market or limit execution.
3. Review price, fee, and slippage, then confirm.

{% hint style="info" %}
Unwinding before maturity realizes the position at the *current* market price, which may be better or worse than holding to maturity, depending on how rates have moved.
{% endhint %}

## What happens at maturity

At maturity, every position is handled the same way — this is protocol-wide behavior, not a setting:

1. **Auto-Roll**: the position is automatically rolled into the nearest 3-month market at the [auto-roll price](../core-concepts/auto-roll-price-discovery.md). A roll fee applies ([Fees](../core-concepts/fees.md)).
2. **No automatic settlement**: the protocol never pushes funds back to your wallet. To exit, unwind the position (before or after maturity) and then withdraw.
3. **Liquidity note**: unwinding requires counterparties on the order book. In thin markets, a full unwind may take time or require a limit order.

More on the mechanics: [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md).

## Troubleshooting

* **Unwind order not executing** — insufficient order-book liquidity or an uncompetitive limit price; try a market unwind or adjust the price.
* **Values look stale** — refresh the page and confirm your wallet is on the right network.
* **Position missing after maturity** — it has rolled into the next maturity; look for the new maturity date in Active Positions.

## Related

* [Quick Start: Lend](quick-start-lend.md) · [Quick Start: Borrow](quick-start-borrow.md)
* [Tokenization](../core-concepts/tokenization.md) — move a position out as an ERC-20 token
* [Liquidation](../core-concepts/liquidation/README.md) — risk management for borrowers
