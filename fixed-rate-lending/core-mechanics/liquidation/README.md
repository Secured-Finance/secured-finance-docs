---
description: Understanding the liquidation process that maintains solvency in the Fixed-Rate Lending Protocol
icon: 🚰
---

# 🚰 Liquidation

## Overview

The liquidation process in the Fixed-Rate Lending protocol is a critical mechanism that ensures the solvency and stability of the system. When a borrower's position becomes undercollateralized, the liquidation process allows for the orderly repayment of debt using the borrower's collateral, protecting lenders and maintaining the overall health of the protocol.

This section explains the liquidation process specific to the Fixed-Rate Lending protocol. Note that this differs from the liquidation process involving the Stability Pool in the USDFC Stablecoin protocol.

## What You'll Learn

- How the liquidation process protects lenders from default risk
- How Loan-to-Value (LTV) ratio determines liquidation eligibility
- How liquidation penalties and thresholds work
- How price oracles determine collateral value
- How liquidators execute the liquidation process

## Key Components

- [**Collateral Liquidations**](collateral-liquidations/README.md): The process of liquidating undercollateralized positions
- [**Mark to Market**](mark-to-market.md): The valuation mechanism for determining collateral value
- [**Liquidators**](liquidators/README.md): The third-party actors who execute liquidations
- [**Case Study**](case-study.md): A detailed example of the liquidation process

## Why Liquidation Process is Important

The liquidation process holds paramount importance for Secured Finance as a Decentralized Loan Protocol, primarily for two crucial reasons:

1.  **Mitigating default risk:** Through the liquidation process, lenders are safeguarded against the risk of default by borrowers. When a borrower's collateral value falls below the liquidation threshold relative to their debt, their loan becomes eligible for liquidation, ensuring the lenders can recover their funds.
2.  **Maintaining protocol stability:** The liquidation process plays a pivotal role in preserving the stability of the DeFi loan protocol. It prevents the accumulation of undercollateralized loans. Excessive loan defaults can deplete the protocol's reserves, potentially leading to system instability. By executing liquidations, the protocol can maintain a healthy balance and ensure its overall stability.

## How Does It Work?

When the borrower's [**Loan to Value (LTV)**](#loan-to-value) ratio surpasses the defined [**Threshold**](#threshold), the borrower's position (collateral) becomes subject to liquidation.

During a liquidation process:
*   A portion of the borrower's outstanding debt (up to 50%) is repaid using their deposited collateral.
*   The amount of collateral seized is equal to the value of the debt being repaid plus a [**Liquidation Penalty**](#liquidation-penalty).
*   Liquidations are typically executed by third-party [Liquidators](./collateral-liquidations/README.md) who are incentivized to perform this action.

### Loan to Value (LTV)

The Loan to Value (LTV) ratio compares the value of a borrower's debt to the value of their collateral.

`LTV = (Value of Debt / Value of Collateral) * 100%`

A higher LTV indicates a higher risk of liquidation. The platform visualizes this risk:
*   **Green:** Low risk
*   **Yellow:** Moderate risk
*   **Red:** High risk (approaching liquidation threshold)

<figure><img src="../../../.gitbook/assets/risk-v2.gif" alt="" width="563"><figcaption><p>LTV and Liquidation Risk Visualization</p></figcaption></figure>

### Threshold

The liquidation threshold is the LTV percentage at which a borrower's position becomes eligible for liquidation.
*   **Current Threshold:** 80% for all currencies.
*   **Dynamic Adjustment:** This threshold may be adjusted based on market conditions (volatility, liquidity) for specific assets.
*   **Over-Collateralization:** Borrowers must initially deposit collateral worth significantly more than their loan amount to provide a safety buffer.

### Price Oracle

The value of collateral is determined using real-time price feeds, primarily from Chainlink. The protocol uses [Mark-to-Market](./mark-to-market.md) principles based on recent trading activity (VWAP) where available, falling back to oracle prices if necessary.

## Liquidation Penalty

A penalty is applied during liquidation to compensate the liquidator and contribute to the protocol's reserve fund.
*   **Current Penalty:** 7% on the value of the collateral being liquidated.

Borrowers should actively manage their collateral levels to avoid liquidation and the associated penalty.

> See a detailed example in the [Liquidation Case Study](./case-study.md).
> Learn more about the role of liquidators in [Collateral Liquidations](./collateral-liquidations/README.md).

## Related Resources

- [Collateralization](../collateralization.md)
- [Order Book System](../order-book-system/README.md)
- [Safety Measures](../../advanced-topics/safety-measures/README.md)
