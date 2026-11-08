---
description: The stricter rules that activate when the whole system is under-collateralized
---

# 🚨 Recovery Mode

Recovery Mode activates automatically when the **Total Collateral Ratio (TCR)**, the combined collateral value divided by all Trove debt, falls below **150%**. It applies to every Trove and ends when TCR returns to at least 150%.

{% hint style="warning" %}
Recovery Mode blocks collateral withdrawals and Trove closure. Liquidation depends on your ratio, the system ratio and Stability Pool coverage. Use the [borrower rules](recovery-mode.md#what-changes) and [complete liquidation table](recovery-mode.md#liquidation-behavior-in-recovery-mode) below.
{% endhint %}

The app shows a prominent Recovery Mode notice on the Dashboard whenever it is active.

## Borrower checklist

* Check **Recovery Mode** and **Total Collateral Ratio** in the app's Protocol Overview, then your own ratio on the Trove page.
* During Recovery Mode, you cannot withdraw collateral or close a Trove. Opening or borrowing more has stricter ratio rules.
* Adding collateral or repaying may improve your ratio, but requires a usable oracle price and must satisfy the checks below. Read the [Trove page's oracle warning](price-oracle.md#checking-oracle-status-in-the-app) before acting.

**Terms used below:** **ICR** is your individual Trove's collateral ratio; **TCR** is the total ratio across all Troves; **SP** means the Stability Pool, whose USDFC can be used to settle liquidated debt.

## What changes

| Action or parameter           | Normal Mode                                   | Recovery Mode                                                                                      |
| ----------------------------- | --------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Liquidation eligibility       | ICR < 110%                                    | See the [complete liquidation table](recovery-mode.md#liquidation-behavior-in-recovery-mode) below |
| Borrowing fee                 | Base Rate + 0.5% (capped at 5%)               | **0%**                                                                                             |
| Minimum ratio for a new Trove | ICR ≥ 110%; resulting TCR ≥ 150%              | ICR ≥ 150%                                                                                         |
| Collateral withdrawal         | Subject to the Normal Mode ratio checks below | **Not allowed**                                                                                    |
| Debt increase                 | Subject to the Normal Mode ratio checks below | Resulting ICR ≥ 150% and no lower than the Trove's previous ICR                                    |
| Add collateral or repay debt  | Subject to the Normal Mode ratio checks below | Allowed, subject to the other checks below                                                         |
| Close a Trove                 | Resulting TCR ≥ 150%                          | **Not allowed**                                                                                    |

In Normal Mode, every opening or adjustment must leave the Trove's ICR at or above 110% and the system TCR at or above 150%. This also applies to adding collateral or repaying debt. In Recovery Mode, combining an adjustment with a debt increase invokes the debt-increase rule above; combining it with a collateral withdrawal is not permitted.

These are the mode-specific rules, not every transaction requirement. Partial repayment must leave at least 200 USDFC of net debt (excluding the 20 USDFC Liquidation Reserve). An address can perform one Trove operation (open, adjust or close) per block; a second operation in the same block reverts. Wallet balances, gas and other contract checks still apply. Borrowing fees are waived in Recovery Mode, but gas costs remain. [Oracle availability requirements](price-oracle.md#which-actions-remain-available) apply independently in both modes.

## Liquidation behavior in Recovery Mode

Liquidation becomes condition-dependent, balancing the Stability Pool's capacity against each Trove's ratio:

| Condition                                                                  | Liquidation Behavior                                                                                                                                                                                                                                                                                                                          |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ICR ≤ 100%                                                                 | **Redistribute** all debt and collateral (minus gas compensation) to active Troves.                                                                                                                                                                                                                                                           |
| <p>100% &#x3C; ICR &#x3C; 110%<br>&#x26;<br>SP USDFC ≥ Trove debt</p>      | USDFC in the Stability Pool equal to the Trove's debt is offset with the Trove's debt. The Trove's FIL collateral (minus gas compensation) is shared between depositors.                                                                                                                                                                      |
| <p>100% &#x3C; ICR &#x3C; 110%<br>&#x26;<br>SP USDFC &#x3C; Trove debt</p> | The total Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of the Trove's collateral (after gas compensation, equal to the ratio of its offset debt to its entire debt) is shared between depositors. The remaining debt and collateral (minus gas compensation) is **redistributed** to active Troves. |
| <p>110% ≤ ICR &#x3C; TCR<br>&#x26;<br>SP USDFC >= Trove debt</p>           | **Your Trove closes.** The Stability Pool cancels its entire debt. Collateral worth 110% of that debt is used for liquidation, including gas compensation. Any surplus is claimable by you. Nothing is redistributed to other active Troves. See the collateral-cap details below.                                                            |
| <p>110% ≤ ICR &#x3C; TCR<br>&#x26;<br>SP USDFC &#x3C; Trove debt</p>       | Not liquidated                                                                                                                                                                                                                                                                                                                                |
| ICR ≥ 110% & ICR ≥ TCR                                                     | Not liquidated                                                                                                                                                                                                                                                                                                                                |

Use the Trove's entire debt and collateral, including pending redistribution, at the protocol's usable oracle price. The last remaining Trove is not liquidated. During a sequence of liquidations, the current TCR and available Stability Pool balance can change between Troves.

The **110% collateral cap applies only to the fourth row**. In that fully covered branch, collateral worth up to 110% of the total debt is used for liquidation, including the liquidator's share; any surplus goes to the `CollSurplusPool` and remains **claimable by the borrower**. This cap does not apply to the below-110% redistribution and offset branches. In the capped branch, the remaining collateral is zero if the ICR was exactly 110%.

## A typical episode

1. FIL drops sharply; the TCR crosses below 150% and Recovery Mode activates. The Dashboard shows the notice.
2. Liquidations follow the table above. Owners can add collateral or repay to improve their ratios, subject to the borrower and oracle checks above.
3. Collateral top-ups raise the TCR at an unchanged price. Liquidations that offset debt can raise or lower TCR, depending on the collateral and debt removed. Redistribution alone does not improve TCR, and collateral gas compensation can reduce it. Recovery Mode ends once TCR reaches 150%; Normal Mode liquidation rules and borrowing fees then apply.

## What to do as a borrower

* **Before:** maintain a collateral buffer that reflects FIL volatility and your ability to monitor the position. A larger buffer gives more room for price falls. Recovery Mode withdrawal and closure restrictions apply to every Trove.
* **During:** compare your ICR, TCR and the Stability Pool balance with the [liquidation table](recovery-mode.md#liquidation-behavior-in-recovery-mode). Before adjusting your Trove, check the [borrower rules](recovery-mode.md#what-changes) and oracle availability.

## Where next

* [Liquidation](liquidation.md) — the normal-mode liquidation these rules extend
* [Stability Pool](stability-pool.md) — the pool whose capacity shapes the table above
* [Monitoring Your Position](../getting-started/monitoring-your-position.md) — staying ahead of the TCR
