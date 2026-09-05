---
description: The face-value exchange that anchors USDFC's peg
---

# 💸 Redemption

Redemption is the protocol's promise that 1 USDFC can always be exchanged for $1 worth of FIL. Any holder can invoke it at any time, and the FIL comes from the collateral of the lowest-ratio Troves. That standing promise is what puts a floor under the price: whenever USDFC trades below $1, redeeming it is free money, and the resulting arbitrage pulls the price back up.

{% hint style="success" %}
**What redemption gives holders**

* **Arbitrage** — buy USDFC below $1, redeem it for $1 of FIL, keep the difference
* **Guaranteed exit** — convert USDFC to FIL at oracle price even when DEX liquidity is thin
{% endhint %}

## How it works

1. A holder submits USDFC for redemption.
2. The protocol pairs it against the Trove with the **lowest collateral ratio** (of those at 110% or above — Troves below that are left for [liquidation](liquidation.md)): the Trove's debt is reduced by the redeemed amount and an equal USD value of its FIL is released.
3. If one Trove isn't enough, the redemption continues into the next-lowest, until fulfilled.
4. The redeemer receives the FIL minus the [redemption fee](#redemption-fee); the fee itself is taken in FIL.

For the affected Trove owner this is a **forced swap, not a loss**: debt falls by exactly the USD value of the collateral taken, so net position value is unchanged — but FIL exposure is gone from that slice, and if FIL later rises, that upside was surrendered. Keeping a higher ratio than the crowd keeps you out of the queue; the app's **Debt in front** figure shows how much debt stands between you and it ([details](../getting-started/monitoring-your-position.md#debt-in-front)).

{% hint style="warning" %}
**Redemption is not repayment.** Redeeming reduces *someone else's* Trove. To reduce your own debt, repay via Update Trove — which has no fee at all.
{% endhint %}

A redemption cannot leave a Trove's borrowed amount below the 200 USDFC minimum — it either stays above it (the redemption amount is adjusted down) or pays the Trove off entirely.

## Redemption Fee

$$
\text{Redemption Fee} = (\text{Base Rate} + 0.5\%) \times \text{Redeemed USDFC}
$$

* **0.5%** is the floor. The [**Base Rate**](mint-and-borrow.md#base-rate-explanation) rises with each redemption — by 0.5 × (redeemed amount / total supply) — and decays with a 12-hour half-life. Unlike the minting fee, the redemption fee has **no upper cap**, so a wave of redemptions makes further redemptions progressively more expensive.
* The fee is deducted from the FIL you receive.
* Redemptions are unavailable while the system's total collateral ratio is below 110%.

This dynamic fee is deliberate: it lets ordinary peg-restoring arbitrage through cheaply, but makes it prohibitively expensive to strip large amounts of collateral out of the system in a short window.

## The peg, from both sides

* **Below $1:** redemption arbitrage burns USDFC supply and pushes the price up (as long as the discount exceeds the current fee).
* **Above $1:** minting becomes the arbitrage — borrow at $1 of value per USDFC, sell at the premium — expanding supply and pushing the price down. The 110% collateral requirement is why the ceiling is softer than the floor.

**Worked example:** USDFC trades at $0.98 and the Base Rate is 1.0%. Buy 1,000 USDFC for $980, redeem: fee = 1.5% = 15 USDFC-worth, so you receive $985 of FIL. Profit ≈ $5 — and shrinking, as your own redemption nudges the Base Rate up for the next arbitrageur.

## Where next

* [Redeeming USDFC](../getting-started/redeeming-usdfc.md) — the hands-on guide
* [Mint & Borrow](mint-and-borrow.md#base-rate-explanation) — the Base Rate mechanics shared by both fees
* [Monitoring Your Position](../getting-started/monitoring-your-position.md) — how Trove owners track redemption risk
