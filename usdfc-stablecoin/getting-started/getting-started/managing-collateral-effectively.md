---
description: Learn how to manage your collateral to maintain a healthy Trove
---

# 🤝 Managing Collateral Effectively

## Prerequisites

* An active Trove with FIL collateral
* Access to the [USDFC application](https://legacy.usdfc.net/)
* Connected wallet with FIL for additional collateral (if adding)

## Overview

Managing your collateral effectively is crucial for maintaining a healthy Trove and avoiding liquidation. This guide will show you how to add or withdraw collateral, and how to determine the optimal collateral ratio for your risk tolerance.

## Step 1: Access Your Trove

First, you need to access your existing Trove in the USDFC application.

1. Navigate to the [USDFC application](https://legacy.usdfc.net/)
2. Connect your wallet if not already connected
3. Go to the "Trove" section on the USDFC Dashboard page
4. Review your current collateral amount, debt, and collateral ratio

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Trove dashboard showing current position details</p></figcaption></figure>

## Step 2: Select "Adjust Trove"

To manage your collateral, you need to adjust your Trove.

1. Click on the "Adjust" button
2. This will open the Trove adjustment interface

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>"Adjust Trove" interface</p></figcaption></figure>

## Step 3: Add or Withdraw Collateral

Now you can add more collateral or withdraw some of your existing collateral.

### To Add Collateral:

1. In the adjustment interface, locate the "Collateral" input field
2. Increase the amount of FIL from your current value
3. The system will automatically calculate your new collateral ratio
4. Adding collateral increases your collateral ratio and reduces liquidation risk

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Screenshot of the interface for adding collateral</p></figcaption></figure>

### To Withdraw Collateral:

1. In the adjustment interface, locate the "Collateral" input field
2. Decrease the amount of FIL from your current value
3. The system will automatically calculate your new collateral ratio
4. Ensure your new collateral ratio remains above the minimum required (110%)

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Screenshot of the interface for withdrawing collateral</p></figcaption></figure>

## Step 4: Review Transaction Details

Before confirming, review all transaction details carefully.

1. Check the collateral adjustment amount
2. Verify your new collateral ratio
3. Understand how this affects your liquidation risk
4. Review any fees that will be applied

## Step 5: Confirm and Execute

Once you're satisfied with the details, you can proceed with the adjustment.

1. Click the "Confirm" button
2. Confirm the transaction in your wallet
3. Wait for the transaction to be processed on the blockchain

<figure><img src="../../../.gitbook/assets/Screenshot 2025-05-11 at 8.06.11.png" alt=""><figcaption><p>Screenshot of the wallet confirmation screen</p></figcaption></figure>

## Step 6: Verify the Adjustment

After the transaction is confirmed, verify that your collateral was adjusted successfully.

1. Check that your Trove details have been updated with the new collateral amount
2. Verify your new collateral ratio
3. If withdrawing collateral, confirm that the FIL has been added to your wallet balance

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Screenshot showing updated Trove details</p></figcaption></figure>

## Understanding Collateral Ratios

### Key Collateral Ratio Thresholds

| Threshold                      | Value | Description                                                                         |
| ------------------------------ | ----- | ----------------------------------------------------------------------------------- |
| Minimum Collateral Ratio (MCR) | 110%  | The absolute minimum ratio required to avoid liquidation                            |
| Recovery Mode Threshold        | 150%  | When the system enters Recovery Mode if the Total Collateral Ratio falls below this |
| Recommended Safe Ratio         | 200%+ | A conservative ratio that provides a good buffer against price fluctuations         |

### Calculating Your Liquidation Price

To calculate the FIL price at which your Trove would reach the minimum collateral ratio (110%):

$$
\text{Liquidation Price} = \frac{\text{Debt in USDFC} \times 1.1}{\text{Collateral in FIL}}
$$

\[Image: Visual representation of the liquidation price calculation]

## Strategies for Collateral Management

### Conservative Strategy (Low Risk)

* Maintain a collateral ratio of 200% or higher
* Add collateral proactively when FIL price starts to decline
* Smaller USDFC minting relative to collateral value

### Balanced Strategy (Medium Risk)

* Maintain a collateral ratio between 150% and 200%
* Monitor FIL price regularly and adjust as needed
* Balance between capital efficiency and safety

### Aggressive Strategy (High Risk)

* Maintain a collateral ratio between 110% and 150%
* Requires very active monitoring and quick reactions to price changes
* Maximizes capital efficiency but has higher liquidation risk

\[Image: Visual comparison of different collateral management strategies]

## Next Steps

* [Monitor your position](monitoring-your-position.md) regularly to stay informed about your Trove's health
* Consider [depositing USDFC into the Stability Pool](using-the-stability-pool.md) to earn rewards
* Learn about [Recovery Mode](../../advanced-topics/recovery-mode.md) and how it affects your Trove

## Troubleshooting

* **Cannot Withdraw Collateral**: Your withdrawal might push your collateral ratio below the minimum requirement
* **Transaction Failed**: Ensure you have enough FIL for gas fees
* **Collateral Not Showing**: Refresh the page or check your transaction history

## Common Questions

**Q: How often should I adjust my collateral?**\
A: This depends on your risk tolerance and FIL price volatility. More volatile markets require more frequent adjustments.

**Q: What happens if FIL price drops suddenly?**\
A: If the price drop causes your collateral ratio to fall below the minimum requirement (110%), your Trove may be liquidated.

**Q: Can I add collateral without minting more USDFC?**\
A: Yes, you can add collateral without changing your debt amount to increase your collateral ratio.

**Q: Is there a fee for adjusting my collateral?**\
A: Adding collateral only incurs gas fees. Withdrawing collateral may incur both gas fees and a small protocol fee.

## Related Topics

* [The Trove System](../../core-mechanics/the-trove-system.md)
* [Liquidation](../../core-mechanics/liquidation.md)
* [Collateral Ratio](../broken-reference/)
* [Recovery Mode](../../advanced-topics/recovery-mode.md)
