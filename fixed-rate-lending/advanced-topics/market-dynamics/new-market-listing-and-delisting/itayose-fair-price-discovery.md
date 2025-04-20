---
description: Understanding the Itayose method for determining fair opening prices for new orderbooks
icon: 🤝
---

# 🤝 Itayose - Fair Price Discovery

## Overview

The Itayose is a key process in our protocol that determines the 'opening price' for a new orderbook every quarter when the nearest orderbook matures. We accept 'pre-open orders' 7 days before the new orderbook starts trading and use the Itayose process to set the opening price. This mechanism ensures fair price discovery and efficient market opening for new tenor periods.

## What You'll Learn

- How the Itayose process works to determine opening prices for new orderbooks
- The timeline and rules for placing pre-open orders
- How opening prices are calculated from overlapping orders
- What happens to unfilled orders after the Itayose process
- Why transaction fees are waived during the Itayose process

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

## Related Resources

- [New Market Listing and Delisting](README.md)
- [Market Dynamics](../../README.md)
- [Orderbook Rotation](../../../orderbook-deep-dive/orderbook-rotation.md)
- [Order Types](../../../../core-mechanics/order-book-system/order-type.md)

