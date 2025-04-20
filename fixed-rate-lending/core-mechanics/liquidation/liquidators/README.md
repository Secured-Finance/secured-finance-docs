---
description: Understanding the role of liquidators in maintaining protocol stability
icon: 🤖
---

# 🤖 Liquidators

## Overview

In the Secured Finance ecosystem, Liquidators play a crucial role in maintaining the health and stability of the decentralized loan protocol. As a Liquidator, you have the unique opportunity to participate in the liquidation process, ensuring the safety of lenders' funds while potentially earning rewards for your efforts.

## What You'll Learn

- How to become a liquidator in the Fixed-Rate Lending Protocol
- What criteria are required to participate in liquidations
- How the liquidation process works from a liquidator's perspective
- What risks and rewards are associated with being a liquidator
- How to maximize profits from liquidation opportunities

## How It Works

When a borrower's collateral value falls below the liquidation threshold, their loan becomes susceptible to liquidation. As a Liquidator, your role is to step in and purchase the undercollateralized loan at a discounted price, providing the borrower with an opportunity to recover their position. By liquidating the loan, you allow lenders to recoup their funds and mitigate the risk of defaults.

To become a Liquidator, you don't need to meet any specific criteria. Any user, even if using smart contracts, can call the liquidation process.

For more technical details, please consult '[How Liquidation Works](how-liquidation-works.md)'.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Liquidation Threshold | The LTV ratio at which a position becomes eligible for liquidation | 80% |
| Liquidation Penalty | The discount applied to collateral during liquidation | 5% |
| Minimum Liquidation Size | The smallest position that can be liquidated | None |
| Liquidation Cooldown | Time required between liquidations of the same position | None |

## Risks and Rewards

Being a Liquidator comes with both risks and rewards. The main risk is the potential price volatility of the assets involved in the liquidation process. The value of the collateral may fluctuate rapidly, affecting the profitability of the liquidation.&#x20;

On the other hand, the rewards for successful liquidations can be lucrative. Liquidators stand to receive a portion of the discounted collateral acquired during the liquidation. This reward serves as an incentive for participants to actively engage in the liquidation process and contribute to the protocol's stability.

## Related Topics

- [Liquidation Process](../README.md)
- [How Liquidation Works](how-liquidation-works.md)
- [Mark to Market](../mark-to-market.md)
- [Collateral Liquidations](../collateral-liquidations/README.md)

