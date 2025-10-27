---
description: Understanding how new markets are introduced and retired in the Fixed-Rate Lending Protocol
icon: 🗓️
---

# 🗓️ New Market Listing and Delisting

## Overview

The Fixed-Rate Lending Protocol maintains a dynamic marketplace by carefully managing the introduction of new markets and the retirement of existing ones. Secured Finance aims to provide a diverse range of loan assets to its users while ensuring orderly transitions. This page outlines the processes for both listing new assets and delisting existing ones.

## What You'll Learn

- How new markets are introduced using the Itayose method
- How pre-open orders facilitate fair price discovery
- How orderbooks expand over time for newly listed assets
- How assets are delisted in an orderly fashion
- How loan expiry and redemption work during the delisting process

## Key Components

- [**Itayose Method**](itayose-fair-price-discovery.md): The fair price discovery mechanism used when listing new markets
- **Pre-Open Orders**: The process for placing orders before a market officially opens
- **Orderbook Expansion**: How orderbooks grow over time for newly listed assets
- **Delisting Process**: The orderly retirement of markets

## Listing Process

### Itayose Method

The Itayose method is used for fair price discovery when listing new markets. For more details, see the [Itayose Fair Price Discovery](itayose-fair-price-discovery.md) page.

### Pre-Open Orders

Seven days before the launch of new tenor periods for a newly listed asset, users can place pre-open 'limit orders' on one side of the orderbook. The orderbook is frozen one hour before the market opens, preventing any further actions like placing, amending, or canceling orders.

### Orderbook Expansion

Initially, four orderbooks are opened, representing approximately a 1-year duration. Every week, an additional 3-month orderbook is added, eventually expanding to eight orderbooks to cover a 2-year duration, aligning with other assets on the platform.

## Delisting Process

### Auto-Rolling Cessation

The first step in the delisting process is to stop the [Auto-Rolling](../auto-rolling/) feature for the asset in question. This means that matured loans will not be automatically reinvested into the nearest 3-month bucket.

### Loan Expiry

Loans for the delisted asset will be allowed to expire naturally, without any forced liquidation or closure.

### Repayment and Liquidation

After the loan's maturity, borrowers have a one-week window to repay their debt. Failure to do so will result in the liquidation of the borrower's collateral, ensuring lenders can recover their funds and maintain protocol stability.

### Asset Redemption

Finally, after the 7-day repayment period, lenders can redeem their entire asset along with the accrued interest.&#x20;

{% hint style="info" %}
**Trading will still be available for those who wish to unwind or clean up their positions even under the delisting process.**
{% endhint %}

By following these procedures, Secured Finance ensures a smooth transition for both listing and delisting assets, maintaining the integrity and stability of the marketplace.

## Related Resources

- [Market Dynamics](../README.md)
- [Auto-Rolling](../auto-rolling/README.md)
- [Itayose Fair Price Discovery](itayose-fair-price-discovery.md)
