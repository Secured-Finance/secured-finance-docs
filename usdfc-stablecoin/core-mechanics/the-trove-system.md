---
description: Collateralized debt positions and their lifecycle
---

# ✏️ The Trove System

A **Trove** is a personal position inside the protocol: FIL collateral on one side, USDFC debt on the other, and a collateral ratio connecting them. Every USDFC in existence was minted from some Trove, so the solvency of the system is the solvency of its Troves. Each address can hold one Trove at a time.

## Lifecycle

1. **Open** — deposit FIL and borrow at least 200 USDFC. The [borrowing fee](protocol-fees.md) and the 20 USDFC Liquidation Reserve are added to your debt.
2. **Manage** — add or withdraw collateral, borrow more, or repay, in any combination, as long as the ratio stays above the minimum.
3. **Close** — repay the debt in full; your collateral returns and the Liquidation Reserve is refunded.
4. **Involuntary changes** — two mechanisms can alter your Trove without your consent: [liquidation](liquidation.md) if your ratio falls below 110%, and [redemption](redemption.md), which pays down the lowest-ratio Troves' debt in exchange for their collateral.

## Debt Calculations

### Total Debt Formula

$$
\text{Total Debt} = (\text{Borrowed Amount}) + (\text{Liquidation Reserve}) + (\text{Borrowing Fee})
$$

* **Borrowed Amount** — the USDFC sent to your wallet (minimum 200 USDFC).
* **Liquidation Reserve** — 20 USDFC set aside to compensate whoever triggers a liquidation of your Trove; refunded when you close it normally.
* **Borrowing Fee** — one-time, (Base Rate + 0.5%) of the borrowed amount; waived entirely during [Recovery Mode](recovery-mode.md). There is no ongoing interest.

**Example (Normal Mode, Base Rate 0%):** borrow 200 USDFC → fee 1.00 USDFC → Total Debt = 200 + 20 + 1.00 = **221.00 USDFC**.

**Closing that Trove:** you repay the Total Debt, but the 20 USDFC reserve is netted out in the same transaction — so the USDFC you must actually hold is **201.00**. Note that this is 1.00 more than you received: the fee has to come from somewhere (mint slightly more up front, or acquire the difference).

### Collateral Ratio Formula

$$
\text{Collateral Ratio} = \frac{\text{Collateral Value (USD)}}{\text{Total Debt (USDFC)}}
$$

* **110%** is the liquidation threshold in Normal Mode.
* **150%** matters twice: it is the system-wide Recovery Mode trigger, and during Recovery Mode, Troves below 150% can themselves be liquidated.
* The app labels ratios below 150% as elevated risk; see [Managing Collateral Effectively](../getting-started/managing-collateral-effectively.md#choosing-a-collateral-ratio) for the full risk bands.

{% hint style="info" %}
**Why a Liquidation Reserve?** Liquidation is performed by third parties who pay gas to do it. The 20 USDFC reserve guarantees that liquidating even a small Trove is worth the gas — which is also why it exists as a *reserve* rather than a fee: if your Trove is never liquidated, you get it back.
{% endhint %}

## Where next

* [Mint & Borrow](mint-and-borrow.md) — fees and the Base Rate in detail
* [Liquidation](liquidation.md) — what happens below 110%
* [Redemption](redemption.md) — why low-ratio Troves get redeemed against first
