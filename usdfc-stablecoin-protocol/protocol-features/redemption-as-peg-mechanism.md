---
description: The 3rd Party Redemption Mechanism to Maintain 1:1 Peg
---

# 📫 Redemption as Peg Mechanism

{% hint style="success" %}
**Benefits of Redemption**

* **Arbitrage Opportunity**: If USDFC dips below $1, buying and redeeming it for FIL can lock in potential gains and help restore the peg.
* **Direct FIL Access**: Redemption guarantees a way to swap USDFC for FIL, even when external exchange liquidity is low.
* **Reduced Market Impact**: Converting large FIL positions into USDFC through redemption avoids triggering selling pressure on open markets.
{% endhint %}

**Redemptions** in the Secured Finance protocol allow **USDFC holders** to exchange their USDFC for **Filecoin (FIL)** at an equivalent USD value, ensuring that **USDFC** maintains its peg to the USD. This function is available anytime while profitable when USDFC trades below 1.0 USD in exchanges.

## **Redemption Process**

* **Who Can Redeem**: Anyone holding USDFC can initiate a redemption, swapping USDFC for FIL at the peg value (**1 USDFC = 1 USD worth of FIL**).
* **Purpose**: This is not a debt repayment mechanism for borrowers. Instead, it is an exchange or swap function, allowing users to convert their **USDFC** holdings into FIL.
* **Steps**:
  1. A user submits a redemption request to the protocol.
  2. The protocol uses the FIL collateral from the **most under-collateralized Troves** to fulfill the request.
  3. The user receives FIL, while the Trove with the **highest risk** has its debt reduced but also loses collateral.

{% hint style="info" %}
Redemptions target Troves with the **lowest collateral ratios** first. Trove owners are advised to keep their collateral ratios well above the 110% minimum (ideally 150% or higher) to reduce the likelihood of being affected by redemptions. Troves affected by redemptions undergo **a forced swap** of USDFC for their collateral at the current spot rate, impacting their collateral balance.
{% endhint %}

### **Key Consideration**

<mark style="background-color:yellow;">**Not Debt Repayment**</mark><mark style="background-color:yellow;">: Redemption does not mean repaying borrowed USDFC.</mark> Instead, it allows the holder to exchange USDFC for FIL directly. Borrowers must repay their debt separately if they wish to close or manage their positions.

{% hint style="warning" %}
The system requires to keep a minimum borrowed amount of 180 USDFC and reserves an additional 20 USDFC as long as trove exists. **You cannot redeem** to reduce a trove's borrowed amount below 180 USDFC; if it would, the redemption amount will be automatically adjusted. However, you may redeem enough to fully close a trove (reducing the borrowed amount to 0). Redemption can span multiple troves, but the same minimum-borrow rule applies to each.
{% endhint %}

## **Redemption Fee**

The **Redemption Fee** is calculated as[ **Base Rate**](mint-and-borrow.md#base-rate-explanation) **+ 0.5%**, which ensures a minimum fee of **0.5%**. This fee dynamically adjusts depending on redemption activity:

* **Fee Calculation**:&#x20;

$$
\text{Redemption Fee} = (\text{Base Rate} + 0.5\%) \times \text{Redeemed USDFC}
$$

* **Base Rate** increases with frequent redemptions and decays over time when redemptions are low. It can never fall below **0.5%**, ensuring that the minimum fee is always charged.
* The more redemptions occur, the higher the **Base Rate** will rise, while a lack of redemptions leads the rate to decay back to the **0.5% minimum**.

{% hint style="info" %}
Note that the redeemed amount is taken into account for calculating the base rate and might have an impact on the redemption fee, especially if the amount is large.
{% endhint %}

***

## **Peg Mechanism**

The **peg mechanism** in the Secured Finance protocol ensures that **USDFC** maintains its stability around **1.0 USD**.

### **Below Peg (USDFC < 1.0 USD)**:

* When USDFC trades below 1.0 USD, users can redeem USDFC for FIL at a 1:1 rate, profiting from arbitrage. This reduces the circulating supply of USDFC, pushing its price back toward the peg.
* **Note**: Even in this scenario, the redemption fee (**Base Rate + 0.5%**) still applies, meaning users should factor in the cost of redemptions when calculating arbitrage opportunities.

### **Above Peg (USDFC > 1.0 USD)**:

* In this scenario, minting USDFC by depositing FIL becomes attractive because users can borrow USDFC at the 1:1 rate and sell it at a premium. This increases the circulating supply and pushes the price back toward 1.0 USD.
* **Note**: Minting requires **over-collateralization** (at least 110% FIL) and incurs a **one-time minting fee** (Base Rate + 0.5%), meaning users should account for these costs when minting USDFC above the peg.

***

## **Example of a Redemption**

1. **Market Situation**: USDFC trades at **0.98 USD**.
2. **Redemption Initiation**: Buy 1,000 USDFC with **980 USD** and user redeems **1,000 USDFC**.
3. **Redemption Fee**: Assume the **Base Rate** is **1.0%**.
   * Redemption Fee = **(1.0% + 0.5%) of 1,000 USDFC** = **15 USDFC**.
4. **Net Redemption**: The user receives FIL equivalent to **985 USD** after the fee is deducted. Net profit of **5 USD**.
