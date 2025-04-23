---
description: Understanding how prices are determined for the Auto-Rolling mechanism
icon: 💰
---

# 💰 Price Discovery for Auto-Rolling

## Overview

The auto-rolling price discovery mechanism is a critical component of Secured Finance's platform. It ensures that the pricing for the quarterly roll is calculated accurately and fairly, preventing potential price manipulation. This mechanism is designed to adapt to varying market conditions, ranging from normal and liquid conditions to less liquid or extreme situations with no liquidity.



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

## Examples

### Example 1: Normal and Liquid Market Condition

Consider a 3-month USDC-ETH Zero-Coupon Bond approaching maturity on June 30th:

1. During the 6-hour window before maturity (12:00-18:00 UTC on June 30th), the following transactions occur:
   - 10,000 USDC worth of bonds traded at 99.20
   - 25,000 USDC worth of bonds traded at 99.15
   - 15,000 USDC worth of bonds traded at 99.25

2. The volume-weighted average price is calculated:
   ```
   VWAP = (10,000 × 99.20 + 25,000 × 99.15 + 15,000 × 99.25) / (10,000 + 25,000 + 15,000)
   VWAP = (992,000 + 2,478,750 + 1,488,750) / 50,000
   VWAP = 4,959,500 / 50,000 = 99.19
   ```

3. The auto-roll price for the new September 30th bonds is set at 99.19, reflecting the fair market value based on actual trading activity.

### Example 2: Less Liquid Market Condition

For a 3-month USDC-FIL Zero-Coupon Bond approaching maturity:

1. No transactions occur during the 6-hour window before maturity
2. The current Mark Price for the bond is 98.50
3. The duration adjustment factor is calculated based on the time to maturity of the new bonds (3 months)
4. If the duration adjustment factor is 0.995, the auto-roll price would be:
   ```
   Auto-Roll Price = 98.50 × 0.995 = 98.01
   ```
5. The new bonds begin trading at 98.01, reflecting the Mark Price adjusted for the new duration

### Example 3: Extreme Market Condition

For a thinly traded 3-month USDC-WBTC Zero-Coupon Bond:

1. No transactions have occurred in the last 3 months
2. The previous roll price (from the last maturity date) was 97.80
3. The auto-roll price is set at 97.80, maintaining continuity with the last known market-determined price
4. This ensures that even in extremely illiquid conditions, the roll price has some basis in market history

### Example 4: Initial Roll with No Transaction History

When launching a new 3-month USDC-AVAX Zero-Coupon Bond market:

1. The initial offering price at launch was 95.00
2. No transactions occur on the second orderbook (for the next maturity date) before the first roll
3. The duration adjustment factor for the new bonds is 0.998
4. The auto-roll price is calculated as:
   ```
   Auto-Roll Price = 95.00 × 0.998 = 94.81
   ```
5. The new bonds begin trading at 94.81, providing a fair starting point based on the initial launch price

## Common Questions

### Why use different price discovery methods based on market conditions?

Different price discovery methods are used for several reasons:
1. **Market Efficiency**: In liquid markets, actual transaction prices provide the most accurate reflection of market sentiment
2. **Manipulation Prevention**: Volume-weighted averaging prevents single transactions from unduly influencing the roll price
3. **Continuity**: In less liquid conditions, using Mark Price or previous roll prices ensures continuity and prevents arbitrary pricing
4. **Adaptability**: The tiered approach allows the protocol to adapt to varying market conditions across different assets
5. **Fairness**: Each method is designed to produce the most fair and representative price given the available market data

### How does the 6-hour observation window protect against manipulation?

The 6-hour observation window provides several protections:
1. **Extended Duration**: The lengthy window makes it costly to manipulate prices throughout the entire period
2. **Volume Weighting**: Larger trades have more impact on the final price, making manipulation more expensive
3. **Transparency**: All participants know when the observation window occurs, allowing for fair participation
4. **Market Depth**: The window captures a broader sample of market activity, diluting the impact of any single trade
5. **Predictability**: The consistent methodology prevents arbitrary pricing decisions

### What happens if there's a sudden market shock during the observation window?

During market shocks in the observation window:
1. **Volume Weighting**: The methodology still applies, with larger trades having more influence
2. **Market Forces**: The price discovery reflects genuine market sentiment, even if volatile
3. **No Circuit Breakers**: The observation window does not have special circuit breakers, as it's capturing market consensus
4. **Risk Management**: Users aware of the upcoming roll can manage their positions accordingly
5. **Subsequent Trading**: After the roll, normal market mechanisms including circuit breakers apply to the new bonds

### How is the duration adjustment calculated for less liquid conditions?

The duration adjustment is calculated as follows:
1. **Time Value Principle**: Accounts for the time value of money between different maturity periods
2. **Yield Curve Consideration**: Incorporates the current shape of the yield curve
3. **Risk Premium**: Includes adjustments for term premium between different durations
4. **Market Conditions**: Takes into account current market conditions and volatility
5. **Consistency**: Ensures consistent pricing between bonds of different maturities

### Can users predict or influence the auto-roll price?

Users have limited ability to influence the auto-roll price:
1. **Transparent Mechanism**: The methodology is transparent, but requires significant capital to meaningfully impact
2. **Economic Disincentives**: Attempting to manipulate prices typically results in unfavorable execution for the manipulator
3. **Volume Requirements**: The volume-weighted approach requires substantial trading to shift the average price
4. **Market Forces**: Other participants can counter manipulation attempts if prices deviate from fair value
5. **Multiple Methods**: The fallback methods for less liquid markets are resistant to direct manipulation

## Related Resources

- [Auto-Rolling](README.md)
- [Market Dynamics](../../README.md)
- [Mark to Market](../../../../core-mechanics/liquidation/mark-to-market.md)
- [Orderbook Rotation](../../../orderbook-deep-dive/orderbook-rotation.md)
