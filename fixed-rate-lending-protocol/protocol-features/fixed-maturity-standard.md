---
description: 3months to 2years loan
---

# ⏳ Fixed Maturity Standard

Secured Finance's Loan Market Platform operates on a Fixed Maturity Standard, with up to eight distinct order books each representing a unique time horizon. These range from 3 months to 2 years, with a maturity gap of three months. Each order book exists until its maturity, with the duration shortening day by day. All currencies adhere to the same "Maturity".

<figure><img src="../../.gitbook/assets/fixedmaturity.gif" alt="" width="563"><figcaption><p>Fixed Maturity Standard of 8 distinct order books ranging from 3 months to 2 years.</p></figcaption></figure>

## When is the Maturity?

The maturity of our Loan Market is set on the **last Friday of the contract month** every March, June, September, and December. This convention aligns with the listed future market, providing maximum utility to our users for reference and hedging purposes.&#x20;

{% hint style="info" %}
For instance, "SEP23" on our order book system refers to the contract month of September 2023, with a maturity ending on the last Friday, 29th September 2023.\
Similarly, "DEC24" would represent the contract month of December 2024 within the order book with a maturity of 27th December 2024.
{% endhint %}

## What happens at Maturity?

To keep the orderbooks current, at Maturity, we will deactivate the orderbook that is expiring each quarter and start a new orderbook with the [Itayose process](broken-reference). This new orderbook is added to the farthest term, currently the 2-year order book. For more details, please refer to the '[Orderbook Life Cycle](../on-chain-orderbook-deep-dive/market-life-cycle.md)' section.

{% hint style="info" %}
What happens to your loan position?&#x20;

No worries. Matured Loan position will be reinvested through our platform using our [Auto-Rolling](auto-rolling/) feature.
{% endhint %}

