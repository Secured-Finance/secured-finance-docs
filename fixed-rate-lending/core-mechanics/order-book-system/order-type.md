---
description: Understanding the different order types available in the Fixed-Rate Lending Protocol
icon: 🆎
---

# 🆎 Order Type

## Overview

Secured Finance's Loan Market Platform supports two primary types of orders: limit orders and market orders. These order types provide users with flexibility and control over their trading strategies in the Fixed-Rate Lending Protocol.

## What You'll Learn

- The difference between limit orders and market orders
- How overlapping limit orders are executed
- The role of market makers and market takers in the orderbook
- How each order type affects market liquidity
- When to use each type of order for different trading strategies

## How It Works

### Limit Orders

A limit order is an order to buy or sell a zero-coupon bond at a specific price or better. This type of order allows users to specify the maximum price at which they are willing to buy or the minimum price at which they are willing to sell. 

If the market doesn't reach these prices, the limit order will not be executed. If the market already exists at executable prices (**overlapping limit orders**), such orders will be executed immediately, and non-overlapping orders will remain as open. 

This ensures that users can control the price points at which they enter or exit their positions. By placing limit orders, users effectively act as market makers, contributing to the liquidity and depth of the market.

### Market Orders

A market order is an order to buy or sell a zero-coupon bond immediately at the best available current price. Market orders are typically executed quickly unless the market is exceptionally volatile. 

While market orders do not guarantee a specific price, they ensure the order will be executed. By placing market orders, users effectively act as market takers, accepting the prices currently offered in the market without contributing to the liquidity.

By offering these two types of orders, Secured Finance's Loan Market Platform caters to both users who prioritize price control (limit orders) and those who prioritize quick execution (market orders).

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Order Types | Types of orders supported by the platform | Limit, Market |
| Limit Order Execution | When limit orders are executed | When market price reaches or exceeds the limit price |
| Market Order Execution | When market orders are executed | Immediately at best available price |
| Order Sides | Sides of the orderbook | Borrow (Sell), Lend (Buy) |
| Maker/Taker Role | Role of users based on order type | Limit orders = Makers, Market orders = Takers |

## Related Resources

- [Orderbook Mechanics](../order-book-system.md)
- [Order Life Cycle](order-life-cycle/case-study-order-status-and-transition.md)
- [Zero-Coupon Bonds](../standardization/zero-coupon-bonds.md)
- [Fixed Maturity](../standardization/fixed-maturity.md)
