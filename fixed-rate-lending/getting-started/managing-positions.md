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

## Step 6: Understanding Auto-Rolling

Auto-Rolling is a protocol-wide feature that automatically transitions positions to the next maturity period:

1. All positions are subject to Auto-Rolling when they reach maturity
2. The protocol automatically handles the transition to the next maturity period
3. There is no need to manually select or configure Auto-Roll settings
4. Be aware that Auto-Rolling will maintain your exposure to the market

{% hint style="info" %}
Auto-Rolling is a protocol feature that applies to all positions. You cannot opt out of Auto-Rolling directly, but you can unwind your position before maturity if you wish to exit.
{% endhint %}

## Step 7: Exiting Positions at Maturity

To exit your position when it reaches maturity:

1. You must manually unwind your position before or after maturity
2. Go to the Active Positions tab
3. Find the position you want to exit
4. Click the "Close" button
5. Review the details, including any fees or slippage
6. Confirm the transaction in your wallet

{% hint style="warning" %}
There is no automatic claim system. You must manually unwind your position to exit, which means there is liquidity risk if there are insufficient counterparties in the market.
{% endhint %}

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
