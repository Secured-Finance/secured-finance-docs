---
description: Market microstructure and the engineering behind the on-chain order book
---

# Advanced Topics

These pages go beyond day-to-day usage into how the protocol's markets operate and how the on-chain order book is engineered. Nothing here is required to lend or borrow — but if you're evaluating the protocol's design, integrating against it, or just curious, this is the good part.

## Market operations

* [**Itayose: Fair Price Discovery**](itayose.md) — the opening auction that prices every new market
* [**Market Listing & Delisting**](market-listing-and-delisting.md) — how assets join and leave the platform

## Safety mechanisms

* [**Circuit Breaker**](circuit-breaker.md) — per-block price limits that blunt manipulation and flash-loan attacks
* [**Base Price Adjustment**](base-price-adjustment.md) — duration-aware minimum collateral requirements
* [**Emergency Global Settlement**](emergency-global-settlement.md) — the last-resort shutdown that returns user funds

## Engineering

* [**Orderbook Deep Dive**](orderbook-deep-dive/README.md) — why a full on-chain order book is hard, and the three techniques that make it economical: [Red-Black Trees](orderbook-deep-dive/red-black-tree.md), [Lazy Evaluation](orderbook-deep-dive/lazy-evaluation.md), and [Genesis Value & Compound Factor](orderbook-deep-dive/genesis-value-and-compound-factor.md)

## Finance background

* [**APR vs APY**](apr-vs-apy.md) — why the protocol quotes APR, and how to compare rates across venues
