---
description: Understanding transaction fees in blockchain networks
---

# Gas Fees

## Overview

Gas fees are the transaction costs paid to execute operations on blockchain networks like Ethereum and Filecoin. These fees compensate validators (miners or stakers) for the computational resources required to process and verify transactions. Understanding gas is essential for anyone interacting with decentralized applications, as it directly affects transaction costs and determines how quickly your transactions are processed.

## How It Works

When you perform any action on a blockchain network—whether sending tokens, interacting with a smart contract, or deploying a new application—you're requesting network validators to process your transaction and include it in a block. Since blockchain networks have limited capacity, gas fees serve as a market mechanism to:

1. **Measure Computational Effort**: Each operation has a fixed gas cost based on its complexity
2. **Allocate Network Resources**: During high demand, higher gas prices prioritize urgent transactions
3. **Prevent Network Abuse**: The gas system prevents infinite loops and denial-of-service attacks

On the Filecoin network, which Secured Finance uses, gas works similarly to Ethereum but with some differences in terminology and pricing mechanisms.

### Gas Components

The gas fee system consists of several components:

- **Gas Units**: Each operation in a transaction requires a specific amount of computational work measured in gas units
- **Gas Limit**: The maximum amount of computational work you're willing to pay for
- **Gas Price**: How much you're willing to pay per unit of gas (typically in gwei, where 1 gwei = 0.000000001 ETH or attoFIL for Filecoin)

Your total transaction fee is calculated as:

$$
\text{Transaction Fee} = \text{Gas Used} \times \text{Gas Price}
$$

Where Gas Used is the actual amount of gas consumed by your transaction (which cannot exceed your specified Gas Limit).

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
| Base Fee | Network-determined minimum fee | Automatically set by the network based on demand |
| Max Fee | Maximum total fee willing to pay | Set based on urgency of transaction |

## Examples

### Simple Token Transfer

A basic token transfer typically requires around 21,000 gas units. If the current gas price is 20 gwei:

$$
\text{Fee} = 21,000 \times 20 \text{ gwei} = 420,000 \text{ gwei} = 0.00042 \text{ ETH or FIL}
$$

### Complex DeFi Transaction

Interacting with DeFi protocols like Secured Finance can require significantly more gas:

- Approving a token: ~45,000 gas units
- Swapping tokens: ~100,000-200,000 gas units
- Providing liquidity: ~150,000-300,000 gas units

## Common Questions

**Why do gas prices fluctuate?**
Gas prices vary based on network demand. During periods of high activity (NFT drops, market volatility), users compete for limited block space by offering higher gas prices.

**What happens if I set my gas limit too low?**
If your gas limit is too low, your transaction will fail when it runs out of gas, but you'll still be charged for the computational resources used up to that point.

**Where can I check the current gas price?**
You can check current gas prices on various websites like Etherscan.io, Ethgas.watch, or GasNow for Ethereum, and Filfox.info for Filecoin. Many wallets also display current gas prices directly in their interfaces.

**How do I convert gas costs to USD value?**
To calculate the USD value of gas fees:
1. Calculate the fee in the native token: Gas Units × Gas Price = Fee in ETH/FIL
2. Multiply by the current token price: Fee in ETH/FIL × Current Price in USD = Fee in USD
For example, if gas costs 0.002 ETH and ETH is $3,000, the fee would be $6.

**How can I reduce gas costs?**
- Execute transactions during periods of lower network activity
- Use gas price estimator tools to avoid overpaying
- Batch multiple operations into a single transaction when possible
- Consider layer-2 solutions or sidechains for frequent transactions

**Is gas refundable?**
You're only charged for the actual gas used, even if you set a higher gas limit. However, failed transactions still consume gas and incur fees without completing the intended action.

**Do all blockchains use gas?**
Not all blockchains use the exact gas model, but most have some form of transaction fee mechanism to prevent spam and allocate resources.

## Related Resources

- [Wallet Setup & Management](wallet-setup-and-management.md)
- [Interacting with DApps](interacting-with-dapps.md)
- [DeFi vs CeFi](defi-vs-cefi.md)
