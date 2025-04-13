---
description: How to calculate the Circuit Breaker Price Limit
---

# 🛑 Price Range Limits

Our trading platform incorporates a circuit breaker mechanism to regulate price fluctuations within a single block. This feature is applicable to both 'market orders' and 'limit orders,' and operates to ensure that orders are executed within acceptable price ranges. The primary objective of the circuit breaker is to mitigate extreme volatility and maintain equilibrium in our Zero Coupon bond market.

### Circuit Breaker Calculation

*   **Limitation on Downward Price Movement:**

    The platform restricts the downward price movement to 5% from the Moving Average of the most recent 5 Reliable Block Prices.
*   **Limitation on Upward Price Movement:**

    Conversely, upward price movement is capped at 10% from the Moving Average of the last 3 Reliable Block Prices.
*   **Minimum Price Fluctuation:**

    The market is permitted to move a minimum of 2.00 for downside and 7.00 for topside.

#### Case Study for Practical Understanding

Consider a situation where the last 5 reliable Block Prices are 80.60, 80.40, 80.30, 80.10, and the most recent is 79.60.

* **Downward Price Limit:**

Moving Average of the most recent 5 reliable block prices is&#x20;

$$
(80.60+80.40+80.30+80.10+79.60)/5 = 80.20
$$

Since movement is limited to 5% to downside, the lowest bound will be&#x20;

$$
80.10 * 0.95 = 76.19
$$

No orders lower than 76.19 will be executed during the next block.



* **Upward Price Limit:**

Moving Average of the most recent 3 reliable block prices is&#x20;

$$
(80.30+80.10+79.60)/3 = 80.00
$$

As topside can move up to 10%, the upper limit will be&#x20;

$$
80.00*1.10 = 88.00
$$

{% hint style="info" %}
Due to the inherent characteristics of Zero-Coupon Bonds—which begin trading at a significant discount and mature at par (100 on our platform)—there should be tighter restrictions on downward movements.
{% endhint %}



*   **Exceptional Case: Minimum Movement:**

    For instance, if the last 5 reliable block prices were 20.00, 18.00, 16.00, 14.00, and 12.00, the Moving Average would be 16.00. Normally, the downward movement would be limited to 15.20 which is 95% of the 16.00. However, the platform allows for a minimum market movement of 1.00, setting the lower limit at 14.00 (= 16.00 - 2.00).

