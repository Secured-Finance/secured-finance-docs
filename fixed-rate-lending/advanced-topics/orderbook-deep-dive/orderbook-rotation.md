---
description: Understanding how orderbooks rotate and recycle in the Fixed-Rate Lending Protocol
icon: 🎡
---

# 🎡 Orderbook Rotation

## Overview

Orderbook Rotation is a key mechanism in the Secured Finance protocol that ensures continuous market operation and efficient resource utilization. Under our protocol, there are currently 8 active orderbooks and 1 inactive orderbook operating for each currency. This rotation system allows for seamless transitions between orderbooks as they mature, maintaining liquidity and market efficiency.

## How It Works

The orderbook rotation process follows a specific cycle that ensures continuous market operation while optimizing for efficiency.

### Orderbook Lifecycle

The inactive orderbook undergoes a pre-order period lasting 168 hours (7 days) up to 1 hour before the expiration date of the shortest orderbook. At that point, the Itayose process is initiated, leading to the opening of the orderbook at the specified date. Simultaneously, the orderbook rotation takes place. 

During this action, if the nearest orderbook has already reached maturity, it will move to the end, and auto-roll will be executed concurrently. The moved orderbook is then recycled and transformed into an inactive, awaiting the next pre-order period.

This cycle ensures a seamless and continuous operation of our orderbooks, facilitating efficient utilization of resources and promoting a dynamic and robust lending ecosystem.

> In this cycle, the number of orderbooks per currency is limited to 9. This means that the increase in order data subject to lazy evaluation can be limited, resulting in lower gas costs.

<figure><img src="../../../.gitbook/assets/Market Kife Cycle (1).png" alt=""><figcaption><p>Market Life Cycle</p></figcaption></figure>

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Active Orderbooks | Number of active orderbooks per currency | 8 |
| Inactive Orderbooks | Number of inactive orderbooks per currency | 1 |
| Pre-Order Period | Duration before new orderbook opens | 168 hours (7 days) |
| Orderbook Freeze | Time before opening when orderbook is frozen | 1 hour |
| Total Orderbooks | Maximum number of orderbooks per currency | 9 |
| Rotation Trigger | Event that initiates orderbook rotation | Maturity of shortest orderbook |
| Maturity Spacing | Typical time between consecutive maturities | 3 months |
| Rotation Frequency | How often orderbook rotation typically occurs | Every 3 months |

## Examples

### Example 1: Complete Orderbook Rotation Cycle

Let's follow a complete rotation cycle for ETH orderbooks:

1. **Initial State**: 8 active orderbooks (maturities: Mar 2024, Jun 2024, Sep 2024, Dec 2024, Mar 2025, Jun 2025, Sep 2025, Dec 2025) and 1 inactive orderbook (future Mar 2026)
   
2. **Pre-Order Period**: 7 days before Mar 2024 maturity, the inactive Mar 2026 orderbook enters pre-order period
   - Users can place pre-orders for the Mar 2026 market
   - These orders will be matched during the Itayose process
   
3. **Maturity and Rotation**: When Mar 2024 orderbook matures:
   - Mar 2024 orderbook is moved to the end of the queue and becomes inactive
   - Mar 2026 orderbook becomes active after Itayose process completes
   - Auto-roll executes for positions in the Mar 2024 orderbook
   
4. **New State**: 8 active orderbooks (Jun 2024, Sep 2024, Dec 2024, Mar 2025, Jun 2025, Sep 2025, Dec 2025, Mar 2026) and 1 inactive orderbook (recycled Mar 2024, which will become Jun 2026)

### Example 2: Pre-Order Placement and Itayose

A trader wants to participate in the pre-order period for a new orderbook:

1. The trader sees that the Sep 2025 orderbook will be opening in 5 days
2. They place a pre-order to lend 10 ETH at a 5% APR
3. Other traders place various pre-orders at different rates
4. One hour before the orderbook opens, the pre-order period ends
5. The Itayose process runs, finding the equilibrium price where supply meets demand
6. The orderbook opens with the fair price determined by Itayose
7. The trader's order is filled at the fair price (which may differ from their requested 5%)

### Example 3: Gas Optimization Through Limited Orderbooks

Consider the impact of limiting orderbooks to 9 per currency:

1. Without the limit: If we had 20 orderbooks per currency, each new order would potentially need to check 20 different price points
2. With the 9 orderbook limit: Each new order only needs to check a maximum of 9 price points
3. Result: Gas costs for order placement are reduced by more than 50%
4. Additionally, the lazy evaluation process has fewer data points to process
5. This optimization is especially important during high network congestion periods

## FAQ

### Why limit the number of orderbooks to 9 per currency?

Limiting the number of orderbooks to 9 per currency (8 active and 1 inactive) serves several important purposes:
1. **Gas Optimization**: Fewer orderbooks means less data to process during order placement and matching, resulting in lower gas costs
2. **Liquidity Concentration**: Concentrating trading in fewer markets increases liquidity depth in each market
3. **Simplified User Experience**: Users can more easily understand and navigate a limited number of maturity options
4. **Efficient Lazy Evaluation**: The lazy evaluation process becomes more efficient with fewer data points to process
5. **Predictable Market Cycle**: Users can anticipate when new markets will open and old ones will close

### How does the pre-order period benefit the protocol?

The pre-order period provides several benefits:
1. **Price Discovery**: It allows for fair price discovery through the Itayose process before the market officially opens
2. **Liquidity Bootstrapping**: New markets start with existing liquidity rather than empty orderbooks
3. **Reduced Slippage**: Initial trades face less slippage due to pre-established liquidity
4. **Market Signals**: Pre-orders provide signals about market sentiment for the new maturity
5. **Smooth Transitions**: It ensures a smooth transition between maturing markets and new ones

### What happens to my positions when an orderbook matures?

When an orderbook reaches maturity, several options are available for your positions:
1. **Auto-Roll**: If enabled, your positions will automatically roll over to a suitable maturity at the prevailing market rate
2. **Settlement**: You can choose to settle your position and receive/pay the underlying asset
3. **Tokenization**: You can tokenize your lending position as an ERC20 token before maturity
4. **Manual Roll**: You can manually roll your position to a specific maturity of your choice

### How is the Itayose price determined for new orderbooks?

The Itayose price is determined through a process that maximizes the matching volume:
1. All pre-orders are collected during the pre-order period
2. The system sorts all buy (borrow) and sell (lend) orders by price
3. It identifies the price point where the maximum number of orders can be matched
4. This becomes the opening price for the new orderbook
5. Orders that can be matched at this price are executed
6. Remaining orders become limit orders in the new active orderbook

### Can I place orders in inactive orderbooks?

Yes, you can place orders in the inactive orderbook during its pre-order period:
1. The pre-order period starts 7 days before the expiration of the shortest active orderbook
2. During this time, you can place orders that will be included in the Itayose process
3. These orders will help establish the opening price for the new orderbook
4. If your pre-order matches during Itayose, it will be executed when the orderbook becomes active
5. If not, it will remain as a limit order in the newly activated orderbook

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Active Orderbooks | Number of active orderbooks per currency | 8 |
| Inactive Orderbooks | Number of inactive orderbooks per currency | 1 |
| Pre-Order Period | Duration before new orderbook opens | 168 hours (7 days) |
| Orderbook Freeze | Time before opening when orderbook is frozen | 1 hour |
| Total Orderbooks | Maximum number of orderbooks per currency | 9 |
| Rotation Trigger | Event that initiates orderbook rotation | Maturity of shortest orderbook |
| Maturity Spacing | Typical time between consecutive maturities | 3 months |
| Rotation Frequency | How often orderbook rotation typically occurs | Every 3 months |

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Itayose Fair Price Discovery](../../market-dynamics/new-market-listing-and-delisting/itayose-fair-price-discovery.md)
- [Auto-Rolling](../../market-dynamics/auto-rolling/README.md)
- [Lazy Evaluation](lazy-evaluation.md)
- [Compound Factor](compound-factor.md)
