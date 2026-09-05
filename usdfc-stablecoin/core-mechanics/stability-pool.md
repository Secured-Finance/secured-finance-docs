---
description: The USDFC reserve that absorbs liquidations
---

# 🏊 Stability Pool

The Stability Pool is the protocol's liquidation engine: a shared reserve of USDFC that stands ready to repay the debt of any Trove that falls below the minimum collateral ratio. It converts a solvency threat into an orderly exchange — bad debt is burned, and the liquidated collateral flows to the depositors who funded the pool.

## How a liquidation flows through the pool

1. A Trove drops below 110% and someone [triggers its liquidation](liquidation.md).
2. USDFC equal to the Trove's debt is **burned from the pool**, extinguishing the debt.
3. The Trove's FIL collateral (minus the [liquidator's 0.5% cut](liquidation.md)) is credited to depositors.

Both effects are shared **pro rata**: if you hold 2% of the pool, 2% of the burned USDFC comes from your deposit and 2% of the seized FIL becomes yours:

$$
\text{Your Gain} = \text{Liquidated Collateral} \times \frac{\text{Your Deposit}}{\text{Total Stability Pool}}
$$

## Why depositing is attractive

A Trove is liquidated below 110% but above 100% in the typical case — so the pool takes on, say, $105–109 of FIL for every $100 of USDFC it burns. Depositors are effectively buying FIL below market price, paid for by liquidated borrowers. The trade-off: your stable asset converts into a volatile one at unpredictable times, and in a severe crash a Trove can be liquidated below 100%, making that particular liquidation a net loss for the pool.

Deposits are never locked, with one exception: **withdrawals are suspended while liquidatable Troves (below 110%) are pending**, so the pool cannot be drained just before it's needed. See the [hands-on guide](../getting-started/using-the-stability-pool.md) for deposits, claims, and withdrawals in the app.

## If the pool runs dry — redistribution

The Stability Pool can only absorb debt it actually holds. If a liquidation exceeds the pool's balance, the protocol falls back to **redistribution**: the remaining debt and collateral of the liquidated Trove are spread across all active Troves, proportionally to their collateral.

For a receiving Trove, this means both its debt and its collateral increase. Because the liquidated Trove was below 110% while receivers are above it, the net USD value received exceeds the debt taken on — but every receiving Trove's collateral *ratio* drops, so a deep cascade pushes the whole system toward [Recovery Mode](recovery-mode.md). A well-funded Stability Pool is what keeps that scenario theoretical.

## Where next

* [Liquidation](liquidation.md) — the full liquidation mechanics, including the liquidator's role
* [Using the Stability Pool](../getting-started/using-the-stability-pool.md) — depositing and withdrawing in the app
* [Recovery Mode](recovery-mode.md) — what happens when the whole system is stressed
