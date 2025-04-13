---
description: Efficient Asset Management
---

# ⏮️ Genesis Value

In the Secured Finance protocol, Genesis Value (GV) revolutionizes asset management by offering a more efficient and cost-effective approach to auto-roll and position calculations. GV is a dynamic value derived from a combination of Future Value (FV) and [Compound Factors](compound-factor.md). This section aims to provide a comprehensive explanation of what is Genesis Value, how it works, and why it is utilized.

### **What is Genesis Value**:&#x20;

Genesis Value represents the Asset Value of the Genesis Date. This serves as an important pillar of the protocol's Lazy Evaluation mechanism and allows for rational asset management without the need to frequently recalculate individual positions on the contract.

### **How Genesis Value Works**:&#x20;

The Genesis Value calculation is initiated based on a predetermined Genesis Date, which marks the starting point. For instance, if the Genesis Date is set to 30th June 2020, the protocol will begin GV calculations for this date.&#x20;

Upon auto-roll, as the nearest order book matures, the protocol captures the [Compound Factor](compound-factor.md) for the next 3-month tenor. This Compound Factor acts as the auto-roll price to calculate Future Value. Simultaneously, shorter than 3-month positions are converted into Genesis Value using the Compound Factors.

### **Why Genesis Value is Utilized**:&#x20;

The utilization of Genesis Value offers several compelling advantages for the Secured Finance protocol:

1. **Gas Cost Reduction**: Traditional approaches require recalculating Future Value for each position individually during auto-roll. However, Genesis Value eliminates the need for such redundant computations, resulting in significant gas cost reduction.
2. **Efficient Auto-Roll**: By leveraging Compound Factors and Genesis Value, the protocol can efficiently calculate Future Value for each position, streamlining the auto-roll process and minimizing computational overhead.
3. **Scalability and User-Friendliness**: Genesis Value's gas cost reduction makes the protocol more economically viable for users of all sizes, enhancing scalability, and encouraging broader participation in the ecosystem.
