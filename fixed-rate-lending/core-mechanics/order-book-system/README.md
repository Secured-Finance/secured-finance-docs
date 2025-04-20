---
description: Understanding the on-chain orderbook system that powers the Fixed-Rate Lending Protocol
icon: 📊
---

# 📊 Order Book System

## Overview

Secured Finance's Loan Market Platform incorporates an on-chain orderbook system, a pioneering application in the DeFi space. This system facilitates the trading of [Zero-Coupon bonds](../standardization/zero-coupon-bonds.md) with a specific maturity date, enabling transparent and efficient fixed-rate lending and borrowing.

## What You'll Learn

- How the on-chain orderbook system works
- The different types of orders in the system
- How borrowing and lending are represented as bond trading
- Why on-chain orderbooks are challenging and how Secured Finance solved this
- How orders are matched and executed

## Key Components

- [**Order Types**](order-type.md): The different types of orders available in the system
- [**Order Life Cycle**](order-life-cycle/README.md): How orders progress through the system
- [**Zero-Coupon Bonds**](../standardization/zero-coupon-bonds.md): The standardized representation of lending and borrowing positions

## Key Concepts

### What is an Orderbook?

It is an electronic list of buy and sell orders for Zero-Coupon bonds, organized by price level. It enhances transparency by providing visualized information on price, availability, depth of trade, and more.

### What is a Borrow Order?

It refers to an order to borrow crypto assets, equivalent to selling a bond on our platform. After pledging sufficient collateral, you can place a sell order, selling a Zero-Coupon bond and receiving the equivalent cash upfront. You then owe the obligation to repay the money with interest at maturity.

### What is a Lend Order?

This is an order to lend, equivalent to buying a bond. You buy a Zero-Coupon bond at a discount, which will be redeemable at par at expiration.

### What is a Zero-Coupon Bond?

A Zero-Coupon bond is a debt security that doesn't pay interest (coupons) but is traded at a deep discount, rendering profit at maturity when the bond is redeemed for its full face value. On our platform, bonds will be redeemable at 100.

### Why is On-Chain Orderbook so difficult?

The on-chain Orderbook system is often perceived as inefficient due to high gas costs. As a result, many DeFi projects rely on the liquidity pool system (LP) which is a great financial innovation for gathering liquidity. However, the interest rate provided by the pool lacks composability and transparency. Secured Finance has successfully deployed an on-chain orderbook system using the 'lazy evaluation' method, which significantly reduces gas costs. Learn more details at '[Full On-Chain Orderbook system](../../advanced-topics/orderbook-deep-dive/README.md)' at technical overview.

## Related Resources

- [Standardization](../standardization/README.md)
- [Collateralization](../collateralization.md)
- [Orderbook Deep Dive](../../advanced-topics/orderbook-deep-dive/README.md)

*(Note: This content was restored from the previous location: `fixed-rate-lending/protocol-features/on-chain-orderbook-system.md`)*
