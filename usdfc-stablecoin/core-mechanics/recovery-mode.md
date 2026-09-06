---
description: The stricter rules that activate when the whole system is under-collateralized
---

# 🚨 Recovery Mode

Recovery Mode is the protocol's defense against systemic under-collateralization. It activates automatically whenever the **Total Collateral Ratio (TCR)** — the combined collateral of all Troves against all debt — falls below **150%**, and deactivates the moment the TCR recovers above it. It is not an opt-in feature or an edge case for advanced users: when it triggers, its rules apply to every Trove at once.

{% hint style="warning" %}
During Recovery Mode, Troves below the **current TCR** can be liquidated — not just those below 110%. If the TCR is 145%, a Trove at 140% is at risk. This is why keeping a ratio comfortably above 150% matters even in calm times.
{% endhint %}

The app shows a prominent Recovery Mode notice on the Dashboard whenever it is active.

## What changes

| | Normal Mode | Recovery Mode |
| --- | --- | --- |
| Liquidation threshold | 110% | Current TCR (< 150%) |
| Borrowing fee | Base Rate + 0.5% | **0%** |
| Minimum ratio for a new Trove | 110% | 150% |
| Collateral withdrawal | Allowed (above 110%) | **Not allowed** |
| Debt increase | Allowed (above 110%) | Only if the Trove ends at ≥ 150% and the adjustment improves its ratio |
| Repaying debt | Allowed | Allowed (down to the 200 USDFC minimum) |
| Closing a Trove | Allowed (unless it would push the TCR below 150%) | **Not allowed** |

Every restriction points the same direction: adjustments that push the system back above 150% are free and easy; adjustments that would drain collateral — including closing a Trove, which returns its collateral — are blocked. The fee waiver removes any cost friction from repairing your position, and the 150% floor on new borrowing ensures new activity strengthens the TCR rather than diluting it.

The 150% line is guarded in Normal Mode too: any operation that would push the TCR below 150% — opening a Trove, increasing debt, withdrawing collateral, or closing a Trove — is rejected before it can trigger Recovery Mode.

## Liquidation behavior in Recovery Mode

Liquidation becomes condition-dependent, balancing the Stability Pool's capacity against each Trove's ratio:

<table><thead><tr><th width="277">Condition</th><th>Liquidation Behavior</th></tr></thead><tbody><tr><td>ICR ≤ 100%</td><td><strong>Redistribute</strong> all debt and collateral (minus gas compensation) to active Troves.</td></tr><tr><td>100% &#x3C; ICR &#x3C; 110%<br>&#x26;<br>SP USDFC > Trove debt</td><td>USDFC in the Stability Pool equal to the Trove's debt is offset with the Trove's debt. The Trove's FIL collateral (minus gas compensation) is shared between depositors.</td></tr><tr><td>100% &#x3C; ICR &#x3C; 110%<br>&#x26;<br>SP USDFC &#x3C; Trove debt</td><td>The total Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of the Trove's collateral (equal to the ratio of its offset debt to its entire debt) is shared between depositors. The remaining debt and collateral (minus gas compensation) is <strong>redistributed</strong> to active Troves.</td></tr><tr><td>110% ≤ ICR &#x3C; TCR<br>&#x26;<br>SP USDFC >= Trove debt</td><td>The Stability Pool USDFC is offset with an equal amount of debt from the Trove. A fraction of FIL collateral with dollar value equal to <code>1.1 * debt</code> is shared between depositors. Nothing is redistributed to other active Troves. Since its ICR was <code>> 1.1</code>, the Trove has a collateral remainder, which is sent to the <code>CollSurplusPool</code> and is claimable by the borrower. The Trove is closed.</td></tr><tr><td>110% ≤ ICR &#x3C; TCR<br>&#x26;<br>SP USDFC &#x3C; Trove debt</td><td>Do nothing.</td></tr><tr><td>ICR ≥ TCR</td><td>Do nothing.</td></tr></tbody></table>

Where ICR = Individual Collateral Ratio, TCR = Total Collateral Ratio, SP = Stability Pool.

Note the important protection in the fourth row: a Trove liquidated **above 110%** only loses collateral worth 110% of its debt — the surplus goes to the `CollSurplusPool` and remains **claimable by the borrower**. Recovery Mode liquidation is capped, not confiscatory.

## A typical episode

1. FIL drops sharply; the TCR crosses below 150% and Recovery Mode activates. The Dashboard shows the notice.
2. Troves below the TCR become liquidatable; their owners add collateral or repay (fee-free) to climb above it, while liquidators work through those that don't.
3. Every liquidation and top-up raises the TCR. Once it crosses 150%, Recovery Mode ends and the 110% threshold and normal fees return.

## What to do as a borrower

* **Before:** the real defense happens in Normal Mode — keeping your ratio well above 150% (the app labels 200%+ as very low risk) means Recovery Mode is something you observe, not suffer.
* **During:** add collateral or repay debt immediately if you're below the TCR; both improve your ratio and the system's. Remember collateral withdrawal is blocked, so you cannot rebalance out — only in.
* **Not available:** closing your Trove. Closing returns collateral to you, so it is blocked until Recovery Mode ends — you can repay debt down to the 200 USDFC minimum in the meantime.

## Where next

* [Liquidation](liquidation.md) — the normal-mode liquidation these rules extend
* [Stability Pool](stability-pool.md) — the pool whose capacity shapes the table above
* [Monitoring Your Position](../getting-started/monitoring-your-position.md) — staying ahead of the TCR
