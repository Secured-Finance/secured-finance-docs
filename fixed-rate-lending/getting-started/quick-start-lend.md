---
description: Place a lending order, verify the fill, and plan your exit
---

# 💵 Quick Start: Lend

Lending on Secured Finance means buying a Zero-Coupon (ZC) bond at a discount: you pay less than its face value today. The execution price fixes the rate for the current term.

**You'll need:** a Web3 wallet, assets to lend, and a small amount of the network's native token for gas.

{% hint style="warning" %}
**Before you deposit or place an order**

* The fixed rate applies to the current term. At maturity, **Auto-Roll** moves the position into the nearest 3-month market at a new rate, with a roll fee. You cannot turn Auto-Roll off.
* To exit, use Unwind to close the position with an opposite trade, then withdraw the available balance. Available liquidity determines how much you can close. Closing at the current price may realize a loss.
* Maturity does not automatically pay funds to your wallet. Review [Fees](../core-concepts/fees.md) and [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md) before committing.
{% endhint %}

New to wallets? Complete [Wallet Setup](../../introduction/defi-starter-guide/wallet-setup.md) and read [DApps: permissions and transactions](../../introduction/defi-starter-guide/dapps.md) first. Check that the wallet and app show the same account and network, and keep native tokens in your wallet for later gas fees.

## Step 1 — Connect and deposit

1. Open [app.secured.finance](https://app.secured.finance/) and click **Connect Wallet**.
2. Go to the **Portfolio** tab and click **Deposit**.
3. Choose the asset and amount to deposit. If prompted, review and confirm the token approval, then complete the deposit transaction. An approval alone does not deposit funds.
4. Wait for confirmation, then verify the deposited balance in Portfolio for the same account and network before placing an order.

## Step 2 — Choose a market

1. Open the **Fixed Income** tab (the trading interface).
2. Select the currency and the maturity date. Markets mature quarterly — the last Friday of March, June, September, and December.
3. Check the current yield for that maturity on the order book, or compare maturities on the [Stats](https://app.secured.finance/stats/) yield curve.

## Step 3 — Place your lend order

1. Select **Lend/Buy**.
2. Pick an order type:
   * **Market order** tries to trade now against available orders. It may fill fully, partly or not at all; any unfilled amount does not wait on the book. Executed volume pays a taker fee ([Fees](../core-concepts/fees.md)).
   * **Limit order** sets the highest bond price you will pay, corresponding to your minimum quoted lending APR. It can fill now, wait on the book, or do both. A fill against existing orders pays the taker fee; a later fill of a resting order pays no trading fee.
3. Enter Amount in the selected currency. This is PV (present value), the amount traded now, before fees. FV (future value) is the position’s accounting value at maturity, not an automatic wallet payment. Review the APR, fee and FV. See the [PV/FV example](../core-concepts/zero-coupon-bonds.md).
4. Submit the order and confirm in your wallet. Then check the transaction result and actual fill in Step 4.

## Step 4 — Verify what executed

After confirmation, check Order History → Filled Amount, Open Orders and Active Positions for the same wallet, network, currency and maturity. A wallet signature is not proof of a fill. See [Order Life Cycle](../core-concepts/order-life-cycle.md) for execution outcomes and how to cancel and replace a live remainder.

Pending or uncertain result? Follow [DApps Step 7](../../introduction/defi-starter-guide/dapps.md#id-7.-wait-for-confirmation) before trying again.

## Step 5 — Exit or continue lending <a href="#step-5-at-maturity-important" id="step-5-at-maturity-important"></a>

To exit before or after maturity, select Unwind in Portfolio → Active Positions and review the Unwind Position dialog. After confirmation, check how much closed and what remains. Any unclosed amount continues as a position; Auto-Roll moves it to the next term at maturity.

If liquidity is thin, see [community liquidity support](managing-positions.md#community-liquidity-support) for how to request a quote through the official Discord community; responses are best-effort and execution is not guaranteed.

**Move available funds to your wallet:** after checking the unwind result, use **Withdraw** in Portfolio, select the asset and an amount within the available balance, and confirm. Wait for the withdrawal to confirm, then verify the balance in the same wallet account and network. Closing a position and withdrawing funds are separate actions. See the [Portfolio guide](platform-guide/portfolio.md).

## Troubleshooting

* **Limit order not filling:** compare your price with the current order book. To change price or amount, see Order Life Cycle in Step 4.
* **Transaction fails**: read the error and check gas, deposited balance, and the order's permitted price range. Confirm whether the transaction reverted before retrying.
* **Unwind blocked or partially filled:** check the remaining position. You can wait for liquidity, request community liquidity support, or consider an opposite (borrow) limit order. Follow the steps in [Managing Your Positions](managing-positions.md).

## Next steps

* [Managing Your Positions](managing-positions.md) — add, reduce, unwind
* [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md) — how quarterly markets work
* [Zero-Coupon Bonds](../core-concepts/zero-coupon-bonds.md) — price ↔ APR mechanics
