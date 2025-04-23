---
description: Understanding the Itayose method for determining fair opening prices for new orderbooks
icon: 🤝
---

# 🤝 Itayose - Fair Price Discovery

## Overview

The Itayose is a key process in our protocol that determines the 'opening price' for a new orderbook every quarter when the nearest orderbook matures. We accept 'pre-open orders' 7 days before the new orderbook starts trading and use the Itayose process to set the opening price. This mechanism ensures fair price discovery and efficient market opening for new tenor periods.



## How It Works

The Itayose process operates in three distinct phases to ensure a fair and efficient opening of each new orderbook.

### Before Itayose

Seven days before the launch of new tenor periods, our platform will indicate that these new tenor periods are available for users to place their pre-open orders. **Users can only place 'limit orders' on one side.** One hour before the launch, the orderbook will be frozen, and users will not be able to take any action on the orderbook. This includes placing, amending, or canceling orders.

{% hint style="info" %}
_During this 7-day pre-open phase, our yield curve view provides additional transparency by displaying the Annual Percentage Rate (APR) calculated based on the estimated **'opening price'**. This offers a clear picture of the expected yield at the time the market starts, giving participants valuable insights for making informed trading decisions._
{% endhint %}

### During Itayose

Once the orderbook is frozen, the Smart Contract for the Itayose process will be activated. This process consolidates all overlapping bids and offers. _**If there are no overlapping orders, there will be no matching, and the market will open without an opening price.**_

For all overlapping orders, we calculate the **opening price** based on:

* The sum of the lend amount
* The sum of the borrow amount
* The execution amount of the opening price ("first come, first serve")
* The imbalance between the lend and borrow
* If there is no imbalance, the mid-price is taken

{% hint style="info" %}
To encourage people to place opening orders closer to the market level for efficient execution and enable everyone to discover the opening price, **transaction fees will be waived during the Itayose process**.
{% endhint %}

### After Itayose

All orders that were not filled by the Itayose process will remain in the Orderbook and start trading normally after the market opens. _**All orders that were executed by the Itayose process will be filled at the 'opening price'.**_

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Pre-Open Order Period | Time before new orderbook launch when users can place orders | 7 days |
| Orderbook Freeze | Time before launch when orderbook is frozen for Itayose | 1 hour |
| Order Types Allowed | Types of orders accepted during pre-open period | Limit orders only |
| Transaction Fees | Fees charged for orders executed during Itayose | Waived (0%) |
| Price Calculation Method | How opening price is determined | Based on order imbalance and mid-price |
| Order Execution Priority | How orders are prioritized for execution | First come, first serve |

## Examples

### Example 1: Balanced Order Book

Consider a new 3-month USDC-ETH Zero-Coupon Bond orderbook opening:

1. During the 7-day pre-open period, the following orders are placed:
   - Lend orders: 50,000 USDC at 98.00, 30,000 USDC at 98.20, 20,000 USDC at 98.40
   - Borrow orders: 40,000 USDC at 98.50, 35,000 USDC at 98.30, 25,000 USDC at 98.10

2. The overlapping price range is 98.10-98.40 (borrow orders willing to pay ≥ 98.10, lend orders willing to accept ≤ 98.40)

3. Total lend amount in the overlapping range: 100,000 USDC
   Total borrow amount in the overlapping range: 100,000 USDC

4. Since the amounts are balanced, the opening price is set at the mid-price: 98.25

5. All orders are executed at 98.25, and the market opens with no remaining orders from the Itayose process

### Example 2: Imbalanced Order Book (More Lenders)

For a new 3-month USDC-FIL Zero-Coupon Bond orderbook:

1. During the pre-open period, these orders are placed:
   - Lend orders: 80,000 USDC at 97.50, 60,000 USDC at 97.70, 40,000 USDC at 97.90
   - Borrow orders: 50,000 USDC at 98.00, 40,000 USDC at 97.80, 30,000 USDC at 97.60

2. The overlapping price range is 97.60-97.90

3. Total lend amount in the overlapping range: 180,000 USDC
   Total borrow amount in the overlapping range: 120,000 USDC

4. Due to the imbalance (more lenders than borrowers), the price is set closer to the lend side: 97.70

5. All borrow orders in the range (120,000 USDC) are filled
   Only 120,000 USDC of the lend orders are filled (based on first-come-first-serve)
   Remaining 60,000 USDC of lend orders stay in the orderbook when trading begins

### Example 3: No Overlapping Orders

For a new 3-month USDC-AVAX Zero-Coupon Bond orderbook:

1. During the pre-open period, these orders are placed:
   - Lend orders: 30,000 USDC at 96.00, 25,000 USDC at 96.20, 20,000 USDC at 96.40
   - Borrow orders: 35,000 USDC at 95.80, 30,000 USDC at 95.60, 25,000 USDC at 95.40

2. There is no overlapping price range (highest borrow price 95.80 < lowest lend price 96.00)

3. No Itayose matching occurs

4. The market opens without an opening price, and all pre-open orders remain in the orderbook

### Example 4: Initial Orderbook Launch

For the very first 3-month USDC-BTC Zero-Coupon Bond orderbook:

1. The platform announces the new market with an estimated opening price of 97.00 (based on market research)

2. During the pre-open period, these orders are placed:
   - Lend orders: 40,000 USDC at 96.80, 35,000 USDC at 97.00, 30,000 USDC at 97.20
   - Borrow orders: 45,000 USDC at 97.30, 40,000 USDC at 97.10, 35,000 USDC at 96.90

3. The overlapping price range is 96.90-97.20

4. Total lend amount in the overlapping range: 105,000 USDC
   Total borrow amount in the overlapping range: 120,000 USDC

5. Due to the imbalance (more borrowers than lenders), the price is set closer to the borrow side: 97.10

6. All lend orders in the range (105,000 USDC) are filled
   Only 105,000 USDC of the borrow orders are filled (based on first-come-first-serve)
   Remaining 15,000 USDC of borrow orders stay in the orderbook when trading begins

## Common Questions

### Why is the Itayose process important for new orderbooks?

The Itayose process serves several critical functions:
1. **Fair Price Discovery**: Establishes a market-determined opening price that reflects supply and demand
2. **Liquidity Aggregation**: Consolidates orders from multiple participants to create initial market depth
3. **Reduced Volatility**: Prevents excessive price swings that might occur with sequential matching
4. **Equal Opportunity**: Gives all participants the same chance to participate in the opening price
5. **Market Efficiency**: Ensures the most efficient clearing price that maximizes execution volume

### Can I place both lend and borrow orders during the pre-open period?

No, during the pre-open period:
1. **Single-Side Restriction**: Users can only place orders on one side (either lend or borrow)
2. **Strategic Focus**: This restriction encourages participants to focus on their primary trading intent
3. **Manipulation Prevention**: Prevents users from artificially creating both sides of the market
4. **Clear Intent**: Ensures that the opening price reflects genuine market sentiment
5. **Order Management**: Simplifies the order management process during the critical opening phase

### What happens if I try to cancel my order right before the Itayose process?

Order cancellation is restricted as follows:
1. **Freeze Period**: Orders cannot be canceled during the 1-hour freeze period before launch
2. **Commitment Enforcement**: This ensures participants commit to their orders for the Itayose process
3. **Market Integrity**: Prevents last-minute withdrawals that could disrupt price discovery
4. **Planning Requirement**: Users must plan their orders carefully before the freeze period begins
5. **System Protection**: The freeze allows the system to prepare for the Itayose calculation without disruption

### How is the opening price determined when there's an imbalance between lend and borrow orders?

When there's an imbalance:
1. **Volume Maximization**: The price that maximizes the execution volume is selected
2. **Imbalance Direction**: The price shifts toward the side with more orders (higher supply or demand)
3. **Price Range**: The price must fall within the overlapping range of lend and borrow orders
4. **Partial Fills**: Orders on the side with greater volume receive partial fills based on time priority
5. **Remaining Orders**: Unfilled portions remain in the orderbook when normal trading begins

### Why are transaction fees waived during the Itayose process?

Transaction fees are waived for several reasons:
1. **Participation Incentive**: Encourages more users to participate in the price discovery process
2. **Market Formation**: Helps establish a more liquid and efficient market from the start
3. **Fair Access**: Removes cost barriers that might discourage smaller participants
4. **Price Accuracy**: Results in more orders and thus a more accurate opening price
5. **Market Adoption**: Promotes adoption of new markets and tenor periods

## Related Resources

- [New Market Listing and Delisting](README.md)
- [Market Dynamics](../../README.md)
- [Orderbook Rotation](../../../orderbook-deep-dive/orderbook-rotation.md)
- [Order Types](../../../../core-mechanics/order-book-system/order-type.md)

