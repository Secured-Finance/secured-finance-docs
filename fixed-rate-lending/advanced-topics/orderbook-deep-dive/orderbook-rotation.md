---
description: Understanding how orderbooks rotate and recycle in the Fixed-Rate Lending Protocol
icon: 🎡
---

# 🎡 Orderbook Rotation

## Overview

Orderbook Rotation is a key mechanism in the Secured Finance protocol that ensures continuous market operation and efficient resource utilization. Under our protocol, there are currently 8 active orderbooks and 1 inactive orderbook operating for each currency. This rotation system allows for seamless transitions between orderbooks as they mature, maintaining liquidity and market efficiency.

## What You'll Learn

- How the orderbook rotation cycle works in the Fixed-Rate Lending Protocol
- The timeline and process for orderbook transitions
- How inactive orderbooks are prepared for future use
- How the Itayose process integrates with orderbook rotation
- Why limiting the number of orderbooks helps reduce gas costs

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

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Itayose Fair Price Discovery](../../market-dynamics/new-market-listing-and-delisting/itayose-fair-price-discovery.md)
- [Auto-Rolling](../../market-dynamics/auto-rolling/README.md)
- [Lazy Evaluation](lazy-evaluation.md)
