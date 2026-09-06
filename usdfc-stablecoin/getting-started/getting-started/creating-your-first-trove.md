---
description: Learn how to create your first Trove to start using USDFC
---

# ⛽ Creating Your First Trove

## Prerequisites

* A wallet with FIL tokens (Filecoin's native cryptocurrency)
* Basic understanding of blockchain transactions
* Access to the [USDFC application](https://legacy.usdfc.net/)

## Overview

A Trove is your personal collateralized debt position in the USDFC protocol. By creating a Trove, you can deposit FIL as collateral and mint USDFC stablecoins against it. This guide will walk you through the process of creating your first Trove.

## Step 1: Connect Your Wallet

Before you can create a Trove, you need to connect your wallet to the USDFC application.

1. Navigate to the [USDFC application](https://legacy.usdfc.net/)
2. Click on the "Connect Wallet" button in the top right corner
3. Select your wallet provider (MetaMask, WalletConnect, etc.)
4. Confirm the connection

<figure><img src="../../../.gitbook/assets/image (124).png" alt="The wallet connection interface after the 'Connect Wallet' button"><figcaption><p>The wallet connection interface after the "Connect Wallet" button</p></figcaption></figure>

## Step 2: Navigate to the Trove Management Section

Once your wallet is connected, you need to navigate to the Trove management section.

1. On the USDFC dashboard, locate and click on the "Open Trove" button
2. You'll see the Trove creation section on the same page

<figure><img src="../../../.gitbook/assets/image (126).png" alt="The USDFC dashboard with the Trove/Mint USDFC section"><figcaption><p>The USDFC dashboard with the Trove/Mint USDFC section</p></figcaption></figure>

## Step 3: Set Your Collateral and Debt Amounts

Now you need to decide how much FIL to deposit and how much USDFC to mint.

1. Enter the amount of FIL you want to deposit as collateral
2. Enter the amount of USDFC you want to mint & borrow
3. The system will automatically calculate your collateral ratio
4. Ensure your collateral ratio is above the minimum required (typically 110%)

<figure><img src="../../../.gitbook/assets/image (129).png" alt="The collateral and debt input fields with the collateral ratio calculation"><figcaption><p>The collateral and debt input fields with the collateral ratio calculation</p></figcaption></figure>

## Step 4: Review Transaction Details

Before confirming, review all transaction details carefully.

1. Check the collateral amount (FIL)
2. Verify the debt amount (USDFC)
3. Review the collateral ratio
4. Note any fees that will be applied (including the Liquidation Reserve of 20 USDFC)

## Step 5: Confirm and Create Your Trove

Once you're satisfied with the details, you can create your Trove.

1. Click the "Confirm" button
2. Confirm the transaction in your wallet
3. Wait for the transaction to be processed on the blockchain

<figure><img src="../../../.gitbook/assets/image (130).png" alt="The confirmation screen with the 'Confirm' button highlighted"><figcaption><p>The confirmation screen with the "Confirm" button highlighted</p></figcaption></figure>

## Step 6: Verify Your Trove Creation

After the transaction is confirmed, verify that your Trove was created successfully.

1. Check that your Trove appears in the dashboard
2. Verify that the USDFC has been added to your wallet balance
3. If you don't see USDFC in your wallet, you may need to add it as a custom token (see a [wallet icon](https://gyazo.com/4102e760883c7c413ee1161a851d5712) in the Protocol Statistics section)

<figure><img src="../../../.gitbook/assets/Screenshot 2025-05-11 at 5.58.15.png" alt="Screenshot showing a successfully created Trove in the dashboard"><figcaption><p>Screenshot showing a successfully created Trove in the dashboard</p></figcaption></figure>

## Next Steps

Now that you've created your first Trove, you can:

* [Mint additional USDFC](minting-usdfc-step-by-step.md)
* [Manage your collateral](managing-collateral-effectively.md)
* [Monitor your position](monitoring-your-position.md)
* [Deposit USDFC into the Stability Pool](using-the-stability-pool.md)

## Troubleshooting

* **Transaction Failed**: Ensure you have enough FIL for gas fees and that your collateral ratio meets the minimum requirement
* **USDFC Not Showing in Wallet**: Add USDFC as a custom token in your wallet using the contract address found in the [deployed contracts](../../deployed-contracts.md) page, or click the wallet icon near the USDFC contract info on the USDFC app
* **High Gas Fees**: Try again when network congestion is lower or adjust your gas settings

## Common Questions

**Q: What is the minimum amount of FIL I can deposit?**\
A: You need to deposit enough FIL to borrow at least 200 USDFC (the minimum borrowing amount) while maintaining at least a 110% collateral ratio. The exact FIL amount will depend on the current FIL price.

**Q: What is the Liquidation Reserve?**\
A: The Liquidation Reserve is a small amount of USDFC (20 USDFC) that is set aside to cover potential gas costs in case your Trove needs to be liquidated.

**Q: Can I create multiple Troves?**\
A: No, each wallet address can only have one Trove at a time.

**Q: What happens if my collateral ratio falls below the minimum?**\
A: Your Trove may be liquidated. Learn more in the [Liquidation](../../core-mechanics/liquidation.md) section.

## Related Topics

* [The Trove System](../../core-mechanics/the-trove-system.md)
* [Mint & Borrow](../../core-mechanics/mint-and-borrow.md)
* [Liquidation](../../core-mechanics/liquidation.md)
* [Recovery Mode](../../core-mechanics/recovery-mode.md)
