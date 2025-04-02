---
description: Leverage with Your Assets
---

# 🏋️‍♀️ Zero Coupon Bond as Collateral

At Secured Finance, we offer our users the innovative opportunity to use Zero Coupon Bond (ZC) as collateral for borrowing. This feature allows participants to leverage yield spread trading while enjoying the benefits of lending and borrowing on our platform. However, it's important to understand the specific conditions and risks associated with using ZC as collateral.

{% hint style="info" %}
Users' ZC bonds will be automatically used as collateral until the usage hits 80%. After that, cash collateral will be used.
{% endhint %}

### **Collateral Valuation**

When leveraging Zero Coupon Bonds (ZCs) as collateral on our platform, the valuation haircut is strategically set at 20% for loans in the same currency as the ZC. Conversely, for loans in a currency different from that of the ZC, a 100% haircut is currently applied.&#x20;

{% hint style="info" %}
We are actively exploring adjustments to this policy, aiming to reduce the haircut for different currency borrowings in the future. Factors such as liquidity, volatility, and correlation between currencies will guide these adjustments. Importantly, these potential changes may also be subject to community voting, allowing our users to have a direct impact on future collateral valuation policies.&#x20;
{% endhint %}

This nuanced approach to collateral valuation is essential for users to understand as they devise their trading strategies and manage their collateral assets effectively, with the added dimension of community-driven governance enhancing the platform's adaptability and responsiveness to user needs.

### Understanding Collateral Utilization Ratio and LTV with Zero Coupon Bonds

Leveraging Zero Coupon Bonds (ZCs) as collateral on our platform requires an understanding of both the collateral utilization ratio and the Loan-to-Value (LTV) ratio, especially for loans in the same currency as the ZC. Our approach aims to maximize the efficiency of your assets while maintaining a prudent risk profile.

#### **ZC Collateral Utilization**

When you secure a loan in the same currency as your ZC, our system implements a specialized collateral utilization strategy. If you're borrowing against a ZC that's denominated in the same currency, the platform prioritizes this ZC as your primary collateral. This prioritization allows for the ZC to be utilized first, up to 80% of its Present Value (PV), before any cash collateral is considered. This method ensures that your ZC assets are leveraged effectively, enhancing your borrowing capabilities. Our platform display the ZC utilization ratio for each currency by the formulaic below.

$$
\text{ZC Utilization} = \frac{\text{Obligation}}{\text{Total ZC}}
$$

#### **Adjusted Loan-to-Value (LTV) Calculation with ZC Collateral**

The standard formula for calculating the Loan-to-Value (LTV) ratio is:

$$
LTV = \frac{\text{Obligation}}{\text{Cash Collateral}}
$$

However, when the obligation currency matches the currency of the ZC you own, the LTV calculation adjusts to incorporate the ZC collateral. The adjusted formula becomes:

$$
\text{LTV (with ZC collateral)} = \frac{\text{Obligation}}{\text{Cash Collateral} + \text{Consumed ZC Collateral}}
$$

In this formula, ZC Collateral is considered alongside cash collateral. We aggregate the cash and the Consumed ZC amount to cover the obligation. The system is designed to cover 125% of the obligation and utilize up to 80% of the total ZC amount.

> Even without pledging any Cash Collateral, you can still borrow in the same currency to engage in Yield Spread Strategy.

### **Liquidation Process with ZC collateral**

In the event of a liquidation trigger, liquidators have the flexibility to choose the currency of both the obligation and the collateral, which may include the ZC. It's important to note that even if the Loan-to-Value (LTV) threshold is breached due to fluctuations in **one currency**, your position may be subject to liquidation in **another currency** along with the collateral.

This mechanism underscores the importance of vigilant collateral management. Users must be aware that the liquidation process can lead to scenarios where the collateral, including ZC, is liquidated in a currency different from the one that triggered the LTV threshold.

### **Risk Management**

Utilizing ZC as collateral offers a unique avenue for capitalizing on yield spreads. However, it comes with its set of risks, primarily due to price fluctuations and the potential for liquidation in a different currency. We urge our users to exercise caution and continuously monitor their collateral positions to mitigate risks and avoid unintended liquidations.
