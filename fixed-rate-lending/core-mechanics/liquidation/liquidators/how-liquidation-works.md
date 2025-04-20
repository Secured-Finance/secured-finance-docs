---
description: A technical guide to the liquidation process implementation in the Fixed-Rate Lending Protocol
icon: ✏️
---

# ✏️ How Liquidation Works

## Overview

The liquidation process in the Fixed-Rate Lending Protocol involves identifying undercollateralized positions and executing liquidation calls through smart contract functions. This technical guide explains the implementation details of how liquidation works from a developer's perspective.

## What You'll Learn

- How to identify positions eligible for liquidation using the `getCoverage()` function
- How to execute liquidation calls with the `executeLiquidationCall()` function
- How to implement callback functions for handling liquidated assets
- How to maximize profits from liquidation opportunities
- How the liquidation process flow works at the smart contract level

## How It Works

First of all, it is necessary to identify the target user through off-chain actions before executing liquidation. The function `getCoverage()` is used for this purpose. A user becomes a target for liquidation if this function returns a value of `8000` or higher. For more details, refer to the documentation at [TokenVault Documentation](https://github.com/Secured-Finance/contracts/blob/develop/docs/protocol/TokenVault.md#getcoverage).

To execute with liquidation, you must specify the currency of the collateral to be received, the currency of the debt to be liquidated, and its maturity. This is done by calling the function `executeLiquidationCall()`. To maximize the profit of the liquidation in the case that users have collateral or debt in multiple currencies, you need to estimate each case and choose one of them through off-chain action. For more details of the function, refer to the documentation at [LendingMarketController Documentation](https://github.com/Secured-Finance/contracts/blob/develop/docs/protocol/LendingMarketController.md#executeliquidationcall).

Upon executing this process, the liquidator receives the liquidated debt and the collateral plus a 5% fee. However, if the liquidator's collateral coverage exceeds 80% at the end of the process, this liquidation process will fail.

When executing the liquidation process through a smart contract, functions `executeOperationForCollateral()` for receiving collateral, and `executeOperationForDebt()` for receiving debt, can be set as callback functions. For usage, please refer to the sample contract at [Liquidator Contract](https://github.com/Secured-Finance/contracts/blob/develop/contracts/external/liquidation/Liquidator.sol).

During the liquidation process, these callback functions enable the handling of received collateral by swapping it through external services or unwinding the received debt. The process flow is as follows:

```mermaid
sequenceDiagram
autonumber

title Liquidation Process

  actor Bot as Liquidatior
  participant Liquidator as Liquidator
  participant Market as LendingMarketContoroller
  participant FV as FutureValueVault
  participant Token as TokenVault

Bot-->>Market: Check if the selected user<BR>has enough collateral 
Bot-->>Liquidator: Liquidate the<BR>selected user
Liquidator-->>Market: Execute liquidation<BR>process
Market-->>Market: Check if the selected user<BR>doesn't has enough collateral 
Market-->>Token: Transfer the collaterl balance<BR>from the selected user<BR>to the liquidator<BR>(Liquidation fee included)
Market-->>Liquidator: Execute the callback<BR>function for the collateral
Market-->>FV: Transfer the debt balance<BR>from the selected user<BR>to the liquidator
Market-->>Liquidator: Execute the callback<BR>function for debt
Market-->>Market: Check if the liquidator<BR>has enough collateral
```

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Coverage Threshold | The threshold value returned by `getCoverage()` that makes a position eligible for liquidation | 8000 |
| Liquidation Fee | The additional collateral received by the liquidator | 5% |
| Liquidator Coverage Limit | Maximum coverage value a liquidator can have after liquidation | 80% |
| Callback Functions | Functions that can be implemented to handle received assets | `executeOperationForCollateral()`, `executeOperationForDebt()` |

## Related Resources

- [Liquidators](README.md)
- [Liquidation Process](../../README.md)
- [Mark to Market](../../mark-to-market.md)
- [Collateral Liquidations](../../collateral-liquidations/README.md)
