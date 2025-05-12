---
description: Learn how to redeem your USDFC for FIL collateral under certain conditions
---

# 💸 Redeeming USDFC

## Prerequisites

* USDFC tokens in your wallet
* Access to the [USDFC application](https://app.usdfc.net)
* Connected wallet with enough FIL for gas fees
* Understanding of repayment with trove adjustments
* Understanding of redemption mechanics and fees

## Overview

Redemption is a process that allows you to exchange your USDFC for FIL collateral at face value (1 USDFC = $1 worth of FIL). This mechanism helps maintain the USDFC peg to the US dollar. This guide will walk you through the redemption process and help you understand when redemption is beneficial.

{% hint style="warning" %}
Repayment is adjusting your trove. However, the redemption is adjusting 3rd party's lowest collateral trove. \
To avoid getting redemption, please watch 'Debt in front' amount and increase the collateral ratio.
{% endhint %}

## Step 1: Access the Redemption Feature

First, you need to navigate to the redemption section in the USDFC application.

1. Navigate to the [USDFC application](https://app.usdfc.net)
2. Connect your wallet if not already connected
3. Locate the "Redemption" page in the "More" tab in the USDFC application

<figure><img src="../../.gitbook/assets/image (136).png" alt=""><figcaption><p>The Redemption page location in the "More" tab</p></figcaption></figure>

## Step 2: Review Redemption Information

Before proceeding, review the current redemption information.

1. Check the current redemption fee (variable based on the base rate)
2. Understand which Troves will be affected by your redemption
3. Review the current FIL price and calculate how much FIL you'll receive

<figure><img src="../../.gitbook/assets/image (137).png" alt=""><figcaption><p>Screenshot of the redemption information page</p></figcaption></figure>

## Step 3: Enter Redemption Amount

Now you can specify how much USDFC you want to redeem.

1. Enter the amount of USDFC you want to redeem
2. The system will calculate the amount of FIL you will receive based on the current FIL price
3. Review the redemption fee that will be applied
4. Understand which Troves will be affected (redemptions start from the lowest collateral ratio Troves)

<figure><img src="../../.gitbook/assets/image (138).png" alt=""><figcaption><p>The lowest Collateral Ratio Troves get redeemed</p></figcaption></figure>

## Step 4: Review Transaction Details

Before confirming, review all transaction details carefully.

1. Check the USDFC amount you're redeeming
2. Verify the FIL amount you'll receive
3. Review the redemption fee
4. Understand the gas costs for the transaction

<figure><img src="../../.gitbook/assets/image (139).png" alt=""><figcaption><p>The Redemption section shows all relevant details</p></figcaption></figure>

## Step 5: Confirm and Execute Redemption

Once you're satisfied with the details, you can proceed with the redemption.

1. Click the "Confirm" button
2. Confirm the transaction in your wallet
3. Wait for the transaction to be processed on the blockchain

<figure><img src="../../.gitbook/assets/image (140).png" alt=""><figcaption><p>Screenshot showing updated wallet balances after redemption</p></figcaption></figure>

\[Image: Screenshot of the confirmation screen with the "Redeem" button highlighted]

## Step 6: Verify Redemption

After the transaction is confirmed, verify that your redemption was successful.

1. Check that your USDFC balance has decreased by the redeemed amount
2. Verify that the FIL has been added to your wallet balance
3. Review the transaction details in your wallet history or on a blockchain explorer

<figure><img src="../../.gitbook/assets/image (141).png" alt=""><figcaption><p>Lowest Collateral Ratio Trove's FIL Collateral and USDFC Debt was reduced</p></figcaption></figure>

## Understanding Redemption Mechanics

### How Redemption Works

1. When you redeem USDFC, the system identifies Troves starting from the lowest collateral ratio
2. Your USDFC is used to repay the debt of these Troves
3. In return, you receive an equivalent value of FIL collateral (minus the redemption fee)
4. This process continues until your redemption amount is fulfilled or no more Troves can be redeemed from

### Redemption Fee

The redemption fee is variable and depends on the current base rate:

$$
\text{Redemption Fee} = \text{Base Rate} + \text{Redemption Fee Multiplier}
$$

The base rate increases with each redemption and decays over time, which helps prevent large-scale redemptions that could destabilize the system.

\[Image: Graph showing how the base rate changes with redemptions]

### When to Redeem

Redemption is most beneficial in the following scenarios:

1. When USDFC is trading below its $1 peg (arbitrage opportunity)
2. When you want to exit the USDFC system entirely
3. When you believe FIL price will increase and want to acquire it at the current price

\[Image: Decision flowchart for when to consider redemption]

## Next Steps

* Consider [depositing USDFC into the Stability Pool](using-the-stability-pool.md) as an alternative to redemption
* Learn about [managing collateral effectively](managing-collateral-effectively.md) if you have your own Trove
* Explore other ways to use your USDFC in the ecosystem

## Troubleshooting

* **Transaction Failed**: Ensure you have enough FIL for gas fees
* **Cannot Redeem**: There may not be enough Troves available for redemption, or the system might be in Recovery Mode
* **High Redemption Fee**: The base rate might be elevated due to recent redemptions; consider waiting for it to decay

## Common Questions

**Q: Can I redeem any amount of USDFC?**\
A: Yes, but smaller amounts may not be cost-effective due to gas fees and the redemption fee.

**Q: Which Troves are affected by my redemption?**\
A: Redemptions start from the Troves with the lowest collateral ratios and move upward.

**Q: Is there a waiting period for redemption?**\
A: No, redemptions can be processed immediately, but the redemption fee increases with each redemption to prevent large-scale redemptions in a short period.

**Q: Can redemptions be blocked?**\
A: Yes, redemptions are disabled during Recovery Mode to protect the system's stability.

## Related Topics

* [The Trove System](../core-mechanics/the-trove-system.md)
* [Redemption](../core-mechanics/redemption.md)
* [Protocol Fees](../core-mechanics/protocol-fees.md)
* [Recovery Mode](../advanced-topics/recovery-mode.md)
