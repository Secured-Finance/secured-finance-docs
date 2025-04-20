---
description: Understanding how assets are valued at current market prices in the Fixed-Rate Lending Protocol
icon: ⚖️
---

# ⚖️ Mark to Market

## Overview

Mark to Market is a pricing methodology where the value of an asset is calculated based on its current market value. In this methodology, the asset is valued at the current market price instead of its book value. We use this price to evaluate Profit and Loss (PnL) and Loan to Value (LTV) ratio.



## How It Works

In our approach to mark-to-market valuation, we focus on zero-coupon bond market pricing, utilizing the 'Mark Price' as our benchmark. This price is derived from the Volume Weighted Average Price (VWAP) calculated over the duration of a single block. Notably, our methodology emphasizes the use of Future Value (FV) in these calculations, as opposed to the more traditional Present Value (PV) approach.&#x20;

> #### Example of FV approach for the VWAP
>
> In the scenario where transactions A and B occur within the same block, a traditional application of the Volume Weighted Average Price (VWAP) would give a value of 93.00, as illustrated in the example below. However, this traditional VWAP calculation does not adequately represent the relationship between Present Value (PV) and Future Value (FV). To address this, we calculate our Block Price by adopting a methodology centered on the FV approach, ensuring a more accurate reflection of market dynamics and valuation in our decentralized finance context.

| Transaction | PV amount | Price | FV amount | VWAP  |
| ----------- | --------- | ----- | --------- | ----- |
| A           | 1,000     | 94.00 | 1,063.83  |       |
| B           | 1,000     | 92.00 | 1,086.96  |       |
| Sum         | 2,000     |       | 2,150.79  | 92.99 |

To safeguard against potential price manipulation within a block, we have implemented a **minimum volume threshold**. This measure ensures that only transactions meeting this specified volume criteria contribute to the block's pricing, thereby maintaining the integrity and reliability.

#### Current Volume Threshold

| Currency | Minimum Volume Threshold |
| -------- | ------------------------ |
| USD      | 100                      |

Should the trading volume within a block fall below our established threshold, we opt not to record the block price for that particular interval. Instead, we continue using the price from the most recent block that met or exceeded this volume threshold for our mark-to-market calculations. This threshold is not arbitrary; it is meticulously calculated for each currency based on the spot price provided by the Chainlink oracle, ensuring accuracy and relevance to current market conditions.

{% hint style="info" %}
We review and revise Volume Threshold periodically.
{% endhint %}

#### Waterfall Mechanism

1. Use 'Opening Price' for 'Mark Price' when Itayose Process Executed
2. Use 'Auto-roll Price' for 'Mark Price' if there are no block price
3. Use 'Last traded price' and/or 'VWAP' for 'Mark to Market' price during the same block if there is no matching orders have been executed before and no 'Mark Price' exist
   * If there are no 'Mark Price' exist yet, we remove the Volume Threshold above and use 'last traded price'

## Examples

### Example 1: Calculating Mark Price with Sufficient Volume

Consider a market with the following transactions in a single block:

| Transaction | PV amount | Price | FV amount |
|-------------|-----------|-------|-----------|
| A           | 500       | 95.00 | 526.32    |
| B           | 700       | 93.00 | 752.69    |
| C           | 300       | 94.00 | 319.15    |
| Total       | 1,500     |       | 1,598.16  |

The total volume (1,500) exceeds the minimum threshold of 100 USD, so the Mark Price is calculated:
- VWAP = Total PV / Total FV = 1,500 / 1,598.16 = 93.86

This Mark Price (93.86) will be used for all mark-to-market calculations in this block and subsequent blocks until a new valid Mark Price is established.

### Example 2: Using the Waterfall Mechanism

Scenario: A new market has just been created through the Itayose process with an Opening Price of 95.00.

1. **Day 1**: No trades occur. The Mark Price remains 95.00 (from Itayose Opening Price).
2. **Day 2**: A few small trades occur with a total volume of 50 USD (below the threshold). The Mark Price remains 95.00.
3. **Day 3**: The market matures and undergoes Auto-rolling with an Auto-roll Price of 94.50. The Mark Price updates to 94.50.
4. **Day 4**: Significant trading activity occurs with a volume of 200 USD and a VWAP of 94.20. The Mark Price updates to 94.20.

This example demonstrates how the waterfall mechanism ensures there is always a valid Mark Price available for collateral valuation and liquidation calculations.

## FAQ

### Why use Future Value (FV) instead of Present Value (PV) for VWAP calculations?

Using Future Value (FV) in our VWAP calculations provides a more accurate representation of the true economic value of zero-coupon bonds. Since zero-coupon bonds are traded at a discount to their face value and redeemed at maturity for their full face value, the FV approach better captures the relationship between current prices and future obligations. This method ensures that our mark-to-market valuations reflect the actual economic exposure of positions in the protocol.

### How does the minimum volume threshold protect against price manipulation?

The minimum volume threshold prevents small trades from disproportionately affecting the Mark Price. Without this threshold, an attacker could execute a small trade at an artificially high or low price to manipulate the Mark Price, potentially triggering unwarranted liquidations or preventing necessary ones. By requiring a minimum trading volume (currently 100 USD), we ensure that only significant market activity influences the Mark Price, making manipulation more costly and less feasible.

### What happens if there's no trading activity for an extended period?

If there's no trading activity that meets the minimum volume threshold for an extended period, the protocol continues to use the last valid Mark Price according to the waterfall mechanism. This ensures continuity in valuation even during periods of low market activity. The waterfall mechanism prioritizes:
1. Opening Price from Itayose Process
2. Auto-roll Price
3. Last traded price/VWAP

This approach maintains system stability while still allowing for price updates when significant market activity resumes.

### How often is the Mark Price updated?

The Mark Price is updated on a block-by-block basis whenever there is sufficient trading volume (above the minimum threshold) within a block. If multiple trades occur within the same block, they are aggregated into a single VWAP calculation. If no trades meeting the threshold occur in a block, the Mark Price remains unchanged from the previous valid Mark Price.

### Can users see the current Mark Price for each market?

Yes, users can view the current Mark Price for each market through the protocol's interface. This transparency allows users to understand how their positions are being valued and to make informed decisions about their borrowing and lending activities. The Mark Price is a critical component for calculating collateralization ratios and determining when positions may be at risk of liquidation.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Minimum Volume Threshold | Minimum trading volume required for Mark Price updates | 100 USD |
| VWAP Calculation Method | How the Volume Weighted Average Price is calculated | Future Value (FV) approach |
| Price Update Frequency | How often the Mark Price can be updated | Per block |
| Waterfall Priority | Order of price sources used when determining Mark Price | 1. Itayose Opening Price<br>2. Auto-roll Price<br>3. Last traded price/VWAP |

## Related Resources

- [Liquidation](README.md)
- [Collateralization](../../collateralization.md)
- [Safety Measures](../../../advanced-topics/safety-measures/README.md)
- [Circuit Breaker](../../../advanced-topics/safety-measures/circuit-breaker/README.md)
