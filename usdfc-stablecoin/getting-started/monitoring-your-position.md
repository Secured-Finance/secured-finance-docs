---
description: Learn how to track and manage your Trove's health
---

# 🏦 Monitoring Your Position

## Prerequisites

* An active Trove with FIL collateral
* Access to the [USDFC application](https://app.usdfc.net)
* Basic understanding of collateral ratios and liquidation risk

## Overview

Monitoring your position is essential for maintaining a healthy Trove and avoiding liquidation. This guide will show you how to track your Trove's health, understand key metrics, and set up alerts to stay informed about changes that could affect your position.

## Step 1: Access Your Trove Dashboard

The Trove dashboard is your primary tool for monitoring your position.

1. Navigate to the [USDFC application](https://app.usdfc.net)
2. Connect your wallet if not already connected
3. Go to the "Trove" section on the USDFC Dashboard page
4. Review your current Trove details

\[Image: Screenshot of the Trove dashboard showing key metrics]

## Step 2: Understand Key Metrics

To effectively monitor your position, you need to understand the key metrics displayed on your dashboard.

### Collateral Ratio

The collateral ratio is the most important metric to monitor. It represents the value of your collateral relative to your debt.

$$
\text{Collateral Ratio} = \frac{\text{Collateral Value in USD}}{\text{Debt in USDFC}} \times 100\%
$$

* **Safe Zone**: Above 200% (Conservative)
* **Caution Zone**: 150% to 200% (Moderate risk)
* **Danger Zone**: 110% to 150% (High risk)
* **Liquidation Zone**: Below 110% (Immediate risk)

\[Image: Visual representation of collateral ratio zones]

### Liquidation Price

The liquidation price is the FIL price at which your Trove would reach the minimum collateral ratio (110%) and become eligible for liquidation.

$$
\text{Liquidation Price} = \frac{\text{Debt in USDFC} \times 1.1}{\text{Collateral in FIL}}
$$

\[Image: Visualization of liquidation price calculation]

### Current FIL Price

The current price of FIL relative to USD is displayed to help you understand how close you are to your liquidation price.

### Available Actions

Based on your current metrics, the dashboard may suggest available actions to improve your position's health.

\[Image: Screenshot showing suggested actions based on Trove health]

## Step 3: Set Up External Alerts

While the USDFC application doesn't currently offer built-in alerts, you can set up external alerts to monitor your position.

### Price Alerts

Set up price alerts for FIL using cryptocurrency tracking apps or exchanges.

1. Calculate your liquidation price
2. Set an alert for when FIL price approaches this threshold (e.g., 20% above liquidation price)
3. Popular platforms for price alerts include CoinGecko, CoinMarketCap, or exchange apps

\[Image: Screenshot of setting up a price alert on a crypto tracking platform]

### Blockchain Monitoring Tools

Use blockchain monitoring tools to track your Trove's health.

1. Find your Trove's address or ID
2. Set up monitoring using tools like Etherscan, Tenderly, or DeFi-specific monitoring platforms
3. Configure alerts for significant changes to your Trove

\[Image: Screenshot of blockchain monitoring tool setup]

## Step 4: Regular Check-ins

Establish a routine for checking your Trove's health.

### Daily Checks (High-Risk Positions)

If your collateral ratio is close to the minimum (110%-150%):

* Check your position at least once daily
* Monitor FIL price movements throughout the day
* Be prepared to add collateral quickly if needed

### Weekly Checks (Moderate-Risk Positions)

If your collateral ratio is in a safer range (150%-200%):

* Check your position at least once weekly
* Review FIL price trends for the week
* Adjust collateral as needed based on market outlook

### Monthly Checks (Low-Risk Positions)

If your collateral ratio is very high (>200%):

* Check your position at least once monthly
* Evaluate if you're being too conservative with your capital
* Consider strategies to optimize your position

\[Image: Calendar or schedule visualization for position monitoring]

## Step 5: Respond to Market Changes

Develop a plan for responding to different market scenarios.

### During FIL Price Decreases

1. Calculate how much the price can drop before reaching your comfort threshold
2. Prepare additional FIL for collateral if needed
3. Consider reducing your debt by repaying some USDFC

### During FIL Price Increases

1. Evaluate if you want to withdraw some collateral
2. Consider minting additional USDFC
3. Rebalance your position to maintain your target collateral ratio

\[Image: Flowchart showing decision paths for different market scenarios]

## Next Steps

* Learn how to [manage your collateral effectively](managing-collateral-effectively.md)
* Consider [depositing USDFC into the Stability Pool](using-the-stability-pool.md) to earn rewards
* Understand [Recovery Mode](../advanced-topics/recovery-mode.md) and how it affects your Trove

## Troubleshooting

* **Dashboard Not Loading**: Try refreshing the page or reconnecting your wallet
* **Metrics Not Updating**: Check if there are pending transactions or network congestion
* **Unexpected Collateral Ratio**: Verify the current FIL price from multiple sources

## Common Questions

**Q: How often does the dashboard update?**\
A: The dashboard updates in real-time based on blockchain data and current price feeds.

**Q: Will I receive notifications if my Trove is at risk?**\
A: The USDFC application doesn't currently send automatic notifications. You should set up external alerts as described above.

**Q: What should I do if I can't access the application but know my position is at risk?**\
A: You can interact with the USDFC protocol directly through the smart contracts if necessary. Keep emergency funds ready to add collateral when needed.

**Q: How can I tell if the system is in Recovery Mode?**\
A: The dashboard will display a prominent notification when the system enters Recovery Mode.

## Related Topics

* [The Trove System](../core-mechanics/the-trove-system.md)
* [Liquidation](../core-mechanics/liquidation/)
* [Collateral Ratio](../core-mechanics/liquidation/collateral-ratio.md)
* [Recovery Mode](../advanced-topics/recovery-mode.md)
