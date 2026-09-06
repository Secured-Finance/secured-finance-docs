---
description: What the protocol charges, when, and where it goes
---

# 🧀 Protocol Fees

The protocol charges exactly two fees — one when USDFC is minted, one when it is redeemed. There is no interest, no deposit or withdrawal fee, and no fee for adjusting collateral or repaying debt.

| Fee | When | Calculation | Range | Paid in |
| --- | --- | --- | --- | --- |
| Borrowing (minting) fee | Each time USDFC is minted | (Base Rate + 0.5%) × minted amount | 0.5% – 5% (capped) | USDFC (added to debt) |
| Redemption fee | Each redemption | (Base Rate + 0.5%) × redeemed amount | 0.5% minimum, no cap | FIL (deducted from proceeds) |

Both fees share the same [**Base Rate**](mint-and-borrow.md#base-rate-explanation), which rises with redemption activity and decays with a 12-hour half-life — so in calm conditions both sit at the 0.5% floor. The borrowing fee is **waived during [Recovery Mode](recovery-mode.md)**; the 20 USDFC Liquidation Reserve is not a fee (it's refunded on close — see [The Trove System](the-trove-system.md#debt-calculations)).

## Where the fees go


All fees are directed to the protocol's **Fee Reserve**. Following the Token Generation Event (TGE), the accumulated reserve is intended to be distributed to Secured Finance token stakers — aligning the protocol's revenue with its long-term supporters. Timing and mechanism will be announced ahead of the TGE.

Until then, fees simply accumulate; none are taken by any intermediary along the way.

## Why the fee design looks like this

* **A floor, not zero:** the 0.5% minimum makes minting-and-dumping or redemption-cycling unprofitable at the margin, without meaningfully taxing normal use.
* **One-time, not ongoing:** with no interest, the cost of a loan doesn't grow with its duration — USDFC is designed to be cheap to hold.
* **Base Rate coupling:** fees automatically rise exactly when the system is under redemption pressure and fall back when it isn't — a stabilizer that needs no governance action.

## Where next

* [Mint & Borrow](mint-and-borrow.md) — the borrowing fee in context
* [Redemption](redemption.md) — the redemption fee in context
