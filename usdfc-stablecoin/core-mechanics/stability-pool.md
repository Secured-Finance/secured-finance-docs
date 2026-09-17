---
description: The USDFC reserve that absorbs liquidations
---

# 🏊 Stability Pool

The Stability Pool is the protocol's liquidation engine: a shared reserve of USDFC used to repay the debt of Troves that fall below the minimum collateral ratio, up to the USDFC it holds. It converts a solvency threat into an orderly exchange — bad debt is burned, and the liquidated collateral flows to the depositors who funded the pool.

## How a liquidation flows through the pool

1. A Trove drops below 110% and someone [triggers its liquidation](liquidation.md).
2. USDFC equal to the Trove's debt is **burned from the pool**, extinguishing the debt.
3. The Trove's FIL collateral (minus the [liquidator's 0.5% cut](liquidation.md)) is credited to depositors.

Both effects are shared **pro rata**: if you hold 2% of the pool, 2% of the burned USDFC comes from your deposit and 2% of the seized FIL becomes yours:

$$
\text{Your Gain} = \text{FIL allocated to the pool} \times \frac{\text{Your Deposit}}{\text{Total Stability Pool}}
$$

where "FIL allocated to the pool" is the liquidated collateral after the liquidator's 0.5% share — and, when the pool only partly covers a debt or a Recovery Mode liquidation is capped at 110%, only the corresponding fraction of it. Your share is measured immediately before the liquidation.

## Why depositing is attractive

A Trove is liquidated below 110% but above 100% in the typical case — so the pool takes on, say, $105–109 of FIL for every $100 of USDFC it burns (before the liquidator's 0.5% share; roughly $104.5–108.5 after it). Depositors are effectively buying FIL below market price, paid for by liquidated borrowers. The trade-off: your stable asset converts into a volatile one at unpredictable times, and in a severe crash a Trove can be liquidated below roughly 100.5% — the point where the collateral, net of the liquidator's share, no longer covers the debt — making that particular liquidation a net loss for the pool.

There is no lock-up period, but **withdrawals are suspended while liquidatable Troves (below 110%) are pending**, so the pool cannot be drained just before it's needed — and, like other operations that need a price, they also revert while the [price feed](price-oracle.md) cannot return a usable price. See the [hands-on guide](../getting-started/using-the-stability-pool.md) for deposits, claims, and withdrawals in the app.

## If the pool runs dry — redistribution

The Stability Pool can only absorb debt it actually holds. If a liquidation exceeds the pool's balance, the protocol falls back to **redistribution**: the remaining debt and collateral of the liquidated Trove are spread across all active Troves, proportionally to their collateral. This applies to Troves below 110%; in [Recovery Mode](recovery-mode.md#liquidation-behavior-in-recovery-mode), a Trove between 110% and the TCR is never redistributed — it is simply not liquidated until the pool can cover its entire debt.

For a receiving Trove, this means both its debt and its collateral increase. Whether that is a net gain depends on the liquidated Trove's ratio: measured before the liquidator's 0.5% cut, redistribution breaks even at roughly 100.5% — above that, the collateral received is worth more than the debt taken on; below it, receivers absorb a shortfall. Either way, a Trove that was healthier than the liquidated one sees its own collateral *ratio* drop, so a deep cascade pushes the whole system toward [Recovery Mode](recovery-mode.md). A well-funded Stability Pool limits how often that happens, but cannot rule it out.

## Where next

* [Liquidation](liquidation.md) — the full liquidation mechanics, including the liquidator's role
* [Using the Stability Pool](../getting-started/using-the-stability-pool.md) — depositing and withdrawing in the app
* [Recovery Mode](recovery-mode.md) — what happens when the whole system is stressed
