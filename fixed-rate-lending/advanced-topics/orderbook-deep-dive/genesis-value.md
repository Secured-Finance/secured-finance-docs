---
description: Understanding how Genesis Value enables efficient asset management in the Fixed-Rate Lending Protocol
icon: ⏮️
---

# ⏮️ Genesis Value

## Overview

In the Secured Finance protocol, Genesis Value (GV) revolutionizes asset management by offering a more efficient and cost-effective approach to auto-roll and position calculations. GV is a dynamic value derived from a combination of Future Value (FV) and Compound Factors. Genesis Value represents the Asset Value of the Genesis Date and serves as an important pillar of the protocol's Lazy Evaluation mechanism.

## How It Works

Genesis Value allows for rational asset management without the need to frequently recalculate individual positions on the contract, providing significant efficiency improvements.

### Genesis Value Calculation

The Genesis Value calculation is initiated based on a predetermined Genesis Date, which marks the starting point. For instance, if the Genesis Date is set to 30th June 2020, the protocol will begin GV calculations for this date.

Upon auto-roll, as the nearest order book matures, the protocol captures the Compound Factor for the next 3-month tenor. This Compound Factor acts as the auto-roll price to calculate Future Value. Simultaneously, shorter than 3-month positions are converted into Genesis Value using the Compound Factors.

### Benefits of Genesis Value

The utilization of Genesis Value offers several compelling advantages for the Secured Finance protocol:

1. **Gas Cost Reduction**: Traditional approaches require recalculating Future Value for each position individually during auto-roll. However, Genesis Value eliminates the need for such redundant computations, resulting in significant gas cost reduction.

2. **Efficient Auto-Roll**: By leveraging Compound Factors and Genesis Value, the protocol can efficiently calculate Future Value for each position, streamlining the auto-roll process and minimizing computational overhead.

3. **Scalability and User-Friendliness**: Genesis Value's gas cost reduction makes the protocol more economically viable for users of all sizes, enhancing scalability, and encouraging broader participation in the ecosystem.

## Examples

### Example 1: Genesis Value Calculation for a New Position

Let's walk through how Genesis Value is calculated when a user opens a new lending position:

1. Initial setup:
   - Genesis Date: June 30, 2020
   - Current Date: September 15, 2023
   - User deposits 1,000 USDC to lend
   - Current Lending Compound Factor (LCF): 1.45 (accumulated since Genesis Date)
   - Current market price: 97.50

2. Calculate the Genesis Value:
   ```
   Genesis Value = Future Value / Current LCF
   Genesis Value = 1,000 / 1.45
   Genesis Value = 689.66
   ```

3. This Genesis Value (689.66) is stored and remains constant for this lending position throughout its lifetime.

4. When the user wants to calculate their current position value:
   ```
   Future Value = Genesis Value × Current LCF
   Future Value = 689.66 × 1.45
   Future Value = 1,000
   ```

### Example 2: Auto-Roll Impact on Genesis Value

Let's examine how Genesis Value remains stable during auto-roll events:

1. Initial position:
   - Genesis Value (GV) for a lender: 500 USDC
   - Current Lending Compound Factor (LCF): 1.20
   - Current Future Value: 500 × 1.20 = 600 USDC

2. Auto-roll occurs with the following parameters:
   - Auto-roll price: 98.50
   - Auto-roll fee rate: 0.001 (0.1%)
   - New Lending Compound Factor: 1.20 × (1/0.985 - 0.001) = 1.20 × 1.014 = 1.2168

3. After auto-roll, the lender's position:
   - Genesis Value remains unchanged at 500 USDC
   - Updated Future Value: 500 × 1.2168 = 608.4 USDC

4. The lender's position has grown by 8.4 USDC without requiring recalculation of their Genesis Value.

### Example 3: Gas Cost Comparison

Let's compare gas costs between traditional position calculation and Genesis Value approach:

1. Traditional approach for 1,000 positions during auto-roll:
   - Each position requires individual Future Value recalculation
   - Approximate gas cost per recalculation: 20,000 gas
   - Total gas cost: 1,000 × 20,000 = 20,000,000 gas

2. Genesis Value approach:
   - Only need to update the Compound Factor once
   - Approximate gas cost for updating Compound Factor: 50,000 gas
   - Individual position values can be calculated off-chain using the updated Compound Factor
   - Total gas cost: 50,000 gas

3. Gas savings: 20,000,000 - 50,000 = 19,950,000 gas (99.75% reduction)

4. This significant gas reduction makes the protocol more economically viable, especially during periods of high Ethereum gas prices.

## FAQ

### How does Genesis Value differ from Future Value?

Genesis Value and Future Value differ in several important ways:
1. **Time Reference**: Genesis Value represents the value at the Genesis Date, while Future Value represents the current or maturity value
2. **Stability**: Genesis Value remains constant for lenders, while Future Value changes with each auto-roll
3. **Calculation Base**: Genesis Value is the base value used to calculate Future Value using Compound Factors
4. **Storage Efficiency**: Storing Genesis Value requires less frequent updates, reducing gas costs
5. **User Perspective**: Users typically interact with Future Value (what their position is worth), while Genesis Value works behind the scenes

### Why use a fixed Genesis Date instead of each user's entry date?

Using a fixed Genesis Date offers several advantages:
1. **Standardization**: All positions reference the same starting point, simplifying calculations
2. **Computational Efficiency**: A single reference point reduces the complexity of tracking individual entry dates
3. **Protocol Consistency**: Ensures all positions follow the same calculation methodology
4. **Gas Optimization**: Reduces the storage and computation requirements for the protocol
5. **Scalability**: Makes the system more scalable as the number of users increases

### How does Genesis Value handle different currencies and assets?

Genesis Value handles different currencies and assets through:
1. **Asset-Specific Compound Factors**: Each asset pair has its own set of Compound Factors
2. **Independent Calculations**: Genesis Values for different assets are calculated independently
3. **Currency Neutrality**: The concept works regardless of the underlying currency or asset
4. **Consistent Methodology**: The same calculation principles apply across all supported assets
5. **Separate Orderbooks**: Each asset pair has separate orderbooks with their own Genesis Values

### What happens to Genesis Value during extreme market conditions?

During extreme market conditions:
1. **Stability Preservation**: Genesis Value remains stable even during market volatility
2. **Compound Factor Adjustments**: Market conditions affect Compound Factors, not Genesis Values
3. **Circuit Breaker Protection**: Circuit breakers may limit extreme price movements that would affect Compound Factors
4. **Governance Oversight**: In extreme cases, governance mechanisms can intervene to ensure system stability
5. **Risk Isolation**: The separation of Genesis Value from market prices helps isolate positions from short-term volatility

### Can users manipulate their Genesis Value?

Users cannot manipulate their Genesis Value because:
1. **Protocol-Controlled Calculation**: Genesis Value is calculated by the protocol, not set by users
2. **Immutable After Creation**: Once set, a position's Genesis Value cannot be altered
3. **Market-Driven Factors**: Compound Factors are determined by market forces, not individual users
4. **Transparent Formulas**: All calculations follow transparent, predetermined formulas
5. **Audit Trail**: All Genesis Value calculations are recorded on-chain and can be verified

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Genesis Date | Starting point for Genesis Value calculations | Protocol-defined date (e.g., June 30, 2020) |
| Genesis Value (GV) | Asset Value at the Genesis Date | Calculated based on position and Compound Factors |
| Future Value (FV) | Projected value calculated from GV | GV × Lending Compound Factor |
| Auto-Roll Period | Frequency of orderbook maturity and GV recalculation | 3 months |
| Position Conversion | How shorter positions are handled | Converted to GV using Compound Factors |

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Compound Factor](compound-factor.md)
- [Lazy Evaluation](lazy-evaluation.md)
- [Auto-Rolling](../../market-dynamics/auto-rolling/README.md)
