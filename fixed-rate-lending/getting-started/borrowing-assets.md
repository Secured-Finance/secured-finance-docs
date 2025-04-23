---
description: A step-by-step guide to borrowing assets on the Fixed-Rate Lending Protocol
---

# 🏦 Borrowing Assets

## Prerequisites

* A connected wallet with sufficient collateral deposited
* Basic understanding of fixed-rate lending concepts
* Access to the Secured Finance platform

## Overview

Borrowing assets on Secured Finance's Fixed-Rate Lending Protocol allows you to access liquidity while maintaining exposure to your collateral assets. The protocol uses an orderbook system to match borrowers with lenders at fixed rates, providing certainty about your borrowing costs for the entire term.

## Step 1: Connect Your Wallet

1. Navigate to the [Secured Finance platform](https://app.secured.finance/)
2. Click the "Connect Wallet" button in the top right corner
3. Select your wallet provider (MetaMask, WalletConnect, etc.)
4. Approve the connection request in your wallet

![Connect Wallet](../../.gitbook/assets/connect-wallet.png)

## Step 2: Deposit Collateral

Before borrowing, you need to deposit collateral to secure your loan.

1. Go to the "Portfolio" tab
2. Click the "Deposit" button
3. Select the asset you want to deposit as collateral
4. Enter the amount and confirm the transaction
5. Wait for the transaction to be confirmed on the blockchain

![Deposit Collateral](../../.gitbook/assets/Deposit-x1.7mp4-ezgif.com-video-to-gif-converter.gif)

## Step 3: Navigate to the Trading Interface

1. Click on the "Trading" tab in the main navigation
2. Select the asset you want to borrow from the dropdown menu
3. Choose the maturity date that suits your needs

![Trading Interface](../../.gitbook/assets/trading-interface.png)

## Step 4: Place a Borrow Order

1. Select "Borrow" in the order type section
2. Choose between "Market Order" (immediate execution at current market price) or "Limit Order" (execution at your specified price)
3. For a Limit Order:
   * Set your desired interest rate (APR)
   * Enter the amount you want to borrow
4. For a Market Order:
   * Enter the amount you want to borrow
   * Review the current market rate
5. Click "Place Order" to submit your borrow request

![Place Borrow Order](../../.gitbook/assets/place-order.png)

## Step 5: Confirm Your Transaction

1. Review the order details in the confirmation modal
2. Check the estimated gas fees
3. Click "Confirm" to proceed
4. Approve the transaction in your wallet
5. Wait for the transaction to be confirmed on the blockchain

## Step 6: Monitor Your Position

After successfully borrowing assets:

1. Go to the "Portfolio" tab to view your active positions
2. Monitor your collateralization ratio to ensure it stays above the minimum requirement
3. Keep track of the maturity date to plan for repayment

![Monitor Position](../../.gitbook/assets/monitor-position.png)

## Next Steps

Now that you've successfully borrowed assets, you might want to:

* [Learn how to manage your positions](managing-positions.md)
* [Explore auto-rolling features](../advanced-topics/market-dynamics/auto-rolling/) to extend your loan term
* [Understand liquidation risks](../core-mechanics/liquidation/) to protect your collateral

## Troubleshooting

### Order Not Executing

If your limit order isn't being executed:

* Your specified interest rate may not be competitive with current market rates
* There might be insufficient liquidity in the orderbook
* Try adjusting your rate or switching to a market order for immediate execution

### Insufficient Collateral Error

If you receive an "Insufficient Collateral" error:

* Your collateral value may be too low for the amount you're trying to borrow
* Deposit additional collateral or reduce your borrow amount
* Check the current collateralization requirements for your selected asset

### Transaction Failing

If your transaction is failing:

* Ensure you have enough native tokens (ETH, MATIC, etc.) to cover gas fees
* Check that you're not exceeding your borrowing capacity
* Try refreshing the page and attempting the transaction again
