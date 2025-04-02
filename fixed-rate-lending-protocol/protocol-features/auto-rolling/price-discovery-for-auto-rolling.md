---
description: Fair Pricing in Auto-Rolling
---

# 💰 Price Discovery for Auto-Rolling

The auto-rolling price discovery mechanism is a critical component of Secured Finance's platform. It ensures that the pricing for the quarterly roll is calculated accurately and fairly, preventing potential price manipulation. This mechanism is designed to adapt to varying market conditions, ranging from normal and liquid conditions to less liquid or extreme situations with no liquidity.

The mechanism operates in three stages, each corresponding to a different market condition:

## **Normal and Liquid Condition**

In a normal and liquid market condition, we observe the transactions that occur within the 6-hour window before maturity. The roll price is calculated based on the volume-weighted average price of these transactions. This method ensures that the roll price accurately reflects the market conditions and transaction volumes during this period.

## **Less Liquid Condition**

In a less liquid market condition, where no transactions occur during the 6-hour window before maturity, we set the roll price based on the '[Mark Price](../../protocol-security-and-safety/mark-to-market.md)'. This price is adjusted for duration to ensure that it accurately reflects the time value of the financial instrument.

## **Extreme Condition**

In an extreme market condition, where no transactions have occurred for the last 3 months, we use the price of the previous roll. This method ensures that the roll price is still determined based on market data, even in situations of extremely low liquidity.

## **Special Case (Only for the Initial Roll)**&#x20;

In the special case of the initial roll, if no transaction occurs on the 2nd order book until the first roll, we use the opening price of our product launch, adjusted for duration. This method ensures that the initial roll price is still based on market data, even if no transactions have occurred.



This mechanism is part of our commitment to providing a transparent, fair, and efficient platform for our users. By carefully designing our price discovery process, we aim to minimize the potential for price manipulation and ensure that our prices accurately reflect market conditions.

