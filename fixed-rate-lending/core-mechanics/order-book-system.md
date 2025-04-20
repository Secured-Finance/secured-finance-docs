---
description: Understanding the on-chain orderbook system that powers the Fixed-Rate Lending Protocol
icon: 🧩
---

# 🧩 Orderbook Mechanics

## Overview

Secured Finance's Loan Market Platform incorporates an on-chain orderbook system, a pioneering application in the DeFi space. This system facilitates the trading of [Zero-Coupon bonds](standardization/zero-coupon-bonds.md) with a specific maturity date.

## What You'll Learn

- What an orderbook is and how it functions in the Fixed-Rate Lending Protocol
- The difference between borrow orders and lend orders
- How Zero-Coupon bonds are traded on the platform
- Why on-chain orderbooks are challenging to implement in DeFi
- How Secured Finance overcomes gas cost challenges with its orderbook implementation

## How It Works

An orderbook is an electronic list of buy and sell orders for Zero-Coupon bonds, organized by price level. It enhances transparency by providing visualized information on price, availability, depth of trade, and more.

A borrow order refers to an order to borrow crypto assets, equivalent to selling a bond on our platform. After pledging sufficient collateral, you can place a sell order, selling a Zero-Coupon bond and receiving the equivalent cash upfront. You then owe the obligation to repay the money with interest at maturity.

A lend order is an order to lend, equivalent to buying a bond. You buy a Zero-Coupon bond at a discount, which will be redeemable at par at expiration.

A Zero-Coupon bond is a debt security that doesn't pay interest (coupons) but is traded at a deep discount, rendering profit at maturity when the bond is redeemed for its full face value. On our platform, bonds will be redeemable at 100.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Bond Par Value | The value at which bonds are redeemed at maturity | 100 |
| Order Types | Types of orders supported by the orderbook | Market, Limit |
| Order Sides | Sides of the orderbook | Borrow (Sell), Lend (Buy) |
| Price Precision | Decimal precision for bond prices | 2 decimal places |
| Minimum Order Size | Smallest order that can be placed | Varies by asset |

{% hint style="info" %}
**Why is On-Chain Orderbook so difficult?**

The on-chain Orderbook system is often perceived as inefficient due to high gas costs. As a result, many DeFi projects rely on the liquidity pool system (LP) which is a great financial innovation for gathering liquidity. However, the interest rate provided by the pool lacks composability and transparency. Secured Finance has successfully deployed an on-chain orderbook system using the 'lazy evaluation' method, which significantly reduces gas costs. Learn more details at '[Full On-Chain Orderbook system](../advanced-topics/orderbook-deep-dive/)' at technical overview.
{% endhint %}

## Related Resources

- [Order Types](order-book-system/order-type.md)
- [Order Life Cycle](order-book-system/order-life-cycle/case-study-order-status-and-transition.md)
- [Zero-Coupon Bonds](standardization/zero-coupon-bonds.md)
- [Orderbook Deep Dive](../advanced-topics/orderbook-deep-dive/README.md)
