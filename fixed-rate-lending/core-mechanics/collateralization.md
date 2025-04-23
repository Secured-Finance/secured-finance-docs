---
description: Understanding how collateral secures loans in the Fixed-Rate Lending Protocol
icon: 🏋️
---

# 🏋️ Collateralization

## Overview

Collateralization is a fundamental mechanism in the Fixed-Rate Lending Protocol that ensures the security and stability of the lending system. By requiring borrowers to deposit assets as collateral, the protocol protects lenders from default risk while enabling borrowers to access liquidity without traditional credit checks.



## How It Works

The collateralization process in the Fixed-Rate Lending Protocol involves users depositing supported assets as collateral before borrowing or trading. The protocol continuously monitors the value of collateral against outstanding loans using real-time price feeds. If the collateralization ratio falls below the required threshold, the position becomes eligible for liquidation to protect the system's solvency.

Each collateral type has specific parameters including minimum collateralization ratios, liquidation thresholds, and accepted currencies. The protocol supports multi-collateral positions, allowing users to diversify their risk across different assets.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Minimum Collateralization Ratio | The minimum ratio of collateral value to loan value required | 110%-150% (varies by asset) |
| Liquidation Threshold | The collateralization ratio at which a position becomes eligible for liquidation | Varies by asset |
| Collateral Factor | The percentage of an asset's value that can be borrowed against | 50%-90% (varies by asset) |
| Price Feed Update Frequency | How often collateral values are updated from oracles | Real-time |
| Supported Collateral Types | Assets accepted as collateral | WBTC, ETH, USDC, FIL, iFIL, pFIL, USDFC (varies by network) |

## What is Collateral?

Collateral is an asset that borrowers pledge to back a loan. It acts as a safety net for lenders, giving them the assurance that borrowers have a strong reason to repay their loans. If a borrower defaults, the lender can seize the collateral to recover the outstanding loan amount. Collateral can take various forms, such as real estate, vehicles, or other valuable assets, but it's a cornerstone of secured loans. It often allows borrowers to enjoy lower interest rates due to reduced lender risk.

### The Dual Role of Collateral in Secured Finance

Collateral serves two main purposes in Secured Finance:

1. **Risk Reduction:** It reduces the risk of loan default. If a borrower's Loan-to-Value (LTV) ratio crosses a certain threshold, or if the collateral's value falls below the loan's required value, the loan becomes eligible for liquidation. This mechanism protects lenders and builds confidence in our platform.
2. **Inclusivity:** It eliminates the need for traditional credit checks, aligning with the DeFi ethos of open and inclusive financial services.

***

## Collateral Currencies

Secured Finance accepts various cryptocurrencies as collateral, tailored to each supported blockchain network to provide users with effective and flexible options.

### Collateral Currencies on Ethereum and Arbitrum

We continue to support these collateral assets on **Ethereum** and **Arbitrum**:

#### **Wrapped Bitcoin (WBTC)**

Represents Bitcoin on Ethereum, allowing BTC holders to tap into Ethereum’s DeFi ecosystem.

#### **Ethereum (ETH)**

Native asset of the Ethereum network, widely used for smart contracts and DeFi applications.

#### **USD Coin (USDC)**

A stablecoin pegged to the US dollar, offering minimal volatility.

### Collateral Currencies on Filecoin Virtual Machine (FVM)

With the launch of the Filecoin Virtual Machine (FVM), Secured Finance now supports different collateral assets unique to this network:

#### **Filecoin (FIL)**

Filecoin is the native cryptocurrency of the Filecoin network, a decentralized storage system aiming to "store humanity's most important information." FIL is used to pay for storage services and incentivize network participants. It can now be used as collateral on Secured Finance within the FVM network.

#### USD for Filecoin Community (USDFC)

[**USDFC** ](../../../../usdfc-stablecoin/overview.md)is a FIL-backed stablecoin minted through a **Collateralized Debt Position (CDP)** approach on the Filecoin Virtual Machine (FVM). By locking FIL as collateral, users can generate USDFC—maintaining a **1:1 peg** to the U.S. dollar—without selling their underlying assets.

#### **iFIL and pFIL (Filecoin Liquid Staking Token)**

iFIL and pFIL are a liquid staking token for Filecoin. It represents staked FIL tokens and provides liquidity to users who stake their FIL. For example, by staking FIL through the [GLIF](https://glif.io/) platform, users receive iFIL tokens, which can be used as collateral on Secured Finance within the FVM network.

{% hint style="success" %}
**How to Obtain iFIL**

To acquire iFIL tokens, follow these steps:

1. **Stake FIL on GLIF**: Visit the GLIF Staking Platform and stake your FIL tokens.
2. **Receive iFIL**: After staking, you will receive an equivalent amount of iFIL tokens.
3. **Use iFIL as Collateral**: Deposit your iFIL tokens into your Secured Finance portfolio on the FVM network to use them as collateral.
{% endhint %}

## Examples

### Example 1: Borrowing with ETH Collateral

A user wants to borrow 1,000 USDC on Ethereum. They would:

1. Deposit 1 ETH as collateral (assuming ETH price is $2,000)
2. This gives them a collateralization ratio of 200% (2,000 / 1,000 × 100%)
3. They can now borrow up to 1,000 USDC while maintaining a safe position
4. If ETH price drops below $1,500, their position would be at risk of liquidation

### Example 2: Using iFIL as Collateral on FVM

A storage provider has 1,000 FIL they want to earn yield on while also accessing liquidity:

1. They stake their 1,000 FIL on GLIF to receive 1,000 iFIL
2. They deposit the 1,000 iFIL as collateral on Secured Finance
3. They can now borrow USDFC while their original FIL continues earning staking rewards
4. This creates a dual yield opportunity: staking rewards plus potential trading gains

## Common Questions

### What happens if my collateral value drops?

If your collateral value drops below the required threshold for your loan, your position becomes eligible for liquidation. The protocol will automatically liquidate a portion of your collateral to repay part of your debt and bring your position back to a safe level. To avoid liquidation, you can either add more collateral or repay part of your loan.

### Can I use multiple types of collateral for a single loan?

Yes, Secured Finance supports multi-collateral positions. You can deposit different types of accepted collateral assets to back your loan, which can help diversify your risk exposure to any single asset's price volatility.

### How often is my collateral value updated?

Collateral values are updated in real-time using oracle price feeds. This ensures that your position's health is always calculated based on the most current market prices.

### What are the minimum collateral requirements?

Minimum collateral requirements vary by asset type and network. Generally, the protocol requires a minimum collateralization ratio of 110%-150% depending on the volatility and liquidity of the collateral asset. Specific requirements for each asset are displayed in the platform interface.

## Future Plans: Expanding Collateral Options

While WBTC, ETH, USDC, FIL, iFIL, pFIL, and USDFC are our current collateral options across supported networks, we continue to explore additional assets that align with our commitment to flexibility, security, and open DeFi principles. Stay tuned for updates on new collateral integrations and chain support as we further evolve the Secured Finance platform.

{% hint style="warning" %}
We are **sunsetting support** for Avalanche and Polygon zkEVM. Collateral options for those networks will no longer be active on Secured Finance Fixed Rate Lending Protocol.
{% endhint %}

## Related Resources

- [Liquidation](liquidation/README.md)
- [Order Book System](order-book-system/README.md)
- [Safety Measures](../advanced-topics/safety-measures/README.md)
