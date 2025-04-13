---
description: 'Orderbook Rotation: A Continuous Cycle'
---

# 🎡 Market Life Cycle

Under our protocol, there are currently 8 active orderbooks and 1 inactive orderbook operating for each currency. The inactive orderbook undergoes a pre-order period lasting 168 hours (7 days) up to 1 hour before the expiration date of the shortest orderbook. At that point, the Itayose process is initiated, leading to the opening of the orderbook at the specified date. Simultaneously, the orderbook rotation takes place. During this action, if the nearest orderbook has already reached maturity, it will move to the end, and auto-roll will be executed concurrently. The moved orderbook is then recycled and transformed into an inactive, awaiting the next pre-order period.&#x20;

This cycle ensures a seamless and continuous operation of our orderbooks, facilitating efficient utilization of resources and promoting a dynamic and robust lending ecosystem.\


> In this cycle, the number of orderbooks per currency is limited to 9. This means that the increase in order data subject to lazy evaluation can be limited, resulting in lower gas costs.



<figure><img src="../../.gitbook/assets/Market Kife Cycle (1).png" alt=""><figcaption><p>Market Life Cycle</p></figcaption></figure>

