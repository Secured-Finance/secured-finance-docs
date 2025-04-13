---
description: How to Build Gas-efficient Orderbook On-chain
---

# ⛓️ On-Chain Orderbook Deep Dive

In traditional orderbook systems, achieving a full on-chain implementation is considered challenging due to the significant amount of data reference and updates, which can lead to high [gas costs](../../resources/knowledge-base/gas-cost.md). However, **Secured Finance has successfully implemented an on-chain orderbook system.**

Particularly, gas-intensive processes such as creating open orders, executing market orders, and auto-rolling result in increasing gas costs proportional to the data volume, according to Solidity's characteristics. In some cases, these processes may even approach Ethereum's block gas limit, potentially causing execution issues.



### The key points of Gas cost for On-chain orderbook:

* Creating open orders incurs increasing [gas costs](../../resources/knowledge-base/gas-cost.md) as the data volume on the orderbook grows.
* Executing [market orders](../platform-navigation/trading/order-type.md) results in escalating gas costs proportional to the number of matched open orders, potentially leading to execution challenges in certain cases.
* [Auto-rolling](../protocol-features/auto-rolling/) faces mounting gas costs proportional to the number of positions subject to auto-rolling, potentially leading to execution challenges in certain scenarios.

These challenges prompted Secured Finance to address them effectively and enable a practical gas cost for the full on-chain orderbook system. To achieve this, we introduced red-black trees, lazy evaluation, and the concept of Genesis Value. These solutions ensure the smooth operation of the on-chain orderbook system, optimizing gas costs and enhancing the overall efficiency and performance of the platform.
