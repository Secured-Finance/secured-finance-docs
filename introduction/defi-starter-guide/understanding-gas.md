---
description: Understanding transaction fees in blockchain networks
---

# Understanding Gas

## Overview

Gas is a crucial concept in blockchain networks, particularly on Ethereum and Filecoin, where it represents the computational cost of executing operations. Understanding gas is essential for anyone interacting with decentralized applications, as it directly affects transaction costs and processing times.

## How It Works

When you perform any action on a blockchain network—whether sending tokens, interacting with a smart contract, or deploying a new application—you're requesting network validators (miners or stakers) to process your transaction and include it in a block. Since these operations require computational resources, gas serves as a mechanism to:

1. **Measure Computational Effort**: Each operation has a fixed gas cost based on its complexity
2. **Allocate Network Resources**: During high demand, higher gas prices prioritize urgent transactions
3. **Prevent Network Abuse**: The gas system prevents infinite loops and denial-of-service attacks

On the Filecoin network, which Secured Finance uses, gas works similarly to Ethereum but with some differences in terminology and pricing mechanisms.

### Gas Components

A transaction's gas fee consists of two main components:

- **Gas Limit**: The maximum amount of computational work you're willing to pay for
- **Gas Price**: How much you're willing to pay per unit of gas (typically in gwei, where 1 gwei = 0.000000001 ETH or FIL)

Your total transaction fee is calculated as:

$$
\text{Transaction Fee} = \text{Gas Used} \times \text{Gas Price}
$$

Where Gas Used is the actual amount of gas consumed by your transaction (which cannot exceed your specified Gas Limit).

## Key Parameters

| Parameter | Description | Recommendation |
|-----------|-------------|---------------|
| Gas Limit | Maximum computational work allowed | Set slightly higher than the estimated requirement |
| Gas Price | Cost per unit of gas | Check current network conditions for appropriate pricing |
| Priority Fee | Additional tip to validators | Optional, but helps during network congestion |
| Base Fee | Network-determined minimum fee | Automatically set by the network based on demand |

## Examples

### Simple Token Transfer

A basic token transfer typically requires around 21,000 gas units. If the current gas price is 20 gwei:

$$
\text{Fee} = 21,000 \times 20 \text{ gwei} = 420,000 \text{ gwei} = 0.00042 \text{ ETH/FIL}
$$

### Complex Smart Contract Interaction

Interacting with DeFi protocols like Secured Finance can require significantly more gas, often 100,000-300,000 gas units or more, depending on the complexity of the operation.

## FAQ

**Why do gas prices fluctuate?**
Gas prices vary based on network demand. During periods of high activity, users compete for limited block space by offering higher gas prices.

**What happens if I set my gas limit too low?**
If your gas limit is too low, your transaction will fail when it runs out of gas, but you'll still be charged for the computational resources used up to that point.

**How can I reduce gas costs?**
- Execute transactions during periods of lower network activity
- Use gas price estimator tools to avoid overpaying
- Batch multiple operations into a single transaction when possible
- Consider layer-2 solutions or sidechains for frequent transactions

**Do all blockchains use gas?**
Not all blockchains use the exact gas model, but most have some form of transaction fee mechanism to prevent spam and allocate resources.

## Related Resources

- [Gas Cost](gas-cost.md)
- [Interacting with DApps](interacting-with-dapps.md)
- [Wallet Setup & Management](wallet-setup-and-management.md)
