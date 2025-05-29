---
description: >-
  Understanding how under-collateralized positions are handled in the USDFC
  protocol
---

# 🚰 Liquidation

## Overview

Liquidation is a critical mechanism in the USDFC Stablecoin Protocol that ensures the system remains solvent by handling under-collateralized positions. When a Trove's collateral ratio falls below 110%, it becomes eligible for liquidation, allowing the protocol to use the Stability Pool to cover the debt and distribute the collateral to depositors.

## How It Works

Liquidations occur when a Trove's collateral ratio falls below the minimum threshold of 110%. The process involves using USDFC from the Stability Pool to repay the debt of the liquidated Trove, while distributing the Trove's collateral to Stability Pool depositors at a discount.

### Liquidation Process

1. **Triggering Liquidation**: When a Trove's collateral ratio falls below 110%, a Liquidator triggers the liquidation
2. **Debt Repayment**: The Stability Pool covers the Trove's debt by burning the corresponding amount of USDFC
3. **Collateral Distribution**: The collateral (FIL) from the liquidated Trove is distributed to the Stability Pool depositors based on their pool share, minus the Liquidator's compensation

### The Stability Pool

The Stability Pool is a reserve of USDFC dedicated to absorbing liquidations when a borrower's collateral ratio falls below the required 110%. The pool serves several important functions:

* **Purpose**: The Stability Pool repays the debt of liquidated borrowers using the deposited USDFC
* **Depositor Rewards**: When USDFC from the pool is used, depositors receive Filecoin (FIL) from the liquidated collateral at a discount
* **System Stability**: By providing a mechanism to handle under-collateralized positions, the Stability Pool helps maintain the overall stability of the protocol

## Key Parameters

| Parameter             | Description                                                 | Default Value |
| --------------------- | ----------------------------------------------------------- | ------------- |
| Liquidation Threshold | Collateral ratio below which a Trove can be liquidated      | 110%          |
| Liquidator Reward     | Percentage of liquidated collateral given to the liquidator | 0.5%          |
| Liquidation Reserve   | USDFC reserved for potential liquidation gas costs          | 20 USDFC      |

## Stakeholders in the Liquidation Process

### 1. Stability Pool Depositors

* Provide USDFC to the pool and receive FIL at a discount when liquidations occur
* Effectively "buy FIL cheaper" than market price through the liquidation process
* Earn passive rewards by helping maintain system stability

### 2. Liquidated Borrowers

* Have their Trove liquidated when their collateral ratio falls below 110%
* Lose a portion of their collateral to repay their debt
* Trove will be closed, but they keep their borrowed USDFC
* Typically incur around a 10% loss in the process

### 3. Liquidators

* Trigger the liquidation process by calling the liquidation function
* Receive the Liquidation Reserve (20 USDFC) as gas compensation
* Earn 0.5% of the liquidated collateral as an incentive

## Price Oracle

Secured Finance uses Pyth as the primary oracle to determine the FIL price. Pyth provides accurate and reliable real-time price feeds essential for system operations.

### Fallback Mechanism

In case of extreme conditions where the Pyth price feed is unavailable, the protocol switches to Tellor as a backup:

* Pyth price not updated for over 4 hours
* Pyth response reverts, returns invalid data, or shows an invalid timestamp
* Price change between consecutive updates exceeds 50%

This dual-oracle approach ensures that the protocol maintains accurate pricing and stability, even under extreme conditions.

## What Happens If the Stability Pool Is Empty?

If the Stability Pool is empty during a liquidation, the protocol switches to a redistribution mechanism:

1. **Trove Liquidation**: A Trove is liquidated, but the Stability Pool has insufficient USDFC
2. **Debt and Collateral Redistribution**: The debt and collateral are proportionally distributed to other active Troves
3. **Impact on Troves**: Troves receiving the redistributed collateral and debt may see their collateral ratio lower, while the net USD value increases

## Common Questions

**How can I avoid liquidation?**\
Maintain a collateral ratio well above 110%. A buffer of 150% or higher is recommended to account for FIL price volatility.

**What happens to my borrowed USDFC if my Trove is liquidated?**\
You keep your borrowed USDFC, but lose your collateral. The liquidation effectively closes your Trove.

**How can I benefit from liquidations?**\
You can deposit USDFC into the Stability Pool to receive discounted FIL when liquidations occur, or become a liquidator to earn rewards for triggering liquidations.

[Learn more in the FAQs section](../faqs.md)

## Related Topics

* [The Trove System](the-trove-system.md)
* [Collateral Ratio](liquidation/collateral-ratio.md)
* [Liquidators](liquidation/liquidators.md)
* [Liquidation Case Study](liquidation/case-study.md)
* [Recovery Mode](../advanced-topics/recovery-mode.md)
