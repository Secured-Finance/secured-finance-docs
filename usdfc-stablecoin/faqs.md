---
description: Comprehensive answers to frequently asked questions about USDFC Stablecoin
---

# ❓ USDFC Stablecoin FAQs

## Overview

This FAQ covers everything you need to know about USDFC, from basic concepts to advanced operations and troubleshooting. Whether you're new to stablecoins or looking for specific technical details, you'll find comprehensive answers here.

## What You'll Learn

- How USDFC stablecoin works and its key features
- Step-by-step processes for minting, managing, and redeeming USDFC
- Risk management and liquidation mechanics
- Advanced topics like Recovery Mode and edge cases
- Stability Pool participation and rewards

## Quick Navigation

- [Getting Started](#getting-started)
- [Minting & Borrowing](#minting--borrowing)
- [Risk Management](#risk-management)
- [Advanced Topics](#advanced-topics)

## Getting Started

<details>
<summary>What is Secured Finance?</summary>

Secured Finance is a decentralized finance platform that facilitates peer-to-contract lending and derivatives trading. Built on multiple blockchains including Ethereum, Arbitrum, and Filecoin, it offers a transparent, robust, and cost-effective alternative to traditional financial institutions.

The platform consists of two main products:
- **Fixed-Rate Lending Protocol**: Enables fixed-rate, fixed-term lending and borrowing through zero-coupon bonds
- **USDFC Stablecoin**: A dollar-pegged stablecoin backed by Filecoin collateral

**Related:** [Platform Overview](../../introduction/overview.md)
</details>

<details>
<summary>What is USDFC?</summary>

USDFC is a decentralized stablecoin pegged to the US Dollar and backed by Filecoin (FIL) collateral. It's designed to maintain its value at $1 USD through over-collateralization and various stability mechanisms.

**Key features:**
- **Decentralized**: No central authority controls USDFC
- **Over-collateralized**: Backed by at least 110% FIL collateral
- **Redeemable**: Exchange USDFC for underlying FIL anytime
- **Yield-generating**: Earn rewards through Stability Pool participation

**Related:** [USDFC Overview](../overview.md)
</details>

<details>
<summary>How does USDFC maintain its peg to the US Dollar?</summary>

USDFC maintains its $1 peg through multiple mechanisms:

1. **Over-collateralization**: Minimum 110% FIL collateral backing
2. **Redemption mechanism**: Direct exchange of USDFC for FIL at $1 rate
3. **Liquidation system**: Automatic closure of under-collateralized positions
4. **Stability Pool**: Buffer that absorbs liquidated debt
5. **Arbitrage opportunities**: Market forces help restore peg when deviations occur

These mechanisms work together to create strong economic incentives for maintaining the peg.

**Related:** [System Overview](../core-mechanics/system-overview.md)
</details>

<details>
<summary>What are the benefits of using USDFC?</summary>

USDFC offers several advantages:

**For Users:**
- **Stable value**: Maintains $1 peg for predictable purchasing power
- **Decentralized**: No reliance on traditional banking systems
- **Transparent**: All operations recorded on blockchain
- **Yield opportunities**: Earn rewards through Stability Pool

**For DeFi:**
- **Composability**: Use in other DeFi protocols
- **Liquidity**: Trade on decentralized exchanges
- **Collateral**: Use as collateral for other loans

**Related:** [USDFC Overview](../overview.md)
</details>

<details>
<summary>How do I get started with USDFC?</summary>

To get started with USDFC:

1. **Set up a wallet**: Use a Web3 wallet like MetaMask
2. **Acquire FIL**: Purchase Filecoin on exchanges
3. **Connect to platform**: Access the USDFC interface
4. **Create a Trove**: Deposit FIL as collateral
5. **Mint USDFC**: Borrow against your collateral
6. **Manage position**: Monitor and maintain healthy ratios

**Related:** [Getting Started Guide](../getting-started/README.md)
</details>

## Minting & Borrowing

<details>
<summary>How do I mint USDFC?</summary>

To mint USDFC:

1. **Connect your wallet** to the USDFC platform
2. **Create a Trove** by depositing FIL as collateral
3. **Set collateral ratio** (minimum 110%, recommended 150%+)
4. **Mint USDFC** against your collateral
5. **Pay borrowing fee** (currently 0.5% of minted amount)
6. **Confirm transaction** and receive USDFC

**Example:**
- Deposit 100 FIL worth $500
- Mint 400 USDFC (125% collateral ratio)
- Pay 2 USDFC borrowing fee
- Receive 398 USDFC in your wallet

**Related:** [Minting USDFC Step-by-Step](../getting-started/minting-usdfc-step-by-step.md)
</details>

<details>
<summary>What is the minimum collateral ratio?</summary>

The minimum collateral ratio for USDFC is **110%**. This means:

- Deposit at least $110 worth of FIL to mint $100 USDFC
- If your ratio falls below 110%, liquidation may occur
- **Recommended ratio**: 150% or higher for safety margin

**Calculation:**
$$
\text{Collateral Ratio} = \frac{\text{FIL Value}}{\text{USDFC Debt}} \times 100\%
$$

**Related:** [Collateral Ratio](../core-mechanics/liquidation/collateral-ratio.md)
</details>

<details>
<summary>What fees are involved in minting USDFC?</summary>

When minting USDFC, you pay:

**One-time fees:**
- **Borrowing Fee**: 0.5% of minted USDFC amount
- **Gas Fees**: Network transaction fees in FIL

**No ongoing fees:**
- No interest payments
- No maintenance fees
- No time-based charges

**Example:** Minting 1,000 USDFC costs 5 USDFC borrowing fee plus gas.

**Related:** [Protocol Fees](../core-mechanics/protocol-fees.md)
</details>

<details>
<summary>Can I mint more USDFC from an existing Trove?</summary>

Yes, you can mint additional USDFC from an existing Trove if:

1. **Collateral ratio remains above 110%** after minting
2. **You pay the borrowing fee** on additional USDFC
3. **Sufficient FIL collateral** supports the new total debt

**Process:**
1. Access your existing Trove
2. Calculate new collateral ratio
3. Mint additional USDFC
4. Pay borrowing fee on new amount only

**Related:** [Managing Collateral Effectively](../getting-started/managing-collateral-effectively.md)
</details>

<details>
<summary>What happens if I want to close my Trove?</summary>

To close your Trove:

1. **Repay all USDFC debt** including any fees
2. **Confirm closure transaction** 
3. **Receive all FIL collateral** back to your wallet
4. **Pay gas fees** for the transaction

**Requirements:**
- Must repay 100% of USDFC debt
- Cannot partially close a Trove
- Trove is permanently removed after closure

**Related:** [Monitoring Your Position](../getting-started/monitoring-your-position.md)
</details>

## Risk Management

<details>
<summary>What is the Stability Pool?</summary>

The Stability Pool is a pool of USDFC tokens that acts as a buffer to absorb debt from liquidated Troves. It provides system stability and rewards for participants.

**How it works:**
1. **Users deposit USDFC** into the pool
2. **Liquidated debt** is paid using pool funds
3. **Liquidated FIL collateral** is distributed to depositors
4. **Depositors typically profit** from liquidation premiums

**Related:** [Using the Stability Pool](../getting-started/using-the-stability-pool.md)
</details>

<details>
<summary>How do liquidations work?</summary>

When a Trove's collateral ratio falls below 110%:

1. **Liquidation trigger**: Anyone can initiate liquidation
2. **Debt payment**: Stability Pool USDFC pays off the debt
3. **Collateral distribution**: FIL collateral goes to Stability Pool depositors
4. **Liquidator reward**: Liquidator receives 0.5% of collateral

**Example:**
- Trove has 100 FIL ($400) and 380 USDFC debt
- Collateral ratio = 105% (below 110%)
- Liquidation occurs, Stability Pool receives ~$400 FIL for $380 debt

**Related:** [Liquidation Process](../core-mechanics/liquidation.md)
</details>

<details>
<summary>What are the benefits of depositing in the Stability Pool?</summary>

Stability Pool depositors receive:

**Rewards:**
- **FIL from liquidations**: Typically profitable due to 110%+ collateral
- **Liquidation premiums**: Receive more value than USDFC deposited
- **System rewards**: Potential additional token rewards

**Example profit:**
- Deposit 1,000 USDFC
- Liquidation occurs, receive 1,100 USDFC worth of FIL
- Net profit: 100 USDFC equivalent

**Related:** [Using the Stability Pool](../getting-started/using-the-stability-pool.md)
</details>

<details>
<summary>What are the risks of the Stability Pool?</summary>

Risks include:

1. **USDFC reduction**: Your deposit decreases during liquidations
2. **FIL price volatility**: Received FIL may fluctuate in value
3. **Opportunity cost**: Might miss FIL price appreciation
4. **Smart contract risk**: Protocol vulnerabilities (though audited)

**Mitigation strategies:**
- **Diversify exposure**: Don't deposit all USDFC
- **Monitor FIL price**: Consider market conditions
- **Understand mechanics**: Know when liquidations likely occur

**Related:** [Using the Stability Pool](../getting-started/using-the-stability-pool.md)
</details>

## Advanced Topics

<details>
<summary>What is redemption and how does it work?</summary>

Redemption allows USDFC holders to exchange their USDFC for underlying FIL collateral directly from the protocol at face value.

**Process:**
1. **Submit redemption request** with USDFC amount
2. **Protocol selects Troves** with lowest collateral ratios
3. **Receive equivalent FIL** based on current price
4. **Pay redemption fee** (0.5% base + dynamic component)

**Use cases:**
- **Arbitrage**: When USDFC trades below $1
- **Exit strategy**: Convert back to FIL
- **Peg maintenance**: Helps maintain $1 peg

**Related:** [Redemption Process](../core-mechanics/redemption.md)
</details>

<details>
<summary>What is Recovery Mode?</summary>

Recovery Mode activates when the system's Total Collateral Ratio (TCR) falls below 150%. It implements stricter rules to restore system health.

**Changes in Recovery Mode:**
- **Lower liquidation threshold**: Troves below 150% can be liquidated
- **Partial liquidations**: Only liquidate enough to reach 150%
- **Restricted operations**: Limited new borrowing
- **Higher requirements**: New Troves need 150% minimum ratio

**User actions:**
- **Add collateral** to improve your ratio
- **Repay debt** to reduce liquidation risk
- **Monitor closely** for system status updates

**Related:** [Recovery Mode](../advanced-topics/recovery-mode.md)
</details>

<details>
<summary>What happens if the Stability Pool is empty during liquidation?</summary>

If the Stability Pool is empty when liquidation occurs:

1. **Redistribution mechanism**: Debt and collateral redistribute to all Troves
2. **Proportional allocation**: Based on each Trove's existing debt
3. **Automatic updates**: Positions adjust automatically
4. **No user action required**: System handles redistribution

**Impact on Trove owners:**
- **Debt increases**: Receive portion of liquidated debt
- **Collateral increases**: Receive portion of liquidated FIL
- **Ratio may improve**: Net effect often positive

**Related:** [Liquidation Process](../core-mechanics/liquidation.md)
</details>

<details>
<summary>What if FIL price crashes significantly?</summary>

In case of severe FIL price decline:

1. **Mass liquidations**: Many Troves become under-collateralized
2. **Recovery Mode**: System automatically activates
3. **Stability mechanisms**: Built-in protections engage
4. **Market forces**: Arbitrage opportunities help stabilize

**User protections:**
- **Over-collateralization**: 110%+ provides buffer
- **Liquidation premiums**: Incentivize quick liquidations
- **Redemption mechanism**: Maintains peg pressure

**Related:** [Recovery Mode](../advanced-topics/recovery-mode.md)
</details>

## Related Resources

- [Getting Started Guide](../getting-started/README.md)
- [Core Mechanics Documentation](../core-mechanics/README.md)
- [Advanced Topics](../advanced-topics/README.md)
- [System Overview](../core-mechanics/system-overview.md)
- [Developer Portal](../../developer-portal/introduction.md)
# ❓ FAQs

{% tabs %}
{% tab title="General" %}
#### **What is Secured Finance?**

Secured Finance is a decentralized protocol offering both fixed-income lending and a stablecoin (USDFC), backed by Filecoin as collateral. It aims to provide users with transparent, secure borrowing and liquidity management.

#### **What is USDFC?**

USDFC is the protocol’s USD-pegged stablecoin, minted by collateralizing Filecoin. It maintains a 1:1 peg to USD through mechanisms like redemptions and Stability Pool operations.

#### **How can I use USDFC?**

After minting USDFC, you can:

* Provide liquidity to the Stability Pool.
* Supply liquidity to decentralized exchanges (DEXs).
* Lend it out via Secured Finance’s fixed-income markets.

#### **What is the minimum collateral ratio?**

The protocol enforces a **minimum collateral ratio (MCR) of 110%** during normal operations, which increases to **150%** during Recovery Mode to ensure overall system stability.

#### **What happens if USDFC loses its peg to the USD?**

If USDFC trades below 1.0 USD, users can redeem USDFC for FIL, which reduces the circulating supply and pushes the price back toward the peg. When USDFC trades above 1.0 USD, minting becomes more attractive, increasing the supply and stabilizing the price.
{% endtab %}

{% tab title="Minting" %}
#### **How do I mint USDFC?**

Users deposit Filecoin to create USDFC, maintaining at least a 110% collateral ratio. The process involves a **one-time minting fee** (Base Rate + 0.5%) but no annual interest, unlike MakerDAO.

#### **What are the costs associated with minting?**

The total minting cost includes the **one-time minting fee** and a **20 USDFC liquidation reserve** to cover potential liquidation gas costs.

#### **Can I lose my collateral in a Trove?**

Yes, if your collateral ratio falls below 110%, your Trove becomes eligible for liquidation. You retain any minted USDFC, but you may lose some or all of your collateral if the Stability Pool absorbs your debt and distributes your collateral.

#### **Is there an interest fee for borrowing?**

Currently, Secured Finance charges **0% interest** on minted USDFC, though a one-time minting fee applies. This interest-free model may change in the future depending on protocol updates.

#### **What happens to the liquidation reserve if my Trove is not liquidated?**

If your Trove remains active and above the liquidation threshold, the **20 USDFC liquidation reserve** is refunded when you close the Trove.
{% endtab %}

{% tab title="Stability Pool and Liquidations" %}
#### **How does the Stability Pool work?**

The Stability Pool holds USDFC to cover liquidations. When a Trove is liquidated, the pool burns an equivalent amount of USDFC and distributes the liquidated Filecoin to depositors at a discount.

#### **What happens if the Stability Pool is empty?**

If the pool is empty, the protocol shifts to a **redistribution mechanism**. Debt and collateral from liquidated Troves are proportionally distributed to other active Troves, ensuring continued solvency.

#### **Who triggers a liquidation, and what rewards do they receive?**

A **Liquidator** initiates the liquidation process when a Trove’s collateral ratio falls below 110%. They receive gas compensation from the liquidation reserve (20 USDFC) and a bonus of 0.5% of the liquidated collateral.

#### **What is the risk of having a low collateral ratio?**

Troves with lower collateral ratios are at higher risk of liquidation, especially during market downturns. Maintaining a collateral ratio of at least 150% is recommended to reduce this risk and avoid forced liquidation.

#### **What if I don’t want my Trove to be subject to redemptions?**

Redemptions target Troves with the lowest collateral ratios first. Keeping your collateral ratio above 150% can reduce the likelihood of your Trove being targeted during redemptions.
{% endtab %}

{% tab title="Redemption" %}
#### **How does redemption work in Secured Finance?**

Redemption allows USDFC holders to exchange USDFC for FIL at a 1:1 USD value. Redemptions use the collateral from the riskiest Troves, reducing their debt and distributing their collateral to the redeemer.

#### **What is the difference between repayment and redemption?**

**Redemption** is a function that allows users holding USDFC to exchange it for FIL collateral at a 1:1 USD value. It’s a direct swap and does not affect the redeemer’s debt. **Repayment**, on the other hand, is when a borrower uses USDFC to settle their debt and close or manage their Trove. Repayments reduce a borrower’s debt, while redemptions involve no debt reduction and instead target the riskiest Troves to balance the peg.

#### **How does redemption affect the collateral ratio of Troves?**

Redemptions target Troves with the **lowest collateral ratios** first, forcing these Troves to exchange some of their collateral for USDFC. As a result, the collateral ratio of the redeemed Troves can increase after redemption, as their debt decreases while their remaining collateral is adjusted. Trove owners are encouraged to maintain collateral ratios above 150% to reduce the risk of being prioritized for redemptions.

#### **Does redemption affect my debt directly?**

No, redemption is a swap for FIL and does not reduce your debt. Borrowers looking to repay their debt must do so separately, as redemptions are an exchange mechanism, not a debt repayment function.

#### **What fees apply to redemptions?**

The **Redemption Fee** is calculated as **Base Rate + 0.5%**. Frequent redemptions increase the Base Rate, while low activity causes it to decay back to a 0.5% minimum.

#### **Can redemptions be profitable?**

Yes, redemptions can be profitable if USDFC trades below 1.0 USD. However, users should consider the redemption fee and any fluctuations in FIL price to evaluate profitability accurately.
{% endtab %}

{% tab title="Recovery mode" %}
#### **What is Recovery Mode?**

Recovery Mode is triggered when the **Total Collateral Ratio (TCR)** falls below **150%**. It enforces stricter liquidation rules, blocking actions that would lower the TCR further and setting borrowing fees to **0%** to encourage users to add collateral and stabilize the system.

#### **How should users manage their Troves during Recovery Mode?**

To avoid liquidation, users should maintain their Troves’ collateral ratio above **150%** by adding collateral or repaying some of the debt.

#### **Can I mint USDFC during Recovery Mode?**

Yes, but minting is restricted to actions that improve the TCR. You can only open a new Trove or adjust an existing Trove if the collateral ratio remains at least 150%.
{% endtab %}

{% tab title="Edge Cases" %}
#### **What happens if the value of Filecoin drops sharply?**

A sharp drop in FIL value may push multiple Troves below the liquidation threshold, triggering liquidations to maintain solvency. In Recovery Mode, Troves below 150% collateral ratio are prioritized for liquidation.

#### **What if I can’t add more collateral and my Trove is at risk?**

If unable to add collateral, consider repaying part of the debt to maintain your collateral ratio above 110% or, ideally, 150% to avoid liquidation or redemption.

#### **What if USDFC is not maintaining its peg?**

If USDFC trades below 1.0 USD, redemptions can restore the peg by reducing circulating supply. If USDFC trades above 1.1 USD, increased minting can bring it back to the peg as more USDFC enters circulation. \*\*Consider the total cost of redeeming and minting.

#### **Can I still interact with my Trove if I’m close to liquidation?**

Yes, you can add collateral or repay debt at any time to increase your collateral ratio and prevent liquidation. However, once your collateral ratio drops below 110%, your Trove becomes eligible for liquidation.
{% endtab %}
{% endtabs %}
