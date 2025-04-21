---
description: A guide to the digital assets available for lending and borrowing on the Fixed-Rate Lending Protocol
icon: 💲
---

# 💲 Supported Currencies

## Prerequisites

- Basic understanding of digital assets and cryptocurrencies
- Access to the Secured Finance platform
- Familiarity with blockchain networks (helpful but not required)

## Overview

Secured Finance supports a carefully selected range of digital assets for lending and borrowing, tailored to meet the needs of diverse users across multiple blockchains. This guide provides an overview of the assets currently supported on our platform and their unique characteristics.

## Step 1: Understanding Available Assets

Secured Finance supports five major digital assets for lending and borrowing:

1. **Filecoin (FIL)**
   - Native token of the decentralized storage network Filecoin
   - Available on: Filecoin (FVM), Ethereum
   - Used for payments and transactions within the Filecoin ecosystem

2. **USD for Filecoin Community (USDFC)**
   - A stablecoin pegged to the US dollar for the Filecoin Community
   - Available exclusively on the FVM for lending/borrowing and collateral
   - Provides price stability for Filecoin ecosystem participants

3. **Ethereum (ETH)**
   - Native token of Ethereum, powering smart contracts and dApps
   - Available on: Ethereum, Arbitrum
   - Core DeFi asset with widespread adoption

4. **USD Coin (USDC)**
   - A stablecoin pegged to the US dollar
   - Available on: Ethereum, Arbitrum
   - Offers price stability for lending and borrowing

5. **Wrapped Bitcoin (WBTC)**
   - Wrapped version of Bitcoin for use within the Ethereum ecosystem
   - Available on: Ethereum, Arbitrum
   - Brings Bitcoin's value and liquidity to DeFi protocols

## Step 2: Checking Asset Availability by Blockchain

Different assets are available on different blockchains. Use this table to determine which assets you can use on each network:

| **Blockchain**     | **Available Assets**                      |
| ------------------ | ---------------------------------------------- |
| **Ethereum**       | WBTC, ETH, USDC, FIL (as axlFIL)               |
| **Arbitrum**       | WBTC, ETH, USDC                                |
| **Filecoin (FVM)** | FIL, iFIL and pFIL (Liquid Staking Tokens), USDFC |

## Step 3: Understanding Collateral Options

Not all assets can be used as collateral. Here's what you can use as collateral on each blockchain:

| **Blockchain**     | **Collateral Currencies**                      |
| ------------------ | ---------------------------------------------- |
| **Ethereum**       | WBTC, ETH, USDC                                |
| **Arbitrum**       | WBTC, ETH, USDC                                |
| **Filecoin (FVM)** | FIL, iFIL and pFIL (Liquid Staking Tokens), USDFC |

## Step 4: Selecting the Right Asset for Your Needs

When choosing which asset to lend or borrow, consider:

1. **Purpose**
   - For stable returns: Consider stablecoins like USDC or USDFC
   - For potential appreciation: Consider native tokens like ETH or FIL
   - For Bitcoin exposure: Consider WBTC

2. **Blockchain**
   - Choose assets available on your preferred blockchain
   - Consider gas fees and transaction speeds of each network
   - Note network-specific features (e.g., liquid staking tokens on FVM)

3. **Risk Profile**
   - Stablecoins typically offer lower but more predictable returns
   - Native tokens may offer higher returns but with more volatility
   - Consider collateral requirements when borrowing

## Step 5: Using Liquid Staking Tokens

For Filecoin users, liquid staking tokens offer additional options:

1. **iFIL**
   - Available on: Filecoin (FVM)
   - Represents staked FIL that continues earning staking rewards
   - Can be used as collateral while still earning staking yield

2. **pFIL**
   - Available on: Filecoin (FVM)
   - Another liquid staking token for FIL
   - Combines staking rewards with lending/borrowing capabilities

## Next Steps

After understanding the supported currencies, you might want to:

- [Start lending assets](../../lending-assets.md) in your preferred currency
- [Borrow assets](../../borrowing-assets.md) using your available collateral
- [Explore the trading interface](../trading/README.md) to place orders

## Troubleshooting

### Asset Not Appearing in Wallet

If you don't see an asset in your wallet:
- Ensure you're connected to the correct blockchain network
- Check that you have the correct token contract address
- Some assets may require manual addition to your wallet
- Verify that the asset is supported on your current network

### Cross-Chain Asset Access

If you need to use assets across different blockchains:
- Use the [Bridge feature](../bridge.md) to transfer assets between networks
- Note that not all assets can be bridged to all networks
- Some assets may have wrapped versions on other networks (e.g., axlFIL on Ethereum)

### Network Sunsetting Notice

{% hint style="warning" %}
We are **sunsetting support** for Avalanche and Polygon zkEVM. These networks and associated assets will no longer be actively supported on Secured Finance Fixed Rate Lending Protocol.
{% endhint %}

If you have assets on sunsetting networks:
- Bridge your assets to supported networks as soon as possible
- Unwind any open positions on these networks
- Monitor announcements for specific sunset timelines
