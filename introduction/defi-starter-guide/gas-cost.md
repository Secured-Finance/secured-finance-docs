---
description: Understanding transaction fees in blockchain networks
---

# Gas Cost

## Overview

Gas costs are the fees paid to execute transactions on blockchain networks like Ethereum and Filecoin. These fees compensate validators for the computational resources required to process and verify transactions. Understanding gas costs is essential for efficiently interacting with decentralized applications and managing your transaction expenses.

## How It Works

When you submit a transaction to a blockchain network, you're requesting validators (miners or stakers) to include your transaction in a block. Since blockchain networks have limited capacity, gas fees serve as a market mechanism to prioritize transactions during periods of high demand.

The gas fee system consists of several components:

1. **Gas Units**: Each operation in a transaction (transfers, smart contract interactions, etc.) requires a specific amount of computational work measured in gas units
2. **Gas Price**: The amount you're willing to pay per unit of gas, typically denominated in a small fraction of the network's native token (gwei for Ethereum, attoFIL for Filecoin)
3. **Gas Limit**: The maximum amount of gas you're willing to spend on a transaction

Your total transaction fee is calculated as:

$$
\text{Transaction Fee} = \text{Gas Used} \times \text{Gas Price}
$$

Where Gas Used is the actual computational resources consumed (which cannot exceed your specified Gas Limit).

### Fee Market Mechanisms

Different blockchain networks implement various fee mechanisms:

- **Ethereum's EIP-1559**: Includes a base fee that gets burned and a priority fee (tip) that goes to validators
- **Filecoin's Gas Model**: Uses a similar approach with base fees adjusted based on network congestion

## Key Parameters

| Parameter | Description | Recommendation |
|-----------|-------------|---------------|
| Gas Limit | Maximum computational units allowed | Set 10-20% higher than estimated requirement |
| Gas Price | Cost per unit of gas | Check current network conditions |
| Priority Fee | Optional tip to validators | Higher during network congestion |
| Max Fee | Maximum total fee willing to pay | Set based on urgency of transaction |

## Examples

### Simple Token Transfer

A basic token transfer on Ethereum typically requires 21,000 gas units. If the current gas price is 20 gwei:

$$
\text{Fee} = 21,000 \times 20 \text{ gwei} = 420,000 \text{ gwei} = 0.00042 \text{ ETH}
$$

### Complex DeFi Transaction

Interacting with DeFi protocols like Secured Finance can require significantly more gas:

- Approving a token: ~45,000 gas units
- Swapping tokens: ~100,000-200,000 gas units
- Providing liquidity: ~150,000-300,000 gas units

## FAQ

**Why do gas prices fluctuate?**
Gas prices vary based on network demand. During periods of high activity (NFT drops, market volatility), users compete for limited block space by offering higher gas prices.

**What happens if I set my gas limit too low?**
If your gas limit is too low, your transaction will fail when it runs out of gas, but you'll still be charged for the computational resources used up to that point.

**How can I reduce gas costs?**
- Execute transactions during periods of lower network activity
- Use gas price estimator tools to avoid overpaying
- Batch multiple operations into a single transaction when possible
- Consider layer-2 solutions or sidechains for frequent transactions

**Is gas refundable?**
You're only charged for the actual gas used, even if you set a higher gas limit. However, failed transactions still consume gas and incur fees without completing the intended action.

## Related Resources

- [Understanding Gas](understanding-gas.md)
- [Wallet Setup & Management](wallet-setup-and-management.md)
- [Interacting with DApps](interacting-with-dapps.md)
