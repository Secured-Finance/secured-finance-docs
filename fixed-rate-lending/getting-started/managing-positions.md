---
description: Monitor, adjust, and exit your lending and borrowing positions
---

# 📈 Managing Your Positions

## Viewing your positions

1. Open the [Portfolio](https://app.secured.finance/portfolio/) tab with your wallet connected.
2. Active Positions shows each position’s asset, size, maturity, present value (PV: value at current prices), and profit or loss (P\&L).
3. **Open Orders** shows live order remainders that can still fill. **Order History** shows order outcomes and filled amounts. **My Transactions** records protocol activity; history entries can relate to positions that are still open.

## What happens at maturity

For supported markets, open positions continue through Auto-Roll at maturity. This is protocol-wide behavior, not a user setting:

1. **Auto-Roll**: the position is automatically rolled into the nearest 3-month market at the [auto-roll price](../core-concepts/auto-roll-price-discovery.md). A roll fee applies ([Fees](../core-concepts/fees.md)).
2. **No automatic settlement**: maturity does not automatically settle your position or pay funds to your wallet. To exit, unwind it before or after maturity, verify what executed, then withdraw available funds.
3. **Exit liquidity:** closing in full requires enough matching orders within the protocol’s price limits. Any unclosed amount stays open. See [Order Life Cycle](../core-concepts/order-life-cycle.md).

More on the mechanics: [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md).

## For borrowers: watch your collateral coverage

* The app uses three labels: Collateral Usage in the order review, and Collateral Utilization and Liquidation Risk in Portfolio. Usage and Utilization show how much collateral capacity is in use; Liquidation Risk shows how close the account is to liquidation.
* These indicators are not loan-to-value (LTV), the ratio of debt value to collateral value. For the protocol’s valuation rules, haircuts and thresholds, see [Liquidation](../core-concepts/liquidation/) and [Protocol Parameters](../protocol-parameters.md).
* Remember that ZC bond prices move with interest rates: your debt's present value changes even when spot prices don't.
* To reduce risk, deposit more collateral, or reduce the borrow — unwind it, or place an opposite (lend) order for part of the amount. Details: [Liquidation](../core-concepts/liquidation/).

## Adding to a position

1. Open the **Fixed Income** tab and select the same currency, maturity, and side (Lend/Borrow) as the existing position.
2. Place a new order for the additional amount. Only executed amounts increase the position; an unfilled limit-order remainder stays in **Open Orders** and can fill later.

## Reducing or closing a position

**Closing the whole position (Unwind)**

Unwind places an opposite trade for your whole current position.

**Borrowers:** Unwind spends the borrowed currency already deposited in the protocol. Check the current quote and fee, and deposit more of that currency first if needed. Tokens held only in your external wallet are not automatically deposited by this action. Keep native tokens in the wallet for gas.

1. In **Portfolio → Active Positions**, select Unwind and review the **Unwind Position** dialog. Its **Cancel** button only dismisses the dialog before submission; it does not close the position or cancel an open order.
2. Review the estimated price and fee, then confirm. The protocol can stop matching at its price limits, so Unwind may close all, some or none of the position. A taker fee applies to the executed amount ([Fees](../core-concepts/fees.md)).
3. After confirmation, check Active Positions and My Transactions for the same wallet, network, currency and maturity. Verify the executed amount and remaining FV (future value, the position’s accounting value at maturity). Borrowers remain exposed to liquidation while debt is open.

Before retrying, check the remaining position and any live opposite orders. An unfilled Unwind amount does not become an order waiting on the book. To replace a live order, follow the cancel-confirm-recheck steps in [Order Life Cycle](../core-concepts/order-life-cycle.md).

**Reducing a position partially**

To choose a smaller reduction, place an opposite order instead of using Unwind:

1. In Fixed Income, select the same currency and maturity as the position.
2. Choose Lend/Buy to reduce a borrow position, or Borrow/Sell to reduce a lend position.
3. Enter the amount you want to trade now (PV), then review the resulting FV and fee. Do not copy the position’s FV into Amount: PV and FV are different, and an oversized order can open a position in the opposite direction. See the [PV/FV example](../core-concepts/zero-coupon-bonds.md).
4. For a lend order, make sure the required currency is available and follow any deposit or approval prompts. Review and confirm the order, then check the remaining position and any live order remainder. Only executed amounts reduce the position.

{% hint style="info" %}
Unwind uses today’s market price. The result can differ from your original trade, so review the current quote and fee before closing.
{% endhint %}

**After closing:** verify the remaining position and any live opposite orders. To move available assets out, use **Withdraw** in Portfolio, review the available amount and collateral impact, and confirm. Check that the withdrawal confirmed and the funds arrived in the intended wallet account and network. See the [Portfolio guide](platform-guide/portfolio.md).

### Community liquidity support <a href="#community-liquidity-support" id="community-liquidity-support"></a>

If the order book has insufficient liquidity, ask the [official Secured Finance Discord community](https://discord.com/invite/3kytCrv3qY) for help. Include the network, asset, maturity, position side, amount you want to reduce, and any preferred price or rate.

This works like a request for a quote (RFQ): community members, including market makers, can respond with trading terms on a best-effort basis. A buyout, your requested price and execution are not guaranteed. Review the proposed transaction and verify actual fills in the app; a Discord discussion alone does not close the position.

## Troubleshooting

* **Unwind not executing or only partially filling:** check the transaction result and remaining position. You can wait for liquidity, use the partial-reduction steps above, or request community liquidity support. Review any existing live orders before another attempt.
* Values look stale: confirm the wallet and network, then refresh. For pending or uncertain transactions, follow [DApps Step 7](../../introduction/defi-starter-guide/dapps.md#id-7.-wait-for-confirmation) before another attempt. A delayed display is not proof that nothing executed.
* **Position missing after maturity** — it has rolled into the next maturity; look for the new maturity date in Active Positions.

## Related

* [Quick Start: Lend](quick-start-lend.md) · [Quick Start: Borrow](quick-start-borrow.md)
* [Tokenization](../core-concepts/tokenization.md) — move a position out as an ERC-20 token
* [Liquidation](../core-concepts/liquidation/) — risk management for borrowers
