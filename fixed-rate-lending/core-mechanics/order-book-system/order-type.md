---
description: Understanding the different order types available in the Fixed-Rate Lending Protocol
icon: 🆎
---

# 🆎 Order Type

## Overview

Secured Finance's Loan Market Platform supports two primary types of orders: limit orders and market orders. These order types provide users with flexibility and control over their trading strategies in the Fixed-Rate Lending Protocol.



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

## Examples

### Example 1: Using a Limit Order to Lend

A user wants to lend 2,000 USDC for 6 months at a minimum 4% APR:

1. They navigate to the lending interface and select the 6-month maturity market
2. For a 4% APR on a 6-month term, they calculate the price as approximately 98.04
   (calculated as: 100 / (1 + 0.04 × 0.5) = 98.04)
3. They place a limit order to buy Zero-Coupon bonds at 98.04
4. The order remains in the orderbook until:
   - A borrower places a market order that matches with this order
   - A borrower places a limit order at 98.04 or lower that matches with this order
   - The user cancels the order
5. If the order is filled, the user pays 1,960.8 USDC (2,000 × 98.04 / 100)
6. At maturity, they receive 2,000 USDC, earning 39.2 USDC in interest

### Example 2: Using a Market Order to Borrow

A borrower needs 5,000 USDC immediately and doesn't want to wait for a limit order to be filled:

1. After depositing sufficient collateral, they navigate to the borrowing interface
2. They select the 3-month maturity market
3. They choose to place a market order to sell Zero-Coupon bonds
4. The current best lending offer in the orderbook is at 99.00
5. Their market order is immediately matched with this offer
6. They receive 4,950 USDC upfront (5,000 × 99.00 / 100)
7. At maturity, they will need to repay 5,000 USDC
8. The effective interest paid is 50 USDC on a loan of 4,950 USDC for 3 months

## Common Questions

### When should I use a limit order versus a market order?

Use a limit order when:
- You want to specify the exact price/rate for your transaction
- You're willing to wait for your order to be filled
- You want to contribute to market liquidity and potentially earn better rates
- You want protection against price slippage in volatile markets

Use a market order when:
- You need immediate execution
- You prioritize speed over getting the best possible rate
- You're satisfied with the current market rates
- You need funds quickly and can't wait for a limit order to fill

### What happens if there's not enough liquidity to fill my market order?

If there's insufficient liquidity to fill your entire market order, the order will be partially filled up to the available liquidity at the best available prices. The unfilled portion will remain as an open market order until more liquidity becomes available or you cancel it.

### Can I modify my limit order after placing it?

No, you cannot modify an existing limit order. If you want to change the price or amount, you'll need to cancel your existing order and place a new one with the updated parameters.

### Do limit orders expire?

By default, limit orders do not expire and will remain in the orderbook until they are either filled or canceled. However, when placing a limit order, you have the option to set an expiration time, after which the order will be automatically canceled if not filled.

### What fees are associated with limit versus market orders?

Both limit and market orders incur protocol fees, but the fee structure may differ:
- Limit orders (makers): Generally have lower fees as they provide liquidity to the market
- Market orders (takers): Generally have higher fees as they consume liquidity from the market

The exact fee structure is subject to change based on protocol governance decisions.

## Related Resources

- [Orderbook Mechanics](../order-book-system.md)
- [Order Life Cycle](order-life-cycle/case-study-order-status-and-transition.md)
- [Zero-Coupon Bonds](../standardization/zero-coupon-bonds.md)
- [Fixed Maturity](../standardization/fixed-maturity.md)
