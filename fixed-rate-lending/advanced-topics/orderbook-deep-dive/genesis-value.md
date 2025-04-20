---
description: Understanding how Genesis Value enables efficient asset management in the Fixed-Rate Lending Protocol
icon: ⏮️
---

# ⏮️ Genesis Value

## Overview

In the Secured Finance protocol, Genesis Value (GV) revolutionizes asset management by offering a more efficient and cost-effective approach to auto-roll and position calculations. GV is a dynamic value derived from a combination of Future Value (FV) and Compound Factors. Genesis Value represents the Asset Value of the Genesis Date and serves as an important pillar of the protocol's Lazy Evaluation mechanism.

## What You'll Learn

- What Genesis Value is and why it's important in the Fixed-Rate Lending Protocol
- How Genesis Value calculations work with the Genesis Date
- How Genesis Value interacts with Compound Factors during auto-roll
- The advantages of using Genesis Value for gas cost reduction
- How Genesis Value improves scalability and user experience

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
