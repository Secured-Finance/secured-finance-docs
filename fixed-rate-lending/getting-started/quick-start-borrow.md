---
description: Place a borrowing order, verify the fill, and manage your debt
---

# 🏦 Quick Start: Borrow

Borrowing on Secured Finance means selling a Zero-Coupon (ZC) bond: an executed trade credits funds to your protocol account and creates a debt position. The execution price fixes your borrowing rate for the current term.

**You'll need:** a Web3 wallet, collateral assets, and a small amount of the network's native token for gas.

{% hint style="warning" %}
**Before you deposit or place an order**

* At maturity, debt is not automatically repaid. Auto-Roll moves it into the nearest 3-month market at a new rate, with a roll fee. You cannot turn Auto-Roll off.
* Unwind attempts to close debt with an opposite (lend) trade. Liquidity may limit how much you can close, and the required amount changes with the market price. You can withdraw collateral only within the available amount after your remaining obligations.
* Your collateral remains exposed to liquidation while debt is open, including after Auto-Roll. Review [Fees](../core-concepts/fees.md) and [Liquidation](../core-concepts/liquidation/) before committing.
{% endhint %}

New to wallets? Complete [Wallet Setup](../../introduction/defi-starter-guide/wallet-setup.md) and read [DApps: permissions and transactions](../../introduction/defi-starter-guide/dapps.md) first. Check that the wallet and app show the same account and network, and keep native tokens in your wallet for later gas fees.

## Step 1 — Connect and deposit collateral

1. Open [app.secured.finance](https://app.secured.finance/) and click **Connect Wallet**.
2. Go to the **Portfolio** tab and click **Deposit**.
3. Choose an accepted collateral asset (see [Collateral](../core-concepts/collateral.md) for the list per network). If prompted, review and confirm the token approval, then complete the deposit transaction. An approval alone does not deposit collateral.
4. Wait for confirmation, then verify the deposited balance in Portfolio for the same account and network before placing an order.

Borrowing requires **over-collateralization** — your collateral must be worth significantly more than the amount you borrow. Current thresholds are listed in [Protocol Parameters](../protocol-parameters.md).

## Step 2 — Choose a market

1. Open the **Fixed Income** tab (the trading interface).
2. Select the currency you want to borrow and a maturity date (quarterly — the last Friday of Mar/Jun/Sep/Dec).
3. Check the current borrow rate on the order book.

## Step 3 — Place your borrow order

1. Select **Borrow/Sell**.
2. Pick an order type:
   * **Market order** tries to trade now against available orders. It may fill fully, partly or not at all; any unfilled amount does not wait on the book. Executed volume pays a taker fee ([Fees](../core-concepts/fees.md)).
   * **Limit order** sets the lowest bond price you will accept, corresponding to your maximum quoted borrowing APR. It can fill now, wait on the book, or do both. A fill against existing orders pays the taker fee; a later fill of a resting order pays no trading fee.
3. Enter Amount in the selected currency. This is PV (present value), the amount traded now, before fees. FV (future value) is the position’s accounting value at maturity, not an automatic wallet payment. Review the APR, fee and FV, plus Collateral Usage. See the [PV/FV example](../core-concepts/zero-coupon-bonds.md).
4. Submit the order and confirm in your wallet. Only the **executed amount** credits borrowed funds and creates debt. Check Step 4 before withdrawing or placing another order.

## Step 4 — Verify execution and position health

After confirmation, check Order History → Filled Amount, Open Orders and Active Positions for the same wallet, network, currency and maturity. A wallet signature is not proof of a fill. See [Order Life Cycle](../core-concepts/order-life-cycle.md) for execution outcomes and how to cancel and replace a live remainder.

Pending or uncertain result? Follow [DApps Step 7](../../introduction/defi-starter-guide/dapps.md#id-7.-wait-for-confirmation) before trying again.

Monitor Collateral Utilization and Liquidation Risk in Portfolio while debt remains open. See [collateral coverage](managing-positions.md#for-borrowers-watch-your-collateral-coverage) for what these indicators mean and how to reduce risk.

**Move borrowed funds to your wallet:** after verifying the fill, use **Withdraw** in Portfolio and select the borrowed asset. Enter no more than the available withdrawal amount, review the effect on collateral risk, and confirm. Verify the confirmed transfer in the same wallet account and network. The debt remains open after withdrawal. See the [Portfolio guide](platform-guide/portfolio.md).

## Step 5 — Repay or continue borrowing <a href="#step-5-repaying-important" id="step-5-repaying-important"></a>

In Portfolio → Active Positions, select Unwind and review the Unwind Position dialog. Closing buys back the bond at the current price.

Unwind spends the borrowed currency already deposited in the protocol. Deposit enough to cover the quote and fee before submitting; tokens in your external wallet are not used automatically. Keep native tokens in your wallet for gas. Review the quote again after funding, then submit and confirm in your wallet.

After confirmation, verify the executed amount and remaining debt before withdrawing available collateral. Any unclosed debt continues through Auto-Roll and remains exposed to liquidation. For partial repayment, see [Managing Your Positions](managing-positions.md#reducing-or-closing-a-position).

If liquidity is thin, see [community liquidity support](managing-positions.md#community-liquidity-support) for how to request a quote through the official Discord community; responses are best-effort and execution is not guaranteed.

## Troubleshooting

* **Transaction fails**: read the error and check gas, collateral, and the order's permitted price range. Confirm whether the transaction reverted before retrying.
* **"Insufficient collateral" error** — deposit more collateral, reduce the borrow amount, or check the asset's haircut in [Protocol Parameters](../protocol-parameters.md).
* **Limit order not filling:** compare your price with the current order book. To change price or amount, see Order Life Cycle in Step 4.
* **Unwind blocked or partially filled:** check the remaining debt. You can wait for liquidity, request community liquidity support, or consider an opposite (lend) limit order. Follow the steps in [Managing Your Positions](managing-positions.md).

## Next steps

* [Collateral](../core-concepts/collateral.md) — accepted assets and haircuts per network
* [Liquidation](../core-concepts/liquidation/) — thresholds, fees, and how to stay safe
* [Managing Your Positions](managing-positions.md) — day-to-day position management
