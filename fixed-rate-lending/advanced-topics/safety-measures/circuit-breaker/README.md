---
description: A protective mechanism that prevents excessive price movements in the Fixed-Rate Lending Protocol
icon: 🚦
---

# 🚦 Circuit Breaker

## Overview

The Circuit Breaker is a protective mechanism used in the bond market to prevent excessive price movements and maintain stability. This user guide will explain what the Circuit Breaker is and why it is important for bond market participants.

## What You'll Learn

- What a Circuit Breaker is and how it functions in the bond market
- Why Circuit Breakers are essential for market stability
- How Circuit Breakers protect against flash loan attacks in crypto trading
- How the Secured Finance platform implements Circuit Breakers
- How the 3-threshold system works to prevent extreme volatility

## What is the Circuit Breaker in Bond Market?&#x20;

The Circuit Breaker in Bond Market is an automatic mechanism that temporarily suspends trading if there is a sudden and significant price movement. The Circuit Breaker is triggered when the price of bonds rises or falls beyond a certain pre-determined limit. The purpose of the Circuit Breaker is to prevent market participants from trading under extreme market conditions and to protect investors from significant losses due to sudden price fluctuations.

## Why is the Circuit Breaker Important?&#x20;

The Circuit Breaker is important for several reasons. First, it helps prevent panic selling or buying during periods of extreme volatility, which can cause prices to move rapidly and unpredictably. This can lead to significant losses for investors who are not able to react quickly enough. Second, it provides market participants with time to assess the situation and make informed decisions about their trades. This helps to prevent knee-jerk reactions that can lead to further market disruption. Finally, the Circuit Breaker promotes overall market stability by reducing the likelihood of extreme price movements and volatility.

## Any specific benefit from Circuit Breaker for crypto trading?

By setting the value threshold of the Circuit Breaker to dynamically change based on interest rates or loan duration, you can effectively mitigate the impact of a Flash loan attack. Restricting the price movement within a single block ensures that any potential damage is contained and doesn't escalate rapidly.

## How It Works

At our trading platform, we have implemented a circuit breaker mechanism that effectively sets price limitations for market movements within a single block. This mechanism applies to both our 'market order' and 'limit order' functions, ensuring that all orders adhere to a well-defined 3-threshold system. By doing so, we guarantee that orders remain within acceptable price ranges, effectively preventing extreme volatility and maintaining stability in our Zero Coupon bond market. The circuit breaker serves as a crucial tool to promote a secure and reliable trading environment, safeguarding both traders and the overall integrity of our platform. For a more detailed calculation, please consult the '[Formulaic for Circuit Breaker](price-range-limits.md)'.

## Key Parameters

| Parameter | Description | Typical Value |
|-----------|-------------|---------------|
| Soft Limit | First threshold for price movement monitoring | 0.5% of current price |
| Medium Limit | Second threshold with partial restrictions | 1.0% of current price |
| Hard Limit | Maximum allowed price movement per block | 1.5% of current price |
| Cooldown Period | Time before thresholds reset after triggering | 10 blocks |
| Threshold Calculation | How thresholds are determined | Based on volatility and liquidity |
| Adjustment Frequency | How often parameters are reviewed | Monthly |
| Implementation Level | Where the mechanism is enforced | Smart contract level |

## Examples

### Example 1: Normal Market Conditions

Under normal market conditions, the Circuit Breaker operates as follows:

1. A trader places a market order to buy 10,000 USDC worth of ETH bonds at the current market price of 95.00
2. The Circuit Breaker system checks if this order would cause the price to move beyond the allowed thresholds
3. Since the order size is moderate and market conditions are normal, the price impact is minimal (e.g., moving the price to 95.10)
4. The Circuit Breaker allows the order to execute normally since the price movement is within acceptable limits
5. The trade completes successfully and the new market price is established at 95.10

### Example 2: Flash Loan Attack Attempt

Consider a scenario where an attacker attempts to manipulate the market using a flash loan:

1. An attacker obtains a large flash loan of 1,000,000 USDC
2. They attempt to place a massive market order to artificially drive the price of ETH bonds up to 98.00 (a 3% move in a single block)
3. The Circuit Breaker detects that this order would cause the price to move beyond the maximum allowed threshold
4. The order is partially filled only up to the maximum allowed price movement (e.g., 95.50, representing the maximum allowed movement)
5. The remainder of the order is rejected, preventing the attacker from manipulating the market
6. The attacker fails to profit from the attempted manipulation and must repay their flash loan

### Example 3: Volatile Market Conditions

During periods of high volatility:

1. Market news causes a sudden increase in selling pressure for FIL bonds
2. Multiple sellers attempt to exit positions simultaneously, potentially causing a price crash
3. The Circuit Breaker activates as the price approaches the lower threshold
4. Orders are only filled up to the maximum allowed price movement
5. This prevents a market crash and gives participants time to reassess
6. Subsequent blocks can continue price discovery in a more orderly fashion
7. The market stabilizes without experiencing extreme price swings

## FAQ

### How does the Circuit Breaker protect against flash loan attacks?

The Circuit Breaker protects against flash loan attacks in several ways:
1. **Single-Block Limitation**: By limiting price movements within a single block, attackers cannot use flash loans to manipulate prices dramatically in the same transaction
2. **Dynamic Thresholds**: Thresholds are set based on market conditions, making them harder to predict and exploit
3. **Order Rejection**: Orders that would cause prices to move beyond thresholds are partially filled or rejected
4. **Time Buffer**: By forcing price movements to occur across multiple blocks, attackers must maintain positions longer, increasing their risk
5. **Monitoring Systems**: Unusual trading patterns trigger additional scrutiny and potential intervention

### What are the three thresholds in the Circuit Breaker system?

The three thresholds in our Circuit Breaker system are:

1. **Limitation on Downward Price Movement**: The platform restricts the downward price movement to 5% from the Moving Average of the most recent 5 Reliable Block Prices.

2. **Limitation on Upward Price Movement**: Conversely, upward price movement is capped at 10% from the Moving Average of the last 3 Reliable Block Prices.

3. **Maximum Price Fluctuation (Max Price Range)**: The market is permitted to move a maximum of 2.00 for downside and 7.00 for topside within a single block.

These thresholds are designed to prevent market manipulation and ensure stability while allowing for natural price discovery. For more detailed calculations, please refer to the [Price Range Limits](price-range-limits.md) page.

### Can the Circuit Breaker be bypassed or manipulated?

The Circuit Breaker is designed to be resistant to manipulation:
1. **On-Chain Implementation**: The mechanism is implemented directly in smart contracts, making it impossible to bypass
2. **Decentralized Verification**: All threshold calculations are transparent and verified by the network
3. **Dynamic Parameters**: Thresholds adjust based on market conditions, making them difficult to game
4. **Multi-Block Design**: Attempting to gradually push prices requires maintaining positions across multiple blocks, increasing cost and risk
5. **Governance Oversight**: Parameters are monitored and can be adjusted through governance if manipulation patterns emerge

### How does the Circuit Breaker affect my trading experience?

Under normal market conditions, most traders will not notice the Circuit Breaker:
1. **Typical Orders**: Standard-sized orders will execute normally without triggering any limits
2. **Market Stability**: The mechanism helps ensure more stable and predictable prices
3. **Execution Certainty**: You can be confident your orders won't execute at extremely unfavorable prices during volatility
4. **Partial Fills**: Very large orders might be partially filled if they would cause excessive price movement
5. **Protection**: Your positions are protected from flash crashes and manipulation attempts

### Are Circuit Breaker parameters the same for all assets?

No, Circuit Breaker parameters vary by asset:
1. **Asset-Specific Calibration**: Each asset has parameters calibrated to its specific volatility profile
2. **Liquidity Considerations**: More liquid assets may have tighter thresholds than less liquid ones
3. **Maturity Adjustment**: Bonds closer to maturity have different parameters than those with longer durations
4. **Periodic Review**: Parameters are reviewed regularly and adjusted based on market conditions
5. **Transparency**: Current parameters for each asset are publicly available in the protocol documentation

## Related Resources

- [Safety Measures](../README.md)
- [Base Price Adjustment](../base-price-adjustment.md)
- [Emergency Global Settlement](../emergency-global-settlement.md)
- [Mark to Market](../../../core-mechanics/liquidation/mark-to-market.md)
- [Price Range Limits](price-range-limits.md)



