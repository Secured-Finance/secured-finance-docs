---
description: A guide to trading zero-coupon bonds on the Fixed-Rate Lending Protocol
icon: 💰
---

# 💰 Trading

## Prerequisites

- A connected wallet with sufficient assets
- Basic understanding of fixed-rate lending concepts
- Assets deposited as collateral (for borrowing)

## Overview

Welcome to the [**Trading tab**](https://app.secured.finance/) on Secured Finance, your gateway to fixed-income trading. This interface enables you to engage in peer-to-contract lending and trading of zero-coupon (ZC) bonds with simplicity, efficiency, and transparency.

## Step 1: Accessing the Trading Interface

1. Navigate to the [Secured Finance platform](https://app.secured.finance/)
2. Connect your wallet if not already connected
3. Click on the "Trading" tab in the main navigation
4. Select the asset pair and maturity date you want to trade

![Trading Interface](../../../../.gitbook/assets/trading-interface.png)

## Step 2: Understanding Zero-Coupon Bond Trading

Before placing orders, it's important to understand the basics:

1. **Buying ZC Bonds (Lending)**
   - When you buy a bond, you're effectively lending assets
   - Your initial investment accrues interest over time
   - At maturity, you receive the full face value of the bond

2. **Selling ZC Bonds (Borrowing)**
   - When you sell a bond, you're borrowing assets
   - You receive funds upfront and repay the face value at maturity
   - Requires sufficient collateral to secure the loan

3. **Orderbook System**
   - All transactions occur on our Orderbook
   - Orders are matched directly with counterparties via smart contracts
   - Provides transparent price discovery and efficient execution

## Step 3: Placing a Buy Order (Lending)

1. Select "Buy" in the order form
2. Choose between "Market Order" or "Limit Order"
   - Market Order: Executes immediately at the best available price
   - Limit Order: Executes only at your specified price or better
3. Enter the amount you want to lend
4. For Limit Orders, specify your desired price (interest rate)
5. Review the order details, including:
   - Total cost
   - Expected yield
   - Maturity date
6. Click "Place Order" to submit
7. Confirm the transaction in your wallet

## Step 4: Placing a Sell Order (Borrowing)

1. Select "Sell" in the order form
2. Choose between "Market Order" or "Limit Order"
3. Enter the amount you want to borrow
4. For Limit Orders, specify your desired price (interest rate)
5. Ensure you have sufficient collateral
6. Review the order details, including:
   - Amount received
   - Repayment amount at maturity
   - Collateral requirements
7. Click "Place Order" to submit
8. Confirm the transaction in your wallet

## Step 5: Managing Open Orders

1. Navigate to the "Open Orders" section below the orderbook
2. View all your pending orders
3. To cancel an order:
   - Find the order you want to cancel
   - Click the "Cancel" button
   - Confirm the cancellation in your wallet

## Step 6: Unwinding a Position

If you need to exit a position before maturity:

1. Go to the "Portfolio" tab
2. Find the position you want to unwind
3. Click the "Unwind" button
4. Choose between Market Unwind or Limit Unwind
5. Enter the amount you want to unwind
6. Review the details and confirm the transaction

## Step 7: Understanding Auto-Rolling

When your loan matures:

1. Funds are automatically reinvested into the next 3-month maturity cycle via our Auto-Roll feature
2. This minimizes reinvestment risks and promotes steady growth
3. You can customize Auto-Roll settings in your Portfolio
4. For more details, see our [Auto-Rolling](../../../advanced-topics/market-dynamics/auto-rolling/) section

## Next Steps

After learning the basics of trading, you might want to:

- [Explore advanced trading strategies](../../../advanced-topics/market-dynamics/README.md)
- [Learn about collateral management](../portfolio/collateral-management.md)
- [Understand security measures](../../../advanced-topics/safety-measures/) that protect your investments

## Troubleshooting

### Order Not Executing

If your limit order isn't being executed:
- Your specified price may not be competitive with current market rates
- There might be insufficient liquidity at your price level
- Try adjusting your price or using a market order for immediate execution

### Insufficient Collateral Error

If you receive an insufficient collateral error when borrowing:
- Check your collateral balance in the Portfolio tab
- Deposit additional collateral if needed
- Reduce the amount you're trying to borrow
- Consider using assets with higher collateral factors

### Transaction Failing

If your transaction is failing:
- Ensure you have enough native tokens (ETH, MATIC, etc.) for gas fees
- Check that you've approved the necessary token permissions
- Try refreshing the page and attempting the transaction again
- If issues persist, check the blockchain explorer for specific error details

## Security Measures

Secured Finance prioritizes loan security with:

1. **Robust Collateral Management**
   - Borrowers must pledge collateral
   - Collateral is managed by smart contracts to reduce counterparty risk
   - Automatic liquidation processes protect lenders

2. **Smart Contract Technology**
   - Enforces loan terms automatically
   - Enhances security and reliability
   - Undergoes regular audits and security reviews

For more details, see our [Collateral](../portfolio/collateral-management.md) and [Security & Safety Measures](../../../advanced-topics/safety-measures/) sections.
