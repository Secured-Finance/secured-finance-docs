---
description: Understanding how price range limits are calculated and applied in the Circuit Breaker mechanism
icon: 🛑
---

# 🛑 Price Range Limits

## Overview

Our trading platform incorporates a circuit breaker mechanism to regulate price fluctuations within a single block. This feature is applicable to both 'market orders' and 'limit orders,' and operates to ensure that orders are executed within acceptable price ranges. The primary objective of the circuit breaker is to mitigate extreme volatility and maintain equilibrium in our Zero Coupon bond market.



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

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Downward Movement Limit | Maximum percentage decrease from Moving Average | 5% |
| Upward Movement Limit | Maximum percentage increase from Moving Average | 10% |
| Downward Moving Average Period | Number of blocks used for downward limit calculation | 5 blocks |
| Upward Moving Average Period | Number of blocks used for upward limit calculation | 3 blocks |
| Minimum Downward Movement | Minimum allowed price decrease regardless of percentage | 2.00 |
| Minimum Upward Movement | Minimum allowed price increase regardless of percentage | 7.00 |

## Examples

### Example 1: Standard Price Range Calculation

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

This means that in the next block, orders will only be executed if their prices fall within the range of 76.19 to 88.00, protecting the market from extreme volatility.

### Example 2: Minimum Movement Rule Application

If the last 5 reliable block prices were 20.00, 18.00, 16.00, 14.00, and 12.00, the Moving Average would be 16.00. 

Normally, the downward movement would be limited to:

$$
16.00 * 0.95 = 15.20
$$

However, since the platform allows for a minimum market movement of 2.00, the actual lower limit would be:

$$
16.00 - 2.00 = 14.00
$$

This minimum movement rule ensures that markets with low prices can still function efficiently, as percentage-based limits might be too restrictive in such cases.

### Example 3: Asymmetric Limits in Action

Consider a market with the following recent prices:
- Last 5 prices: 50.00, 49.80, 49.60, 49.40, 49.20
- Moving Average (5 blocks): 49.60
- Moving Average (3 blocks): 49.40

The price limits would be:
- Downward limit: 49.60 * 0.95 = 47.12
- Upward limit: 49.40 * 1.10 = 54.34

This asymmetric design (5% down vs. 10% up) reflects the natural tendency of Zero-Coupon Bonds to increase in price as they approach maturity, allowing for more natural upward movement while protecting against sharp downward spikes.

## FAQ

### Why are downward price movements more restricted than upward movements?

Downward price movements are more restricted for several important reasons:
1. **Zero-Coupon Bond Characteristics**: Zero-Coupon Bonds naturally increase in price as they approach maturity, so downward movements are more likely to be anomalous
2. **Liquidation Protection**: Tighter downward limits help protect borrowers from unnecessary liquidations due to temporary price volatility
3. **Market Stability**: More restrictive downward limits prevent panic selling and market crashes
4. **Flash Loan Defense**: Stricter downward limits make it harder for attackers to manipulate prices downward to trigger liquidations
5. **Asymmetric Risk**: The risk of rapid price collapses is generally more damaging to the protocol than rapid price increases

### How are "Reliable Block Prices" determined?

Reliable Block Prices are determined through the following process:
1. **Price Validation**: Each block price must pass validation checks to be considered reliable
2. **Manipulation Detection**: Prices that show signs of manipulation are excluded
3. **Volume Requirements**: Blocks must have sufficient trading volume to be included
4. **Outlier Rejection**: Statistical methods identify and exclude outlier prices
5. **Recency Weighting**: More recent blocks have higher priority for inclusion

### What happens if there aren't enough Reliable Block Prices available?

If there aren't enough Reliable Block Prices available:
1. **Fallback Mechanism**: The system uses a fallback calculation based on available data
2. **Extended Timeframe**: The lookback period is extended until sufficient data is found
3. **Oracle Integration**: External price oracles may be consulted as a secondary source
4. **Conservative Limits**: More conservative limits are applied when data is limited
5. **Admin Notification**: Protocol administrators are notified of the data shortage

### Can the Circuit Breaker price limits be adjusted?

Yes, the Circuit Breaker price limits can be adjusted:
1. **Governance Process**: Changes to parameters require approval through protocol governance
2. **Market-Specific Adjustments**: Different markets may have different parameters based on their characteristics
3. **Volatility Adaptation**: Parameters can be adjusted in response to changing market volatility
4. **Periodic Review**: All parameters are reviewed quarterly to ensure they remain appropriate
5. **Emergency Adjustments**: In extreme market conditions, emergency parameter changes may be implemented

### How do the minimum movement allowances work?

The minimum movement allowances work as follows:
1. **Floor Value**: They establish a minimum price movement that's always allowed regardless of percentage calculations
2. **Market Efficiency**: They ensure that markets with very low prices can still function efficiently
3. **Calculation Priority**: The system uses whichever is more permissive: the percentage-based limit or the minimum movement
4. **Asymmetric Design**: Different minimum movements are set for upward (7.00) and downward (2.00) price changes
5. **Practical Application**: For example, if 5% of the Moving Average is less than 2.00, the 2.00 minimum is used instead

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

