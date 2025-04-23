---
description: The mechanism that maintains USDFC's 1:1 peg to the US Dollar
---

# 💸 Redemption

## Overview

The Redemption Mechanism is a critical component of the USDFC Stablecoin Protocol that allows USDFC holders to exchange their tokens for Filecoin (FIL) at face value. This direct conversion path creates arbitrage opportunities that help maintain USDFC's peg to the US Dollar, especially when the market price falls below $1.

{% hint style="success" %}
**Benefits of Redemption**

* **Arbitrage Opportunity**: If USDFC dips below $1, buying and redeeming it for FIL can lock in potential gains and help restore the peg
* **Direct FIL Access**: Redemption guarantees a way to swap USDFC for FIL, even when external exchange liquidity is low
* **Reduced Market Impact**: Converting large FIL positions into USDFC through redemption avoids triggering selling pressure on open markets
{% endhint %}

## How It Works

The redemption process allows any USDFC holder to exchange their tokens for FIL at the current USD value, targeting Troves with the lowest collateral ratios first:

1. A user submits a redemption request to the protocol
2. The protocol uses the FIL collateral from the most under-collateralized Troves to fulfill the request
3. The user receives FIL, while the targeted Troves have their debt reduced but also lose collateral

{% hint style="info" %}
Redemptions target Troves with the **lowest collateral ratios** first. Trove owners are advised to keep their collateral ratios well above the 110% minimum (ideally 150% or higher) to reduce the likelihood of being affected by redemptions. Troves affected by redemptions undergo **a forced swap** of USDFC for their collateral at the current spot rate, impacting their collateral balance.
{% endhint %}

### Important Distinction

<mark style="background-color:yellow;">**Not Debt Repayment**</mark><mark style="background-color:yellow;">: Redemption does not mean repaying borrowed USDFC.</mark> Instead, it allows the holder to exchange USDFC for FIL directly. Borrowers must repay their debt separately if they wish to close or manage their positions.

{% hint style="warning" %}
The system requires a minimum borrowed amount of 180 USDFC and reserves an additional 20 USDFC as long as trove exists. **You cannot redeem** to reduce a trove's borrowed amount below 180 USDFC; if it would, the redemption amount will be automatically adjusted. However, you may redeem enough to fully close a trove (reducing the borrowed amount to 0). Redemption can span multiple troves, but the same minimum-borrow rule applies to each.
{% endhint %}

## Key Parameters

| Parameter          | Description                                                | Default Value    |
| ------------------ | ---------------------------------------------------------- | ---------------- |
| Redemption Fee     | Fee charged on redemption transactions                     | Base Rate + 0.5% |
| Minimum Fee        | Minimum fee regardless of Base Rate                        | 0.5%             |
| Base Rate          | Variable component that increases with redemption activity | 0% to 4.5%       |
| Minimum Trove Size | Minimum USDFC debt a Trove must maintain                   | 180 USDFC        |

## Redemption Fee

The **Redemption Fee** is calculated as [**Base Rate**](mint-and-borrow.md#base-rate) + 0.5%, which ensures a minimum fee of **0.5%**. This fee dynamically adjusts depending on redemption activity:

$$\text{Redemption Fee} = (\text{Base Rate} + 0.5\%) \times \text{Redeemed USDFC}$$

* **Base Rate** increases with frequent redemptions and decays over time when redemptions are low
* The more redemptions occur, the higher the **Base Rate** will rise, while a lack of redemptions leads the rate to decay back to the **0.5% minimum**

{% hint style="info" %}
Note that the redeemed amount is taken into account for calculating the base rate and might have an impact on the redemption fee, especially if the amount is large.
{% endhint %}

## Peg Mechanism

The redemption mechanism works alongside minting to maintain USDFC's stability around **1.0 USD**:

### Below Peg (USDFC < 1.0 USD)

* When USDFC trades below 1.0 USD, users can redeem USDFC for FIL at a 1:1 rate, profiting from arbitrage
* This reduces the circulating supply of USDFC, pushing its price back toward the peg
* The redemption fee (Base Rate + 0.5%) still applies, meaning users should factor in the cost when calculating arbitrage opportunities

### Above Peg (USDFC > 1.0 USD)

* In this scenario, minting USDFC by depositing FIL becomes attractive because users can borrow USDFC at the 1:1 rate and sell it at a premium
* This increases the circulating supply and pushes the price back toward 1.0 USD
* Minting requires over-collateralization (at least 110% FIL) and incurs a one-time minting fee (Base Rate + 0.5%)

## Example of a Redemption

1. **Market Situation**: USDFC trades at **0.98 USD**
2. **Redemption Initiation**: Buy 1,000 USDFC with **980 USD** and user redeems **1,000 USDFC**
3. **Redemption Fee**: Assume the **Base Rate** is **1.0%**
   * Redemption Fee = **(1.0% + 0.5%) of 1,000 USDFC** = **15 USDFC**
4. **Net Redemption**: The user receives FIL equivalent to **985 USD** after the fee is deducted. Net profit of **5 USD**

## Common Questions

**Can I redeem USDFC to pay back my own debt?**\
No, redemption is not a debt repayment mechanism. It's a separate process that allows USDFC holders to exchange their tokens for FIL at face value.

**How can I avoid having my Trove targeted by redemptions?**\
Maintain a higher collateral ratio than other Troves in the system. Redemptions always target Troves with the lowest collateral ratios first.

**Is there a limit to how much USDFC can be redeemed at once?**\
There's no hard cap, but large redemptions may be limited by the available collateral in under-collateralized Troves and will incur higher fees as the Base Rate increases.

[Learn more in the FAQs section](../faqs.md)

## Related Topics

* [The Trove System](the-trove-system.md)
* [Mint & Borrow](mint-and-borrow.md)
* [Liquidation](liquidation.md)
* [Protocol Fees](protocol-fees.md)
