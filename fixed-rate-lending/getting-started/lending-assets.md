---
description: A step-by-step guide to lending assets on the Fixed-Rate Lending Protocol
icon: 💰
---

# 💰 Lending Assets

## Prerequisites

- A connected wallet with sufficient assets to lend
- Basic understanding of fixed-rate lending concepts
- Access to the Secured Finance platform

## Overview

Lending assets on Secured Finance's Fixed-Rate Lending Protocol allows you to earn predictable yields on your digital assets. By lending through the protocol's orderbook system, you can lock in fixed rates for specific time periods, providing certainty about your returns regardless of market volatility.

## Step 1: Connect Your Wallet

1. Navigate to the [Secured Finance platform](https://app.secured.finance/)
2. Click the "Connect Wallet" button in the top right corner
3. Select your wallet provider (MetaMask, WalletConnect, etc.)
4. Approve the connection request in your wallet

![Connect Wallet](../../.gitbook/assets/connect-wallet.png)

## Step 2: Deposit Assets

Before lending, you need to deposit the assets you want to lend into the protocol.

1. Go to the "Portfolio" tab
2. Click the "Deposit" button
3. Select the asset you want to deposit for lending
4. Enter the amount and confirm the transaction
5. Wait for the transaction to be confirmed on the blockchain

![Deposit Assets](../../.gitbook/assets/Deposit-x1.7mp4-ezgif.com-video-to-gif-converter.gif)

## Step 3: Navigate to the Trading Interface

1. Click on the "Trading" tab in the main navigation
2. Select the asset you want to lend from the dropdown menu
3. Choose the maturity date that suits your investment timeframe

![Trading Interface](../../.gitbook/assets/trading-interface.png)

## Step 4: Place a Lending Order

1. Select "Lend" in the order type section
2. Choose between "Market Order" (immediate execution at current market price) or "Limit Order" (execution at your specified price)
3. For a Limit Order:
   - Set your desired interest rate (APR)
   - Enter the amount you want to lend
4. For a Market Order:
   - Enter the amount you want to lend
   - Review the current market rate
5. Click "Place Order" to submit your lending request

![Place Lending Order](../../.gitbook/assets/LPonOrderbookx1.5-ezgif.com-video-to-gif-converter.gif)

## Step 5: Confirm Your Transaction

1. Review the order details in the confirmation modal
2. Check the estimated gas fees
3. Click "Confirm" to proceed
4. Approve the transaction in your wallet
5. Wait for the transaction to be confirmed on the blockchain

## Step 6: Monitor Your Position

After successfully lending assets:

1. Go to the "Portfolio" tab to view your active lending positions
2. You'll receive Zero-Coupon Bonds (ZC Bonds) representing your lending position
3. These ZC Bonds will mature to their full face value at the maturity date
4. You can track the current value of your lending position in the Portfolio section

![Monitor Position](../../.gitbook/assets/monitor-position.png)

## Step 7: Managing Your Lending Position

You have several options for managing your lending position:

1. **Hold Until Maturity**: Receive the full face value of your ZC Bonds at maturity
2. **Unwind Position**: Exit your position early by selling your ZC Bonds on the orderbook
3. **Auto-Rolling**: Set up automatic reinvestment at maturity to maintain your lending position

## Next Steps

Now that you've successfully lent assets, you might want to:

- [Learn how to manage your positions](managing-positions.md)
- [Explore auto-rolling features](../advanced-topics/market-dynamics/auto-rolling/README.md) to automatically reinvest at maturity
- [Understand how Zero-Coupon Bonds work](../core-mechanics/standardization/zero-coupon-bonds.md) as representations of your lending position

## Troubleshooting

### Order Not Executing

If your limit order isn't being executed:
- Your specified interest rate may not be competitive with current market rates
- There might be insufficient borrowing demand at your specified rate
- Try adjusting your rate or switching to a market order for immediate execution

### Transaction Failing

If your transaction is failing:
- Ensure you have enough native tokens (ETH, MATIC, etc.) to cover gas fees
- Check that you have sufficient balance of the asset you're trying to lend
- Try refreshing the page and attempting the transaction again

### ZC Bonds Not Appearing

If your ZC Bonds don't appear in your portfolio after lending:
- The transaction may still be pending; check your wallet for transaction status
- There might be a delay in the UI updating; try refreshing the page
- Verify the transaction was successful on the blockchain explorer
