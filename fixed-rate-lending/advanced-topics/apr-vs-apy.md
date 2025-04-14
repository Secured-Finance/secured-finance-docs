---
description: Annualised Interest Rate
---

# APR vs APY

APR (Annual Percentage Rate) and APY (Annual Percentage Yield) are two common measures of interest rates that are used in the DeFi loan and deposit markets. While they may seem similar, there are key differences between them.

## What is APY?

APY stands for Annual Percentage Yield, which is a measure of the interest earned on a deposit or investment over a year, taking into account the effect of **compounding** interest.

## How about APR?

APR is the interest rate that is charged on a loan or credit card balance. It is the annual rate of interest that is applied to the outstanding balance on the loan, expressed as a percentage. The APR does **not** take **compounding** into account.

## Case Study

Bob lend his 100 USD with a fixed rate of 10% for 6 months. How much do you think he earned after 6 months?

#### APR 10%

<div align="left"><figure><img src="../../.gitbook/assets/image (47).png" alt="" width="349"><figcaption></figcaption></figure></div>

He earns 5% of interest for 6 months and his FV will be 105 or he earns 5 dollars

#### APY 10%

In case this APY is compounded by 6 months, APY 10% and APR 'r' will have a relationship like&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/image (48).png" alt="" width="563"><figcaption></figcaption></figure></div>

Hence his 100 will be 104.88 or he earns 4.88 dollars.

{% hint style="info" %}
The use of APY is widespread in DeFi projects because of the variable nature of their quoted interest, leading to the representation of compounded interest. APY assumes that the current variable rate remains constant for the next 365 days and compounds daily. Moreover, fixed-term projects that depend on variable rates as their underlying interest rate also utilize APY.

However, adhering to the prevailing market conventions, our protocol naturally displays APR rather than APY.
{% endhint %}
