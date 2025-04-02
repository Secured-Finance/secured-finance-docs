---
description: The Most Efficient Way of Find Price from Orderbook Openings
---

# 🤝 Itayose - Fair Price Discovery

The Itayose is a key process in our protocol that determines the 'opening price' for a new orderbook every quarter when the nearest orderbook matures. We accept 'pre-open orders' 7 days before the new orderbook starts trading and use the Itayose process to set the opening price. Only limit orders are accepted before trading begins.

## Itayose Rules

### Before Itayose

Seven days before the launch of new tenor periods, our platform will indicate that these new tenor periods are available for users to place their pre-open orders. **Users can only place 'limit orders' on one side.** One hour before the launch, the orderbook will be frozen, and users will not be able to take any action on the orderbook. This includes placing, amending, or canceling orders.

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

The Itayose Method is a critical part of our protocol, ensuring a fair and efficient opening of each new orderbook.



{% hint style="info" %}
_During this 7 days pre-open phase, our yield curve view provides additional transparency by displaying the Annual Percentage Rate (APR) calculated based on the estimated **'opening price'**. This offers a clear picture of the expected yield at the time the market starts, giving participants valuable insights for making informed trading decisions._
{% endhint %}

