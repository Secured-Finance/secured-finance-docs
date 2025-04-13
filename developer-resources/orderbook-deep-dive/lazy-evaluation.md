---
description: 'Optimizing Gas Costs: The Intersection of Lazy Evaluation'
---

# ⏯️ Lazy Evaluation

Secured Finance has introduced a revolutionary feature known as “lazy evaluation,” which significantly streamlines the management of orders and the auto-roll process. This mechanism works by deferring the computation and update of orders and positions until absolutely necessary. As a result, it eliminates the need to manually roll over each position or update a multitude of open orders whenever an order is filled. This approach not only leads to substantial savings in [gas costs](../../resources/knowledge-base/gas-cost.md) but also boosts the overall efficiency of the protocol.

### States of Orders:

Orders in the system can exist in three states: Open Order, Active Position (FV), and Auto-rolled Position (GV).&#x20;

1. Open Order: Remaining Orders which is not filled on our orderbook system.
2. Active Position (FV): Once Orders are filled, it will be managed by Future Value (FV)
3. Auto-rolled Position (GV): Positions that have reached their maturity date will be Auto-rolled without any action and managed by [Genesis Value](genesis-value.md) (GV).



**Lazy evaluation is utilized for all states above**. For Open Orders, the contract checks if the order has been unlinked on the red-black tree, indicating that the order has already been filled. As for Active Positions (FV), if the positions reach their maturity date, they are then treated as Auto-rolled Positions (GV) and returned as such. As for Auto-rolled Positions (GV), only borrowing positions will increase after each roll. (Please refer to the [Compound Factor](broken-reference) for more detail)

### States update:

Lazy evaluation continues to be applied to these data as long as they exist. However, when a CleanUp process is executed, the state of the data changes, and they are no longer subject to lazy evaluation once it turned to GV. CleanUp processes are implicitly executed during certain operations taken by users such as order execution, collateral withdrawals, and so on.

{% hint style="info" %}
To optimize the gas costs of lazy evaluation, market contracts that have reached maturity are recycled, and new markets are opened. This ensures efficient utilization of gas costs for lazy evaluation. Please refer to the [ Orderbook Life Cycle](market-life-cycle.md)
{% endhint %}

### Smart Contract Storage and Real-Time Calculation:&#x20;

The above states are stored on the smart contract storage, ensuring data integrity and consistency. When a user calls the smart contract to retrieve their own amount, the system calculates the actual amount in real-time, providing up-to-date and accurate information.

### Importance in Supporting Key Functionalities:&#x20;

Lazy order evaluation is a critical component for supporting essential functionalities such as market orders and auto-roll. Without it, executing these operations would result in substantial gas costs, particularly in terms of storage. By adopting lazy evaluation, Secured Finance streamlines its platform and ensures a more cost-effective and user-friendly experience for all participants.

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>
