---
description: Where the FIL/USD price comes from and what happens when it goes stale
---

# 🔮 Price Oracle

Every collateral ratio in the protocol — and therefore every liquidation and redemption — depends on one number: the FIL/USD price reported by the **PriceFeed** contract. This page explains where that price comes from and how the protocol behaves when it can't get a fresh one.

## The two price sources

| Role | Source | Notes |
| --- | --- | --- |
| Primary | [RedStone](https://redstone.finance/) | Chainlink-compatible FIL/USD price feed; replaced Pyth in 2026 |
| Fallback | [Tellor](https://tellor.io/) | Decentralized oracle network; prices are submitted by an update job operated by Secured Finance, roughly every 12 hours |

One trust assumption worth knowing: while the primary price comes from RedStone's oracle network, the **Tellor fallback submissions currently depend on an update job operated by Secured Finance**. The contracts constrain what a bad price can do (see the sanity checks below), but the fallback path is not independent of the team.

## When the protocol switches sources

The PriceFeed falls back from the primary to Tellor when any of these occur:

* The primary price hasn't been updated for longer than the **oracle timeout (16 hours)**
* The primary call reverts, or returns invalid data or an invalid timestamp
* The price moves more than **50%** between consecutive updates (treated as a glitch unless Tellor confirms it)

Returning to the primary requires the two sources to agree within **5%** — after an incident, the protocol may stay on the fallback for a while even once the primary is healthy again.

## When both sources are stale

If Tellor is also stale, the protocol keeps operating on the **last good price** it recorded — for up to **48 hours**. Past that, price fetches revert and protocol operations that need a price — opening, adjusting, liquidating, redeeming — halt until a fresh price lands on-chain.

For a Trove owner, the practical implication: during an oracle outage the price the protocol uses can lag the real market. A liquidation that "should" have happened may be delayed — and conversely, you cannot assume a market recovery protects you until the on-chain price reflects it.

## Where next

* [Liquidation](liquidation.md) — how the oracle price triggers liquidations
* [Contracts and Security](../deployed-contracts.md) — contract addresses
