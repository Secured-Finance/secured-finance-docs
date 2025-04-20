---
description: Understanding the fixed maturity structure used in the Fixed-Rate Lending Protocol
icon: ⏳
---

# ⏳ Fixed Maturity Standard

## Overview

Secured Finance's Loan Market Platform operates on a Fixed Maturity Standard, with up to eight distinct order books each representing a unique time horizon. These range from 3 months to 2 years, with a maturity gap of three months. Each order book exists until its maturity, with the duration shortening day by day. All currencies adhere to the same "Maturity".



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

## Examples

### Example 1: Lending Across Multiple Maturities

A user wants to diversify their lending strategy across different time horizons:

1. They deposit 3,000 USDC into the platform
2. They allocate 1,000 USDC to the 3-month maturity (JUN24)
3. They allocate 1,000 USDC to the 6-month maturity (SEP24)
4. They allocate 1,000 USDC to the 9-month maturity (DEC24)
5. This creates a "ladder" strategy that provides liquidity at regular intervals
6. When the JUN24 position matures, it will auto-roll to the new 2-year maturity (JUN26)

### Example 2: Navigating Orderbook Transitions

A borrower has an active loan in the SEP23 orderbook approaching maturity:

1. As the maturity date (September 29, 2023) approaches, they receive notifications
2. On maturity day, their position is automatically handled by the Auto-Rolling feature
3. The SEP23 orderbook is deactivated and a new orderbook (SEP25) is created
4. Their position is rolled into the next available maturity with similar duration
5. The borrower can view their new position details in the platform interface

## FAQ

### What happens if I want to exit before maturity?

If you want to exit your position before maturity, you can take an opposite position in the same maturity orderbook. For example, if you initially lent in the DEC24 orderbook, you can borrow in the same DEC24 orderbook to close your position. Market conditions at the time will determine whether you realize a gain or loss.

### How are new orderbooks created?

New orderbooks are created through the Itayose process, which is a price discovery mechanism. When the shortest-term orderbook matures, a new orderbook is created for the longest term (currently 2 years out). This maintains a consistent set of eight active orderbooks at all times.

### Can I choose which maturity my position auto-rolls into?

By default, positions auto-roll according to the protocol's rules, typically into the next available maturity. However, you can manually close your position before maturity and open a new position in your preferred maturity orderbook if you want more control over the rollover process.

### Why use quarterly maturities instead of monthly or weekly?

Quarterly maturities (Mar/Jun/Sep/Dec) align with traditional financial markets and futures contracts, providing better liquidity and price discovery. This standardization also reduces fragmentation of liquidity across too many orderbooks, which could lead to thinner markets and wider spreads.

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
