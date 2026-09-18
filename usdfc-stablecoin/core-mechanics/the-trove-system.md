---
description: Collateralized debt positions and their lifecycle
---

# ✏️ The Trove System

A **Trove** is a personal position inside the protocol: FIL collateral on one side, USDFC debt on the other, and a collateral ratio connecting them. Every USDFC in existence was minted from some Trove, so the solvency of the system is the solvency of its Troves. Each address can hold one Trove at a time.

## Lifecycle

1. **Open** — deposit FIL and borrow USDFC (the app requires at least 200). The [borrowing fee](protocol-fees.md) and the 20 USDFC Liquidation Reserve are added to your debt.
2. **Manage** — add or withdraw collateral, borrow more, or repay, in any combination, as long as the ratio stays above the minimum and the system-wide checks pass (see [Recovery Mode](recovery-mode.md)).
3. **Close** — repay the debt in full; your collateral returns. You don't repay the Liquidation Reserve — it is netted out of what you owe. Closing is refused during [Recovery Mode](recovery-mode.md), or if it would push the system-wide ratio below 150%.
4. **Involuntary changes** — two mechanisms can alter your Trove without your consent: [liquidation](liquidation.md) if your ratio falls below 110%, and [redemption](redemption.md), which pays down the lowest-ratio Troves' debt in exchange for their collateral.

## Debt Calculations

### Total Debt at opening

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve}) + (\text{Borrowing Fee})
$$

* **Borrowed Amount** — the USDFC sent to your wallet. The protocol requires a **net debt** (borrowed amount + fee) of at least 200 USDFC, which the app enforces as a 200 USDFC minimum borrow; partial repayments must also keep net debt at or above 200.
* **Liquidation Reserve** — 20 USDFC set aside to compensate whoever triggers a liquidation of your Trove. If you close the Trove normally, you don't repay it — it is burned from the protocol's gas pool and netted out of what you owe.
* **Borrowing Fee** — one-time, (Base Rate + 0.5%) of the borrowed amount, capped at 5%; waived entirely during [Recovery Mode](recovery-mode.md). There is no ongoing interest.

**Example (Normal Mode, Base Rate 0%):** borrow 200 USDFC → fee 1.00 USDFC → Total Debt = 200 + 20 + 1.00 = **221.00 USDFC**.

### How Total Debt changes over time

The formula above is what you owe the moment the Trove opens. From then on, the balance moves — some of it through your own actions, some without them:

* **Up** — when you borrow more (plus that mint's fee), and when a liquidation elsewhere is [redistributed](stability-pool.md#if-the-pool-runs-dry-redistribution) rather than absorbed by the Stability Pool: that debt is spread across all active Troves in proportion to their collateral, adding debt (and collateral) to yours without any action on your part. The protocol applies these pending amounts to your Trove the next time it is touched.
* **Down** — when you repay, and when a [redemption](redemption.md) is processed against your Trove (debt and a matching value of collateral are removed).

The **Total Debt** figure in the app is your current outstanding balance with all of this applied, so it can differ from borrowed amount + fee + reserve.

**Closing that Trove:** you repay your current Total Debt minus the 20 USDFC reserve — in the example above, **201.00** USDFC. Note that this is already 1.00 more than you received at opening (and any debt redistributed to you since then adds to it): minting more from the same Trove can't cover it (every extra USDFC minted adds its own fee), so the difference has to come from elsewhere — a swap, another account, or Stability Pool gains swapped into USDFC.

### Collateral Ratio Formula

$$
\text{Collateral Ratio} = \frac{\text{Collateral Value (USD)}}{\text{Total Debt (USDFC)}}
$$

* **110%** is the liquidation threshold in Normal Mode.
* **150%** matters twice: it is the system-wide Recovery Mode trigger, and during Recovery Mode, Troves below the system's total ratio (which can be anywhere up to 150%) can themselves be liquidated.
* The app labels ratios below 150% as elevated risk; see [Managing Collateral Effectively](../getting-started/managing-collateral-effectively.md#choosing-a-collateral-ratio) for the full risk bands.

{% hint style="info" %}
**Why a Liquidation Reserve?** Liquidation is performed by third parties who pay gas to do it. The 20 USDFC reserve is meant to make liquidating even a small Trove worth the gas — which is also why it exists as a *reserve* rather than a fee: if your Trove is never liquidated, you never repay it.
{% endhint %}

## Where next

* [Mint & Borrow](mint-and-borrow.md) — fees and the Base Rate in detail
* [Liquidation](liquidation.md) — what happens below 110%
* [Redemption](redemption.md) — why low-ratio Troves get redeemed against first
