---
description: Understanding the role of liquidators in maintaining protocol stability
---

# 👮‍♂️ Liquidators

## Overview

In the Secured Finance ecosystem, Liquidators play a crucial role in maintaining the health and stability of the decentralized loan protocol. As a Liquidator, you have the unique opportunity to participate in the liquidation process, ensuring the safety of lenders' funds while potentially earning rewards for your efforts.

## How It Works

When a borrower's collateral value falls below the liquidation threshold, their loan becomes susceptible to liquidation. As a Liquidator, your role is to step in and purchase the undercollateralized loan at a discounted price, providing the borrower with an opportunity to recover their position. By liquidating the loan, you allow lenders to recoup their funds and mitigate the risk of defaults.

To become a Liquidator, you don't need to meet any specific criteria. Any user, even if using smart contracts, can call the liquidation process.

For more technical details, please consult '[How Liquidation Works](how-liquidation-works.md)'.

## Key Parameters

| Parameter                | Description                                                        | Value |
| ------------------------ | ------------------------------------------------------------------ | ----- |
| Liquidation Threshold    | The LTV ratio at which a position becomes eligible for liquidation | 80%   |
| Liquidation Penalty      | The discount applied to collateral during liquidation              | 5%    |
| Minimum Liquidation Size | The smallest position that can be liquidated                       | None  |
| Liquidation Cooldown     | Time required between liquidations of the same position            | None  |

## Examples

### Example 1: Basic Liquidation Process

A liquidator monitors the protocol for undercollateralized positions:

1. The liquidator identifies a borrower with an LTV ratio of 82% (above the 80% threshold)
2. The borrower has 10,000 USDC collateral and 8,200 USDC worth of debt
3. The liquidator calls the liquidation function, specifying the borrower's address
4. The protocol automatically liquidates 50% of the position (4,100 USDC worth of debt)
5. The liquidator pays 4,100 USDC to cover this debt
6. The liquidator receives 4,305 USDC worth of collateral (4,100 × 1.05)
7. The liquidator earns a profit of 205 USDC (5% liquidation fee)

### Example 2: Liquidation Bot Implementation

```javascript
// Pseudocode for a basic liquidation bot
async function monitorForLiquidations() {
  while (true) {
    // Get all borrowers from the protocol
    const borrowers = await protocol.getAllBorrowers();
    
    // Check each borrower's position
    for (const borrower of borrowers) {
      const ltv = await protocol.getLTV(borrower);
      
      // If LTV is above liquidation threshold
      if (ltv >= 8000) { // 80% represented as 8000 basis points
        // Calculate potential profit
        const debtValue = await protocol.getDebtValue(borrower);
        const liquidationAmount = debtValue.div(2); // 50% liquidation
        const profit = liquidationAmount.mul(5).div(100); // 5% fee
        
        // Check if profitable after gas costs
        const gasEstimate = await protocol.estimateGas.liquidate(borrower);
        const gasCost = gasEstimate.mul(gasPrice);
        
        if (profit.gt(gasCost)) {
          // Execute liquidation
          await protocol.liquidate(borrower);
          console.log(`Liquidated ${borrower} for a profit of ${profit} USDC`);
        }
      }
    }
    
    // Wait before next check
    await sleep(30000); // Check every 30 seconds
  }
}
```

## FAQ

### Who can become a liquidator?

Anyone can become a liquidator in the Fixed-Rate Lending Protocol. There are no special requirements or permissions needed. Both individuals and smart contracts can participate in the liquidation process.

### How do I profit from being a liquidator?

Liquidators profit from the liquidation penalty (currently 5%) applied to the liquidated debt. When you liquidate a position, you pay the debt amount but receive collateral worth more than what you paid. The difference is your profit.

### What tools do I need to become an effective liquidator?

To be an effective liquidator, you typically need:

1. A monitoring system to track positions close to liquidation threshold
2. Sufficient capital to cover the debt you're liquidating
3. Automation tools or bots to execute liquidations quickly
4. Gas price monitoring to ensure liquidations remain profitable

### Are there any risks involved in being a liquidator?

Yes, there are several risks:

1. **Price Volatility**: Rapid price changes can affect the value of the collateral you receive
2. **Gas Costs**: High gas prices can reduce or eliminate profitability
3. **Competition**: Other liquidators may compete for the same liquidation opportunities
4. **Smart Contract Risk**: As with any DeFi activity, there's always some level of smart contract risk

### How quickly do I need to act when a position becomes eligible for liquidation?

Speed is crucial in liquidations. Once a position crosses the liquidation threshold, it becomes a race among liquidators to execute the transaction first. Positions are typically liquidated within seconds or minutes of becoming eligible, depending on market conditions and visibility of the position.

## Risks and Rewards

Being a Liquidator comes with both risks and rewards. The main risk is the potential price volatility of the assets involved in the liquidation process. The value of the collateral may fluctuate rapidly, affecting the profitability of the liquidation.

On the other hand, the rewards for successful liquidations can be lucrative. Liquidators stand to receive a portion of the discounted collateral acquired during the liquidation. This reward serves as an incentive for participants to actively engage in the liquidation process and contribute to the protocol's stability.

## Related Topics

* [Liquidation Process](../)
* [How Liquidation Works](how-liquidation-works.md)
* [Mark to Market](../mark-to-market.md)
