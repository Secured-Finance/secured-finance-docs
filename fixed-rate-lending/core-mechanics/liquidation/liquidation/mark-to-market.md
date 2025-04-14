---
description: Real-Time Asset Valuation
---

# ⚖️ Mark to Market

## What is Mark to Market

Mark to Market is a pricing methodology where the value of an asset is calculated based on its current market value. In this methodology, the asset is valued at the current market price instead of its book value. We use this price to evaluate Profit and Loss (PnL) and Loan to Value (LTV) ratio.

## Our Method - Mark Price

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

#### Waterfall Mechanizm

1. Use ‘Opening Price’ for ‘Mark Price’ when Itayose Process Executed
2. Use ‘Auto-roll Price’ for ‘Mark Price’ if there are no block price
3. Use ‘Last traded price’ and/or ‘VWAP’ for ‘Mark to Market’ price during the same block if there is no matching orders have been executed before and no ‘Mark Price’ exist
   * [ ] If there are no ‘Mark Price’ exist yet, we remove the Volume Threshold above and use ‘last traded price’
