---
description: Comprehensive answers to frequently asked questions about Fixed-Rate Lending
---

# ❓ Fixed-Rate Lending FAQs

## Overview

This FAQ covers the Fixed-Rate Lending protocol, from basic trading concepts to advanced features and risk management. Whether you're new to fixed-rate lending or looking for specific technical details, you'll find comprehensive answers here.

## What You'll Learn

- How zero-coupon bonds and fixed-rate lending work on Secured Finance
- Trading operations, order management, and platform navigation
- Collateral requirements and liquidation processes
- Advanced features like auto-rolling, Itayose, and market dynamics
- Risk management and troubleshooting common issues

## Quick Navigation

- [Platform Basics](#platform-basics)
- [Trading Operations](#trading-operations)
- [Risk Management](#risk-management)
- [Advanced Features](#advanced-features)

## Platform Basics

<details>
<summary>What is Secured Finance?</summary>

Secured Finance is a decentralized finance platform that facilitates peer-to-contract lending and derivatives trading. Built on multiple blockchains including Ethereum, Arbitrum, and Filecoin, it offers a transparent, robust, and cost-effective alternative to traditional financial institutions.

The platform consists of two main products:
- **Fixed-Rate Lending Protocol**: Enables fixed-rate, fixed-term lending and borrowing through zero-coupon bonds
- **USDFC Stablecoin**: A dollar-pegged stablecoin backed by Filecoin collateral

**Related:** [Platform Overview](../overview/README.md)
</details>

<details>
<summary>What is a Zero-Coupon Bond (ZC Bond)?</summary>

A Zero-Coupon Bond (ZC Bond) is a debt instrument that doesn't pay interest during its life. Instead, it's sold at a discount to its face value and pays the full face value at maturity. This makes them ideal for users who want a guaranteed return at a specific future date.

**Example:**
- You buy a ZC Bond for 950 USDC that matures in 6 months for 1,000 USDC
- Your fixed return is 50 USDC (approximately 10.5% APR)
- No interest payments during the 6-month period

**Related:** [Zero-Coupon Bonds](../core-mechanics/standardization/zero-coupon-bonds.md)
</details>

<details>
<summary>What is the underlying asset for zero-coupon bonds?</summary>

The underlying asset for zero-coupon bonds is the specific digital asset lent by the user. For example, lending ETH in the "September 2026 Order Book" mints a bond called **"ZC ETH SEP2026"**, representing the loaned ETH and its maturity date.

Each ZC Bond is:
- **Asset-specific**: Denominated in the currency being lent (ETH, USDC, etc.)
- **Maturity-specific**: Includes the exact maturity date in the token name
- **Transferable**: Can be traded or used as collateral on other DeFi protocols

**Related:** [Tokenization](../core-mechanics/tokenization.md)
</details>

<details>
<summary>Can zero-coupon bonds be used outside the Secured Finance platform?</summary>

Yes, zero-coupon bonds are tokenized and fully transferable ERC-20 tokens. They can be used on other DeFi protocols for:
- **Trading**: Sell your position on secondary markets
- **Collateral**: Use ZC Bonds as collateral for other loans
- **Yield optimization**: Integrate with other DeFi strategies
- **Portfolio management**: Track and manage across multiple platforms

This composability is a key advantage of Secured Finance's tokenized approach to fixed-rate lending.

**Related:** [Tokenization](../core-mechanics/tokenization.md)
</details>

## Trading Operations

<details>
<summary>How do I buy or sell a ZC Bond on Secured Finance?</summary>

To trade ZC Bonds on Secured Finance:

1. **Connect your wallet** to the platform
2. **Browse the order book** for your desired maturity and asset
3. **Place your order** (market or limit order)
4. **Confirm the transaction** in your wallet
5. **Receive your ZC Bond** automatically via smart contract

The platform uses smart contracts to ensure automatic execution and settlement. For detailed instructions, see our [Trading Guide](../getting-started/platform-guide/trading/README.md).

**Related:** [Platform Guide](../getting-started/platform-guide/README.md)
</details>

<details>
<summary>Is my money locked until maturity?</summary>

No, there is **no lock-up period** involved. Similar to spot transactions, our platform facilitates the trading of Zero Coupon Bonds (ZC Bonds) 24/7.

**As a lender** (ZC Bond holder):
- **Unwind**: Sell your ZC Bond back to the market anytime
- **Transfer**: Move your ZC Bond to another wallet or platform
- **Use as collateral**: Leverage your ZC Bond in other DeFi protocols

**As a borrower** (with outstanding orders):
- **Cancel orders**: Withdraw funds from unfilled limit orders anytime
- **Partial fills**: Access funds from partially filled orders immediately

**Note:** Users must manually unwind their positions when bonds reach maturity. The protocol does not automatically settle positions at maturity.

**Related:** [Order Life Cycle](../core-mechanics/order-book-system/order-life-cycle/README.md)
</details>

<details>
<summary>How does lending and borrowing work on Secured Finance?</summary>

Secured Finance uses a peer-to-peer order book system where lending and borrowing happen through ZC Bond creation and trading:

**To Lend (Buy ZC Bonds):**
1. Deposit assets into your collateral vault
2. Browse available borrowing orders
3. Buy ZC Bonds at your desired rate
4. Receive principal + yield at maturity

**To Borrow (Sell ZC Bonds):**
1. Deposit collateral (must exceed borrowing amount)
2. Create a ZC Bond sell order
3. Receive borrowed funds when order is filled
4. Repay at maturity or face liquidation

**Related:** [Core Mechanics](../core-mechanics/README.md)
</details>

<details>
<summary>What is the user journey for lending assets?</summary>

The complete lending journey involves:

1. **Wallet Connection**: Connect your Web3 wallet to the platform
2. **Deposit Collateral**: Add assets to your collateral vault for gas and potential margin
3. **Select Order Book**: Choose your preferred maturity date and asset
4. **Place Lending Order**: Buy ZC Bonds at your desired rate
5. **Receive ZC Bonds**: Get tokenized proof of your lending position
6. **Monitor Position**: Track performance in your portfolio
7. **Maturity Settlement**: Manually unwind position to receive principal + yield, or trade before maturity

**Related:** [Lending Assets Guide](../getting-started/lending-assets.md)
</details>

<details>
<summary>What happens to my outstanding order when the order book matures?</summary>

When an order book reaches maturity:

- **Unfilled orders** are automatically sent to your Collateral Vault
- **Filled positions** are settled according to the contract terms
- **Funds become available** for withdrawal or new trades

From your Collateral Vault, you can:
- **Withdraw funds** to your wallet
- **Place new orders** in active order books
- **Transfer to other assets** or maturities

This automatic process ensures you never lose access to your funds due to market maturity.

**Note:** For filled positions, users must manually unwind their ZC Bonds when they reach maturity to receive their principal and yield.

**Related:** [Order Life Cycle](../core-mechanics/order-book-system/order-life-cycle/README.md)
</details>

<details>
<summary>Why is my unwinding order 'Blocked' or 'Partially Blocked'?</summary>

Unwinding orders may become **'Blocked'** for two main reasons:

1. **Insufficient liquidity**: Not enough matching orders available on the order book
2. **Circuit Breaker limits**: Available orders are outside the acceptable price range

**'Partially Blocked'** means only part of your unwinding order was executed, with the remainder still seeking matches.

**Solutions:**
- **Wait for liquidity**: New orders may appear that match your requirements
- **Place a limit order**: Set your own price and wait for execution
- **Adjust your price**: Move closer to market rates if acceptable

The Circuit Breaker is a safety feature that prevents price manipulation by limiting deviations from the mark price.

**Related:** [Circuit Breaker](../advanced-topics/safety-measures/circuit-breaker/README.md)
</details>

## Risk Management

<details>
<summary>What is collateral and why is it needed?</summary>

Collateral is an asset that borrowers deposit to secure their loans. It serves as protection for lenders and ensures the integrity of the lending process.

**Key functions:**
- **Security**: Protects lenders against borrower default
- **Liquidation source**: Provides assets to cover unpaid debts
- **Risk management**: Enables automated position monitoring

**For borrowers**: Collateral must exceed the borrowed amount by a safety margin
**For lenders**: Collateral provides confidence in loan repayment

**Related:** [Collateralization](../core-mechanics/collateralization.md)
</details>

<details>
<summary>What types of assets can be used as collateral?</summary>

Secured Finance currently accepts these assets as collateral:

**Ethereum & Arbitrum:**
- **ETH**: Native Ethereum
- **WBTC**: Wrapped Bitcoin
- **USDC**: USD Coin stablecoin

**Filecoin:**
- **FIL**: Native Filecoin
- **iFIL**: Interest-bearing FIL (FVM only)

These assets were chosen for their:
- **Liquidity**: High trading volumes and market depth
- **Stability**: Established track record and wide acceptance
- **Oracle support**: Reliable price feeds for liquidation calculations

Secured Finance continuously evaluates additional assets based on community demand and risk assessment.

**Related:** [Supported Currencies](../getting-started/platform-guide/trading/supported-currencies.md)
</details>

<details>
<summary>What happens if the value of my collateral falls?</summary>

If your collateral value falls and your loan-to-value (LTV) ratio exceeds the liquidation threshold:

1. **Warning phase**: Your position becomes at-risk
2. **Liquidation trigger**: Automated liquidators can close your position
3. **Asset sale**: Collateral is sold to repay the debt
4. **Remaining funds**: Any surplus is returned to you

**Prevention strategies:**
- **Monitor your LTV ratio** regularly in your portfolio
- **Add more collateral** when approaching limits
- **Reduce debt** by repaying part of your loan
- **Set up alerts** for position health monitoring

**Related:** [Liquidation Process](../core-mechanics/liquidation/README.md)
</details>

## Advanced Features

<details>
<summary>What is the Itayose process?</summary>

Itayose is a fair price discovery mechanism used when new order books start trading. It ensures efficient order matching by:

1. **Collecting orders**: Gathering all initial buy and sell orders
2. **Finding equilibrium**: Determining the price that maximizes trading volume
3. **Batch execution**: Executing all compatible orders simultaneously
4. **Fair pricing**: Ensuring all participants get the same fair market price

This process prioritizes the highest bid and lowest ask prices while maximizing the number of successful trades.

**Benefits:**
- **Fair price discovery**: Prevents manipulation during market opening
- **Maximum liquidity**: Enables the most trades possible
- **Equal treatment**: All participants get the same execution price

**Related:** [Itayose Process](../advanced-topics/market-dynamics/new-market-listing-and-delisting/itayose-fair-price-discovery.md)
</details>

<details>
<summary>What is Auto-Rolling?</summary>

Auto-Rolling is a feature that automatically reinvests your funds when positions mature, helping you:

**Benefits:**
- **Mitigate reinvestment risk**: Avoid gaps between investment periods
- **Ensure cost-efficiency**: Reduce transaction costs through automation
- **Promote continuous growth**: Maintain your investment strategy seamlessly
- **Save time**: Eliminate manual reinvestment processes

**How it works:**
1. **Position maturity**: Your ZC Bond reaches its maturity date
2. **Automatic reinvestment**: Funds are automatically placed in the next available market
3. **Rate determination**: New rate is set based on current market conditions
4. **Continuous compounding**: Your returns continue growing without interruption

**Related:** [Auto-Rolling](../advanced-topics/market-dynamics/auto-rolling/README.md)
</details>

## Related Resources

- [Getting Started Guide](../getting-started/README.md)
- [Core Mechanics Documentation](../core-mechanics/README.md)
- [Advanced Topics](../advanced-topics/README.md)
- [Platform Guide](../getting-started/platform-guide/README.md)
- [Developer Portal](../../developer-portal/introduction.md)
