# ❓ FAQs

{% tabs %}
{% tab title="General" %}
### **What is Secured Finance?**

Secured Finance is a decentralized protocol offering both fixed-income lending and a stablecoin (USDFC), backed by Filecoin as collateral. It aims to provide users with transparent, secure borrowing and liquidity management.

### **What is USDFC?**

USDFC is the protocol’s USD-pegged stablecoin, minted by collateralizing Filecoin. It maintains a 1:1 peg to USD through mechanisms like redemptions and Stability Pool operations.

### **How can I use USDFC?**

After minting USDFC, you can:

* Provide liquidity to the Stability Pool.
* Supply liquidity to decentralized exchanges (DEXs).
* Lend it out via Secured Finance’s fixed-income markets.

### **What is the minimum collateral ratio?**

The protocol enforces a **minimum collateral ratio (MCR) of 110%** during normal operations, which increases to **150%** during Recovery Mode to ensure overall system stability.

### **What happens if USDFC loses its peg to the USD?**

If USDFC trades below 1.0 USD, users can redeem USDFC for FIL, which reduces the circulating supply and pushes the price back toward the peg. When USDFC trades above 1.0 USD, minting becomes more attractive, increasing the supply and stabilizing the price.
{% endtab %}

{% tab title="Minting" %}
### **How do I mint USDFC?**

Users deposit Filecoin to create USDFC, maintaining at least a 110% collateral ratio. The process involves a **one-time minting fee** (Base Rate + 0.5%) but no annual interest, unlike MakerDAO.

### **What are the costs associated with minting?**

The total minting cost includes the **one-time minting fee** and a **20 USDFC liquidation reserve** to cover potential liquidation gas costs.

### **Can I lose my collateral in a Trove?**

Yes, if your collateral ratio falls below 110%, your Trove becomes eligible for liquidation. You retain any minted USDFC, but you may lose some or all of your collateral if the Stability Pool absorbs your debt and distributes your collateral.

### **Is there an interest fee for borrowing?**

Currently, Secured Finance charges **0% interest** on minted USDFC, though a one-time minting fee applies. This interest-free model may change in the future depending on protocol updates.

### **What happens to the liquidation reserve if my Trove is not liquidated?**

If your Trove remains active and above the liquidation threshold, the **20 USDFC liquidation reserve** is refunded when you close the Trove.
{% endtab %}

{% tab title="Stability Pool and Liquidations" %}
### **How does the Stability Pool work?**

The Stability Pool holds USDFC to cover liquidations. When a Trove is liquidated, the pool burns an equivalent amount of USDFC and distributes the liquidated Filecoin to depositors at a discount.

### **What happens if the Stability Pool is empty?**

If the pool is empty, the protocol shifts to a **redistribution mechanism**. Debt and collateral from liquidated Troves are proportionally distributed to other active Troves, ensuring continued solvency.

### **Who triggers a liquidation, and what rewards do they receive?**

A **Liquidator** initiates the liquidation process when a Trove’s collateral ratio falls below 110%. They receive gas compensation from the liquidation reserve (20 USDFC) and a bonus of 0.5% of the liquidated collateral.

### **What is the risk of having a low collateral ratio?**

Troves with lower collateral ratios are at higher risk of liquidation, especially during market downturns. Maintaining a collateral ratio of at least 150% is recommended to reduce this risk and avoid forced liquidation.

### **What if I don’t want my Trove to be subject to redemptions?**

Redemptions target Troves with the lowest collateral ratios first. Keeping your collateral ratio above 150% can reduce the likelihood of your Trove being targeted during redemptions.
{% endtab %}

{% tab title="Redemption" %}
### **How does redemption work in Secured Finance?**

Redemption allows USDFC holders to exchange USDFC for FIL at a 1:1 USD value. Redemptions use the collateral from the riskiest Troves, reducing their debt and distributing their collateral to the redeemer.

### **What is the difference between repayment and redemption?**

**Redemption** is a function that allows users holding USDFC to exchange it for FIL collateral at a 1:1 USD value. It’s a direct swap and does not affect the redeemer’s debt. **Repayment**, on the other hand, is when a borrower uses USDFC to settle their debt and close or manage their Trove. Repayments reduce a borrower’s debt, while redemptions involve no debt reduction and instead target the riskiest Troves to balance the peg.

### **How does redemption affect the collateral ratio of Troves?**

Redemptions target Troves with the **lowest collateral ratios** first, forcing these Troves to exchange some of their collateral for USDFC. As a result, the collateral ratio of the redeemed Troves can increase after redemption, as their debt decreases while their remaining collateral is adjusted. Trove owners are encouraged to maintain collateral ratios above 150% to reduce the risk of being prioritized for redemptions.

### **Does redemption affect my debt directly?**

No, redemption is a swap for FIL and does not reduce your debt. Borrowers looking to repay their debt must do so separately, as redemptions are an exchange mechanism, not a debt repayment function.

### **What fees apply to redemptions?**

The **Redemption Fee** is calculated as **Base Rate + 0.5%**. Frequent redemptions increase the Base Rate, while low activity causes it to decay back to a 0.5% minimum.

### **Can redemptions be profitable?**

Yes, redemptions can be profitable if USDFC trades below 1.0 USD. However, users should consider the redemption fee and any fluctuations in FIL price to evaluate profitability accurately.
{% endtab %}

{% tab title="Recovery mode" %}
### **What is Recovery Mode?**

Recovery Mode is triggered when the **Total Collateral Ratio (TCR)** falls below **150%**. It enforces stricter liquidation rules, blocking actions that would lower the TCR further and setting borrowing fees to **0%** to encourage users to add collateral and stabilize the system.

### **How should users manage their Troves during Recovery Mode?**

To avoid liquidation, users should maintain their Troves’ collateral ratio above **150%** by adding collateral or repaying some of the debt.

### **Can I mint USDFC during Recovery Mode?**

Yes, but minting is restricted to actions that improve the TCR. You can only open a new Trove or adjust an existing Trove if the collateral ratio remains at least 150%.
{% endtab %}

{% tab title="Edge Cases" %}
### **What happens if the value of Filecoin drops sharply?**

A sharp drop in FIL value may push multiple Troves below the liquidation threshold, triggering liquidations to maintain solvency. In Recovery Mode, Troves below 150% collateral ratio are prioritized for liquidation.

### **What if I can’t add more collateral and my Trove is at risk?**

If unable to add collateral, consider repaying part of the debt to maintain your collateral ratio above 110% or, ideally, 150% to avoid liquidation or redemption.

### **What if USDFC is not maintaining its peg?**

If USDFC trades below 1.0 USD, redemptions can restore the peg by reducing circulating supply. If USDFC trades above 1.1 USD, increased minting can bring it back to the peg as more USDFC enters circulation. \*\*Consider the total cost of redeeming and minting.

### **Can I still interact with my Trove if I’m close to liquidation?**

Yes, you can add collateral or repay debt at any time to increase your collateral ratio and prevent liquidation. However, once your collateral ratio drops below 110%, your Trove becomes eligible for liquidation.
{% endtab %}
{% endtabs %}
