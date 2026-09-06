---
description: Creating USDFC against FIL collateral — costs, fees, and the Base Rate
---

# 💰 Mint & Borrow

Minting is how USDFC comes into existence: you lock FIL in a [Trove](the-trove-system.md) and the protocol issues new USDFC to your wallet as debt. You get dollar liquidity without selling FIL — keeping your upside exposure — and repay on your own schedule, with no interest accruing.

{% hint style="success" %}
**Why mint instead of sell?**

* Instant dollar liquidity while keeping FIL price exposure
* No counterparty, order book, or exchange involved
* One-time fee, zero ongoing interest
{% endhint %}

## The flow

1. **Open a Trove** with FIL collateral and choose a borrow amount (minimum 200 USDFC), keeping the collateral ratio above **110%** — e.g. $1,000 of FIL supports at most ~909 USDFC of total debt.
2. **Receive the full amount.** The USDFC you requested arrives in your wallet; the fee and Liquidation Reserve are added to your *debt*, not deducted from the transfer.
3. **Maintain the ratio.** If FIL falls, add collateral or repay to stay clear of [liquidation](liquidation.md). Be aware your Trove can also be affected by [redemption](redemption.md) if its ratio is among the lowest.
4. **Adjust or close whenever.** Borrow more, repay, or close entirely by repaying the total debt (see the [walkthrough](../getting-started/minting-usdfc-step-by-step.md)).

## Minting costs

Two amounts are added to your debt when you mint:

### 1. Liquidation Reserve

* A **20 USDFC** reserve added to your debt while the Trove exists — not a fee.
* It compensates the liquidator's gas if your Trove is ever liquidated; otherwise it is **refunded in full** when you close the Trove.

### 2. One-Time Minting Fees

$$
\text{One-Time Minting Fee} = (\text{Base Rate} + 0.5\%) \times \text{Minted USDFC}
$$

* **0.5%** is the fixed floor; the **Base Rate** component varies with system conditions (see below).
* The total is **capped at 5%** of the minted amount, and the whole fee is **waived during [Recovery Mode](recovery-mode.md)**.
* Charged per mint — borrowing more later incurs the fee again on the new amount.

**Example** — mint 4,000 USDFC while the Base Rate is 0.5%:

* One-Time Minting Fee: (0.5% + 0.5%) × 4,000 = 40 USDFC
* Liquidation Reserve: 20 USDFC
* **Total Debt: 4,060 USDFC**, while 4,000 USDFC arrives in your wallet

In calm conditions the Base Rate sits at 0%, making the typical fee exactly 0.5%.

## Base Rate Explanation

The **Base Rate** is a single system-wide variable that couples fees to redemption pressure.

* **It rises with redemptions:** each redemption increases it by $$0.5 \times \frac{m}{n}$$ where *m* is the USDFC redeemed and *n* the total supply.
* **It decays over time** with a **12-hour half-life** (per-hour factor ≈ 0.944), evaluated whenever a new mint or redemption occurs. With no redemption activity it drifts back toward 0%.
* For the minting fee, its effect is capped: fee = min(Base Rate + 0.5%, 5%). The [redemption fee](redemption.md#redemption-fee) uses the same Base Rate but has no 5% cap.

**Why it exists:** a redemption wave signals USDFC trading below peg. A rising Base Rate makes further redemptions more expensive (throttling the drain on collateral) and makes minting new supply more expensive (slowing supply growth until the peg recovers). When calm returns, the rate decays and fees fall back to the floor.

## Interest Rate

The protocol charges **no ongoing interest** on USDFC debt — the borrowing fee is the entire cost of a loan, however long you hold it. This is a deliberate choice to make USDFC cheap to hold and encourage adoption across the Filecoin ecosystem.

{% hint style="info" %}
An interest rate on borrowed USDFC may be introduced in the future to support the protocol's long-term sustainability. Any such change would be announced in advance.
{% endhint %}

## Where next

* [Protocol Fees](protocol-fees.md) — where the fees go
* [The Trove System](the-trove-system.md) — debt math and the Trove lifecycle
* [Minting USDFC Step-by-Step](../getting-started/minting-usdfc-step-by-step.md) — the hands-on guide
