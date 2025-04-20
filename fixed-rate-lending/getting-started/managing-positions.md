---
description: A step-by-step guide to managing your positions on the Fixed-Rate Lending Protocol
icon: 📊
---

# 📊 Managing Positions

## Prerequisites

- Active lending or borrowing positions on the Secured Finance platform
- A connected wallet
- Basic understanding of fixed-rate lending concepts

## Overview

Managing your positions effectively is crucial for maximizing returns and minimizing risks in the Fixed-Rate Lending Protocol. This guide will walk you through the various ways to monitor, adjust, and close your positions, helping you navigate the platform with confidence.

## Step 1: View Your Active Positions

1. Navigate to the [Secured Finance platform](https://app.secured.finance/)
2. Connect your wallet if not already connected
3. Go to the "Portfolio" tab to see all your active positions
4. Review your positions, including:
   - Asset type
   - Position size
   - Maturity date
   - Current value
   - Profit/loss

![Portfolio View](../../.gitbook/assets/portfolio-view.png)

## Step 2: Monitor Collateralization Ratio (For Borrowers)

If you have borrowed assets, it's essential to monitor your collateralization ratio:

1. In the Portfolio tab, locate your borrowing positions
2. Check the current collateralization ratio for each position
3. Ensure it stays above the minimum required ratio to avoid liquidation
4. Set up notifications (if available) to alert you when your ratio approaches the minimum threshold

## Step 3: Adding to Existing Positions

To increase an existing position:

1. Navigate to the Trading tab
2. Select the same asset and maturity as your existing position
3. Choose the same position type (Lend or Borrow)
4. Place a new order with the additional amount
5. Confirm the transaction in your wallet

![Add to Position](../../.gitbook/assets/add-position.png)

## Step 4: Reducing Positions

To partially close a position before maturity:

1. Go to the Portfolio tab
2. Find the position you want to reduce
3. Click the "Unwind" button
4. Select "Partial" unwind option
5. Enter the amount you want to reduce
6. Review the details and confirm the transaction

![Reduce Position](../../.gitbook/assets/reduce-position.png)

## Step 5: Unwinding Positions (Early Exit)

To completely close a position before maturity:

1. Go to the Portfolio tab
2. Find the position you want to close
3. Click the "Unwind" button
4. Select "Full" unwind option
5. Review the details, including any fees or slippage
6. Confirm the transaction in your wallet

{% hint style="info" %}
Unwinding positions before maturity may result in different returns than holding until maturity, depending on current market rates.
{% endhint %}

## Step 6: Auto-Rolling Positions

To set up automatic reinvestment at maturity:

1. Go to the Portfolio tab
2. Find the position you want to auto-roll
3. Click the "Auto-Roll" button
4. Select your preferred settings:
   - Target maturity date for the new position
   - Price parameters (market rate or custom rate)
5. Review and confirm the auto-roll settings

![Auto-Roll Settings](../../.gitbook/assets/auto-roll.png)

## Step 7: Claiming Matured Positions

When a position reaches maturity:

1. Go to the Portfolio tab
2. Locate your matured positions (they will be marked as "Matured")
3. Click the "Claim" button
4. Review the amount to be claimed
5. Confirm the transaction in your wallet
6. The funds will be transferred to your wallet or collateral vault, depending on your settings

## Next Steps

After mastering position management, you might want to:

- [Explore advanced trading strategies](../advanced-topics/market-dynamics/README.md)
- [Learn about liquidation mechanics](../core-mechanics/liquidation/README.md) to better manage risk
- [Understand Zero-Coupon Bond tokenization](../core-mechanics/tokenization.md) for additional opportunities

## Troubleshooting

### Unwind Order Not Executing

If your unwind order isn't being executed:
- There might be insufficient liquidity in the orderbook
- Your unwind price might not be competitive with current market rates
- Try using a market unwind instead of a limit unwind for immediate execution

### Position Not Showing Updated Values

If your position values aren't updating:
- Refresh the page to get the latest data
- Check that your wallet is still connected
- Verify that the blockchain network is functioning normally
- Contact support if the issue persists

### Auto-Roll Not Working

If your auto-roll settings aren't being applied:
- Ensure you have sufficient collateral for the new position
- Check that you've approved the necessary token permissions
- Verify that the target maturity date is available for trading
- Review the auto-roll settings to ensure they're correctly configured
