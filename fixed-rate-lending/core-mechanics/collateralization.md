---
description: Understanding how collateral secures loans in the Fixed-Rate Lending Protocol
icon: 🏋️
---

# 🏋️ Collateralization

## Overview

Collateralization is a fundamental mechanism in the Fixed-Rate Lending Protocol that ensures the security and stability of the lending system. By requiring borrowers to deposit assets as collateral, the protocol protects lenders from default risk while enabling borrowers to access liquidity without traditional credit checks.

## What You'll Learn

- What collateral is and why it's essential for secured lending
- How collateral serves dual purposes in risk reduction and financial inclusivity
- What cryptocurrencies are accepted as collateral across different networks
- How to obtain and use specialized collateral types like iFIL
- How collateral management affects liquidation risk

## Key Components

- **Loan-to-Value (LTV) Ratio**: The relationship between borrowed amount and collateral value
- **Collateral Currencies**: The various assets accepted as collateral across different networks
- **Liquidation Threshold**: The point at which undercollateralized positions become eligible for liquidation

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

## Future Plans: Expanding Collateral Options

While WBTC, ETH, USDC, FIL, iFIL, pFIL, and USDFC are our current collateral options across supported networks, we continue to explore additional assets that align with our commitment to flexibility, security, and open DeFi principles. Stay tuned for updates on new collateral integrations and chain support as we further evolve the Secured Finance platform.

{% hint style="warning" %}
We are **sunsetting support** for Avalanche and Polygon zkEVM. Collateral options for those networks will no longer be active on Secured Finance Fixed Rate Lending Protocol.
{% endhint %}

## Related Resources

- [Liquidation](liquidation/README.md)
- [Order Book System](order-book-system/README.md)
- [Safety Measures](../advanced-topics/safety-measures/README.md)
