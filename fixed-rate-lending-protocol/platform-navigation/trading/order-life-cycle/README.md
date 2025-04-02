---
description: Understanding how your order begins and ends
---

# 🪃 Order Life Cycle

In this section, we aim to demystify the various stages your order may undergo, providing clarity on your current order status, which is accessible through the 'Order History' tab on our [portfolio page.](https://app.gitbook.com/o/DralddHerVJQe2eHzg9a/s/5n2yKWdxy0II5Sd3ZIQL/~/changes/105/platform-guide/trading-interface/portfolio)&#x20;

## Life Cycle Representation by Order Statuses

As you embark on your trading journey with us, you initially select an Order Type—either 'Market Order' or 'Limit Order', as detailed in the [preceding section](../order-type.md). As your order progresses, it will assume one of seven distinct states that delineate its current status and actions being undertaken on it.

<figure><img src="../../../../.gitbook/assets/image (116).png" alt=""><figcaption><p>Order Status Diagram</p></figcaption></figure>

1.  **Open**

    Exclusive to Limit Order. This state indicates an order is awaiting execution, pending the market price reaching the specified limit.&#x20;
2.  **Partially Filled**

    Applicable to both Market and Limit Order. Indicates that only a portion of the order has been executed, due to limited liquidity at the desired price.&#x20;
3.  **Filled**

    Relevant for both Market and Limit Orders, signifying complete execution. Market Orders achieve this state almost immediately at current market prices, while Limit Orders do so once the market price meets the specified limit.
4.  **Killed**

    Specific to Market Orders that have been partially filled. This state indicates that the order cannot proceed to full execution due to **insufficient liquidity**.
5.  **Blocked**

    It pertains solely to market order and arises in exceptional regulatory conditions, such as the activation of [**circuit breakers**](../../../protocol-security-and-safety/circuit-breaker/)**.**&#x20;
6.  **Canceled**

    This state is possible for Limit Order. The trader can cancel the order if it has not yet been executed.
7.  **Expired**

    Specifically for Limit Order, this state is reached when an order remains unfulfilled by the time the underlying bond reaches its maturity in the order book. After an order expires, any funds that were allocated but not used for the trade are returned to your collateral vault.

A unique aspect of our order lifecycle is the occurrence of combined states, particularly for orders that still need to be fully executed. These include states such as 'Partially Filled & Cancelled' or 'Partially Filled & Blocked', which serve as final designations for an order. Such combined states are crucial for understanding the nuanced outcomes of your trading actions, indicating that an order has been initiated but not completed due to specific conditions and, subsequently, the action is taken (canceled, blocked, etc.) as a resolution.

{% hint style="info" %}
For detailed examples, please take a look at the next section.
{% endhint %}
