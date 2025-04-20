---
description: Understanding how prices are determined for the Auto-Rolling mechanism
icon: 💰
---

# 💰 Price Discovery for Auto-Rolling

## Overview

The auto-rolling price discovery mechanism is a critical component of Secured Finance's platform. It ensures that the pricing for the quarterly roll is calculated accurately and fairly, preventing potential price manipulation. This mechanism is designed to adapt to varying market conditions, ranging from normal and liquid conditions to less liquid or extreme situations with no liquidity.

## What You'll Learn

- How the Auto-Rolling price discovery mechanism works
- How prices are determined in different market conditions
- Why different price discovery methods are used based on liquidity
- How the platform prevents price manipulation during Auto-Rolling
- How the initial roll price is determined when no transaction history exists

## How It Works

The price discovery mechanism operates in different ways depending on the market conditions, ensuring fair and accurate pricing in all scenarios.

### Normal and Liquid Condition

In a normal and liquid market condition, we observe the transactions that occur within the 6-hour window before maturity. The roll price is calculated based on the volume-weighted average price of these transactions. This method ensures that the roll price accurately reflects the market conditions and transaction volumes during this period.

### Less Liquid Condition

In a less liquid market condition, where no transactions occur during the 6-hour window before maturity, we set the roll price based on the 'Mark Price'. This price is adjusted for duration to ensure that it accurately reflects the time value of the financial instrument.

### Extreme Condition

In an extreme market condition, where no transactions have occurred for the last 3 months, we use the price of the previous roll. This method ensures that the roll price is still determined based on market data, even in situations of extremely low liquidity.

### Special Case (Only for the Initial Roll)

In the special case of the initial roll, if no transaction occurs on the 2nd order book until the first roll, we use the opening price of our product launch, adjusted for duration. This method ensures that the initial roll price is still based on market data, even if no transactions have occurred.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Observation Window | Time period before maturity used for price calculation in liquid conditions | 6 hours |
| Price Calculation Method (Liquid) | Method used to calculate price in liquid conditions | Volume-weighted average price |
| Price Calculation Method (Less Liquid) | Method used when no transactions occur in observation window | Mark Price adjusted for duration |
| Price Calculation Method (Extreme) | Method used when no transactions occur for extended period | Previous roll price |
| Initial Roll Price | Method used for the first roll with no transaction history | Opening price adjusted for duration |

## Related Resources

- [Auto-Rolling](README.md)
- [Market Dynamics](../../README.md)
- [Mark to Market](../../../../core-mechanics/liquidation/mark-to-market.md)
- [Orderbook Rotation](../../../orderbook-deep-dive/orderbook-rotation.md)
