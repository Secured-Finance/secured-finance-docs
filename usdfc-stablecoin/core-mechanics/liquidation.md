---
description: How under-collateralized Troves are resolved
---

# 🚰 Liquidation

## What are Liquidations?

Liquidation is how the protocol removes under-collateralized debt before it can threaten the system. When a Trove's collateral ratio falls below **110%**, anyone can trigger its liquidation: the Trove's debt is repaid by the [Stability Pool](stability-pool.md) and its FIL collateral is distributed to the pool's depositors. The Trove is closed in the process.

The threshold extends during [Recovery Mode](recovery-mode.md): while the system-wide ratio (TCR) is below 150%, any Trove **below the current TCR** can also be liquidated — though for a Trove above 110%, only collateral worth 110% of its debt is taken, and the remainder stays claimable by the owner.

## The process

1. **Trigger** — a Trove's ratio drops below the threshold and a **liquidator** (any address) calls the liquidation function.
2. **Debt repayment** — USDFC equal to the Trove's debt is burned from the Stability Pool.
3. **Collateral distribution** — the Trove's FIL, minus the liquidator's 0.5% share, goes to Stability Pool depositors pro rata. If the pool can't cover the debt, the remainder is [redistributed](stability-pool.md#if-the-pool-runs-dry-redistribution) across all active Troves in proportion to their collateral.

## Key parameters

| Parameter | Description | Value |
| --- | --- | --- |
| Liquidation threshold | Per-Trove ratio below which liquidation is possible | 110% (the current TCR, up to 150%, in Recovery Mode) |
| Liquidator reward | Share of the liquidated collateral paid to the liquidator | 0.5% |
| Gas compensation | Paid to the liquidator from the Trove's Liquidation Reserve | 20 USDFC |

## What each party experiences

**The liquidated borrower** loses their collateral but keeps every USDFC they borrowed, and their debt is gone — the Trove is simply closed. Since liquidation happens just below 110%, the collateral lost is worth roughly 10% more than the debt cleared: that gap is the borrower's loss and the system's safety margin.

**Stability Pool depositors** acquire the FIL at that same discount — see [Stability Pool](stability-pool.md) for the economics.

**The liquidator** is whoever pays the gas to trigger it, compensated with the 20 USDFC reserve plus 0.5% of the collateral.

## Becoming a liquidator

Liquidation is permissionless, and the app makes it accessible: the **Risky Troves** page (under the **More** tab) lists Troves ordered by collateral ratio with a **Liquidate** action next to any that are eligible, plus a control to liquidate several at once. The 20 USDFC + 0.5% compensation is designed to cover gas with a margin, so watching the risky list during sharp FIL drops can be profitable — but you're competing with bots, and a transaction that loses the race still costs gas.

{% hint style="info" %}
Liquidation depends on the oracle price, not any exchange's price — a Trove that looks under-water on a DEX chart isn't liquidatable until the [protocol's price feed](price-oracle.md) says so.
{% endhint %}

## Where next

* [Stability Pool](stability-pool.md) — where the debt and collateral go
* [Price Oracle](price-oracle.md) — the price that decides eligibility
* [Managing Collateral Effectively](../getting-started/managing-collateral-effectively.md) — staying out of liquidation range
