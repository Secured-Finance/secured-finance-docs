---
description: Understanding the fixed maturity structure used in the Fixed-Rate Lending Protocol
icon: ⏳
---

# ⏳ Fixed Maturity Standard

## Overview

Secured Finance's Loan Market Platform operates on a Fixed Maturity Standard, with up to eight distinct order books each representing a unique time horizon. These range from 3 months to 2 years, with a maturity gap of three months. Each order book exists until its maturity, with the duration shortening day by day. All currencies adhere to the same "Maturity".

## What You'll Learn

- How the Fixed Maturity Standard structures loan terms in the Fixed-Rate Lending Protocol
- How maturity dates are determined for different contract months
- What happens to orderbooks and loan positions at maturity
- How the platform maintains a consistent set of maturity options
- How Auto-Rolling works to reinvest matured positions

## How It Works

The Fixed Maturity Standard provides a structured approach to loan terms with eight distinct orderbooks representing different time horizons:

<figure><img src="../../.gitbook/assets/fixedmaturity.gif" alt="" width="563"><figcaption><p>Fixed Maturity Standard of 8 distinct order books ranging from 3 months to 2 years.</p></figcaption></figure>

The maturity of our Loan Market is set on the **last Friday of the contract month** every March, June, September, and December. This convention aligns with the listed future market, providing maximum utility to our users for reference and hedging purposes.

{% hint style="info" %}
For instance, "SEP23" on our order book system refers to the contract month of September 2023, with a maturity ending on the last Friday, 29th September 2023.\
Similarly, "DEC24" would represent the contract month of December 2024 within the order book with a maturity of 27th December 2024.
{% endhint %}

To keep the orderbooks current, at Maturity, we will deactivate the orderbook that is expiring each quarter and start a new orderbook with the Itayose process. This new orderbook is added to the farthest term, currently the 2-year order book. For more details, please refer to the 'Orderbook Life Cycle' section.

{% hint style="info" %}
What happens to your loan position?

No worries. Matured Loan position will be reinvested through our platform using our [Auto-Rolling](../../advanced-topics/market-dynamics/auto-rolling/README.md) feature.
{% endhint %}

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Number of Orderbooks | Total number of active orderbooks at any time | 8 |
| Maturity Range | Time range covered by the orderbooks | 3 months to 2 years |
| Maturity Gap | Time between consecutive maturities | 3 months |
| Maturity Date | When loans in an orderbook mature | Last Friday of Mar/Jun/Sep/Dec |
| Contract Naming | How contracts are named in the system | MMM+YY (e.g., SEP23, DEC24) |

## Related Resources

- [Zero-Coupon Standard](zero-coupon-bonds.md)
- [Orderbook Mechanics](../order-book-system.md)
- [Auto-Rolling](../../advanced-topics/market-dynamics/auto-rolling/README.md)
- [New Market Listing and Delisting](../../advanced-topics/market-dynamics/new-market-listing-and-delisting/README.md)
