---
description: The face-value exchange that anchors USDFC's peg
---

# 💸 Redemption

Redemption is the protocol's mechanism for exchanging 1 USDFC for $1 worth of FIL. Any holder can invoke it (as long as the system's total collateral ratio is at or above 110%), and the FIL comes from the collateral of the lowest-ratio Troves. That standing mechanism is what supports the price from below: whenever USDFC trades far enough below $1 that the discount exceeds the redemption fee and transaction costs, redeeming becomes profitable, and the resulting arbitrage pushes the price back toward $1.

{% hint style="success" %}
**What redemption gives holders**

* **Arbitrage** — buy USDFC below $1, redeem it for $1 of FIL, keep the difference
* **On-demand exit** — convert USDFC to FIL at the oracle price even when DEX liquidity is thin (subject to the conditions below)
{% endhint %}

## How it works

1. A holder submits USDFC for redemption.
2. The protocol pairs it against the Trove with the **lowest collateral ratio** (of those at 110% or above — Troves below that are left for [liquidation](liquidation.md)): the Trove's debt is reduced by the redeemed amount and an equal USD value of its FIL is released.
3. If one Trove isn't enough, the redemption continues into the next-lowest, until fulfilled.
4. The redeemer receives the FIL minus the [redemption fee](#redemption-fee); the fee itself is taken in FIL.

For the affected Trove owner this is a **forced swap**: debt falls by exactly the USD value of the collateral taken, valued at the oracle price with 1 USDFC counted as $1, so net position value is unchanged on those terms — but FIL exposure is gone from that slice, and if FIL later rises, that upside was surrendered. Keeping a higher ratio than the crowd moves you further back in the queue — it doesn't exempt you; the app's **Debt in front** figure shows how much debt stands between you and it ([details](../getting-started/monitoring-your-position.md#debt-in-front)).

{% hint style="warning" %}
**Redemption is not repayment.** Redemption targets Troves in collateral-ratio order and doesn't let you choose which one — it is not a way to pay down your own debt. To reduce your own debt, repay via Update Trove, which has no fee at all.
{% endhint %}

A redemption cannot leave a Trove's net debt below the 200 USDFC minimum. If the next partial redemption would do so, the redemption **stops there**: whatever was already processed goes through, and the unprocessed USDFC stays in the redeemer's wallet. A Trove that is redeemed in full is closed — its owner's remaining collateral is moved to the `CollSurplusPool` and can be claimed from the app.

## Redemption Fee

$$
\text{Redemption Fee (in FIL)} = (\text{Base Rate} + 0.5\%) \times \text{FIL drawn}
$$

* The fee is charged as a share of the FIL drawn from Troves and deducted from what you receive — in USD terms, (Base Rate + 0.5%) of the redeemed amount.
* **0.5%** is the floor. The [**Base Rate**](mint-and-borrow.md#base-rate-explanation) rises with each redemption — by 0.5 × (redeemed amount / total supply) — and decays with a 12-hour half-life. The increase from your own redemption is applied **before** your fee is calculated, so large redemptions pay a slightly higher rate than the one displayed beforehand.
* Unlike the borrowing fee, the redemption fee is **not capped at 5%** (the technical ceiling is 100%, at which point the redemption reverts), so a wave of redemptions makes further redemptions progressively more expensive.
* Redemptions are unavailable while the system's total collateral ratio is below 110%.

This dynamic fee is deliberate: it lets ordinary peg-restoring arbitrage through cheaply, but makes it prohibitively expensive to strip large amounts of collateral out of the system in a short window.

## The peg, from both sides

* **Below $1:** redemption arbitrage burns USDFC supply and pushes the price up (as long as the discount exceeds the current fee).
* **Above $1:** minting becomes the arbitrage — borrow at $1 of value per USDFC, sell at the premium — expanding supply and pushing the price down. The 110% collateral requirement is why the ceiling is softer than the floor.

**Worked example:** USDFC trades at $0.98, the Base Rate is 1.0%, and total supply is 1,000,000 USDFC. You buy 1,000 USDFC for $980 and redeem. Your redemption first raises the Base Rate by 0.5 × 1,000 / 1,000,000 = 0.05 percentage points, to 1.05%, so your fee is 1.55% — you receive $984.50 of FIL. Profit ≈ $4.50 before gas, and the next arbitrageur starts from the higher rate.

## Where next

* [Redeeming USDFC](../getting-started/redeeming-usdfc.md) — the hands-on guide
* [Mint & Borrow](mint-and-borrow.md#base-rate-explanation) — the Base Rate mechanics shared by both fees
* [Monitoring Your Position](../getting-started/monitoring-your-position.md) — how Trove owners track redemption risk
