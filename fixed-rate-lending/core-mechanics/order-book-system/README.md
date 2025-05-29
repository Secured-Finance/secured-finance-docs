---
description: Understanding the on-chain orderbook system that powers the Fixed-Rate Lending Protocol
icon: 🧩
---

# 🧩 Orderbook Mechanics

## Overview

Secured Finance's Loan Market Platform incorporates an on-chain orderbook system, a pioneering application in the DeFi space. This system facilitates the trading of [Zero-Coupon bonds](../standardization/zero-coupon-bonds.md) with a specific maturity date.

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

The on-chain Orderbook system is often perceived as inefficient due to high gas costs. As a result, many DeFi projects rely on the liquidity pool system (LP) which is a great financial innovation for gathering liquidity. However, the interest rate provided by the pool lacks composability and transparency. Secured Finance has successfully deployed an on-chain orderbook system using the 'lazy evaluation' method, which significantly reduces gas costs. Learn more details at '[Full On-Chain Orderbook system](../../advanced-topics/orderbook-deep-dive/)' at technical overview.
{% endhint %}

## Examples

### Example 1: Placing a Lend Order

A user wants to lend 1,000 USDC for a 3-month term at a 5% APR:

1. They navigate to the lending interface and select the 3-month maturity market
2. They choose to place a limit order to buy a Zero-Coupon bond
3. For a 5% APR on a 3-month term, they set their price at approximately 98.75
   (calculated as: 100 / (1 + 0.05 × 0.25) = 98.75)
4. They specify the amount as 1,000 USDC
5. When the order is filled, they receive a Zero-Coupon bond that will be worth 1,000 USDC at maturity
6. At maturity, they automatically receive 1,000 USDC, earning approximately 12.5 USDC in interest

### Example 2: Placing a Borrow Order

A borrower needs 5,000 USDC for 6 months and is willing to pay up to 6% APR:

1. After depositing sufficient collateral, they navigate to the borrowing interface
2. They select the 6-month maturity market
3. They choose to place a market order to sell a Zero-Coupon bond
4. For a 6% APR on a 6-month term, the price would be approximately 97.09
   (calculated as: 100 / (1 + 0.06 × 0.5) = 97.09)
5. They specify the amount as 5,000 USDC
6. When the order is filled, they receive approximately 4,854.5 USDC upfront
7. At maturity, they will need to repay 5,000 USDC

## Common Questions

### How does the orderbook match orders?

The orderbook matches orders based on price-time priority. The highest buy (lend) orders are matched with the lowest sell (borrow) orders. If multiple orders exist at the same price, they are matched in the order they were placed (first come, first served).

### What happens if my order is not filled immediately?

If your order is not filled immediately, it remains in the orderbook until it is either filled, canceled by you, or expires (if you set an expiration time). You can monitor the status of your orders in the "Open Orders" section of the platform.

### Can I cancel an order after placing it?

Yes, you can cancel any unfilled or partially filled order at any time. Once an order is filled, however, it becomes a position and cannot be canceled. You would need to close the position by taking an opposite position.

### What's the difference between market and limit orders?

A market order is executed immediately at the best available price in the orderbook. A limit order is only executed at the specified price or better. Market orders provide immediate execution but may have price slippage, while limit orders give you price control but may not be filled immediately or at all.

### How is the APR calculated from bond prices?

For bonds with maturity less than 1 year:
APR = (100/BondPrice - 1) × (365/DaysToMaturity)

For example, a 3-month bond priced at 98.75 would have an APR of approximately 5%:
(100/98.75 - 1) × (365/90) ≈ 0.05 or 5%

## Related Resources

- [Order Types](order-type.md)
- [Order Life Cycle](order-life-cycle/case-study-order-status-and-transition.md)
- [Zero-Coupon Bonds](../standardization/zero-coupon-bonds.md)
- [Orderbook Deep Dive](../../advanced-topics/orderbook-deep-dive/README.md)
