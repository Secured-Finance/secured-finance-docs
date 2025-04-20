---
description: Understanding how price range limits are calculated and applied in the Circuit Breaker mechanism
icon: 🛑
---

# 🛑 Price Range Limits

## Overview

Our trading platform incorporates a circuit breaker mechanism to regulate price fluctuations within a single block. This feature is applicable to both 'market orders' and 'limit orders,' and operates to ensure that orders are executed within acceptable price ranges. The primary objective of the circuit breaker is to mitigate extreme volatility and maintain equilibrium in our Zero Coupon bond market.

## What You'll Learn

- How the Circuit Breaker mechanism calculates price range limits
- Why different limits are applied to upward vs. downward price movements
- How Moving Averages of reliable block prices are used to determine limits
- How to calculate price range limits using practical examples
- How minimum price fluctuation rules are applied in exceptional cases

## How It Works

The Circuit Breaker mechanism uses a combination of historical price data and percentage-based limits to determine the acceptable range for price movements within a single block.

### Price Range Limit Calculation

* **Limitation on Downward Price Movement:**
  The platform restricts the downward price movement to 5% from the Moving Average of the most recent 5 Reliable Block Prices.

* **Limitation on Upward Price Movement:**
  Conversely, upward price movement is capped at 10% from the Moving Average of the last 3 Reliable Block Prices.

* **Minimum Price Fluctuation:**
  The market is permitted to move a minimum of 2.00 for downside and 7.00 for topside.

{% hint style="info" %}
Due to the inherent characteristics of Zero-Coupon Bonds—which begin trading at a significant discount and mature at par (100 on our platform)—there are tighter restrictions on downward movements to prevent excessive volatility.
{% endhint %}

### Practical Example

Consider a situation where the last 5 reliable Block Prices are 80.60, 80.40, 80.30, 80.10, and the most recent is 79.60.

#### Downward Price Limit:

Moving Average of the most recent 5 reliable block prices is:

$$
(80.60+80.40+80.30+80.10+79.60)/5 = 80.20
$$

Since movement is limited to 5% to downside, the lowest bound will be:

$$
80.20 * 0.95 = 76.19
$$

No orders lower than 76.19 will be executed during the next block.

#### Upward Price Limit:

Moving Average of the most recent 3 reliable block prices is:

$$
(80.30+80.10+79.60)/3 = 80.00
$$

As topside can move up to 10%, the upper limit will be:

$$
80.00 * 1.10 = 88.00
$$

### Exceptional Case: Minimum Movement

For instance, if the last 5 reliable block prices were 20.00, 18.00, 16.00, 14.00, and 12.00, the Moving Average would be 16.00. Normally, the downward movement would be limited to 15.20 which is 95% of the 16.00. However, the platform allows for a minimum market movement of 2.00, setting the lower limit at 14.00 (= 16.00 - 2.00).

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Downward Movement Limit | Maximum percentage decrease from Moving Average | 5% |
| Upward Movement Limit | Maximum percentage increase from Moving Average | 10% |
| Downward Moving Average Period | Number of blocks used for downward limit calculation | 5 blocks |
| Upward Moving Average Period | Number of blocks used for upward limit calculation | 3 blocks |
| Minimum Downward Movement | Minimum allowed price decrease regardless of percentage | 2.00 |
| Minimum Upward Movement | Minimum allowed price increase regardless of percentage | 7.00 |

## Related Resources

- [Circuit Breaker](README.md)
- [Safety Measures](../../README.md)
- [Order Status & Transition](../../../../core-mechanics/order-book-system/order-life-cycle/case-study-order-status-and-transition.md)
- [Mark to Market](../../../../core-mechanics/liquidation/mark-to-market.md)

