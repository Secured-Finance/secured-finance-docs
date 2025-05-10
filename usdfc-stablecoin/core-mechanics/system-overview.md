---
description: Understanding the USDFC Stablecoin Protocol Architecture
---

# 🏗️ System Overview

## Overview

The USDFC Stablecoin Protocol is a decentralized system that enables users to mint a USD-pegged stablecoin (USDFC) by depositing Filecoin (FIL) as collateral. The protocol maintains stability through a series of interconnected mechanisms that ensure USDFC maintains its 1:1 peg to the US Dollar.

## How It Works

The protocol operates through several key components that work together to maintain stability, manage collateral, and ensure the proper functioning of the system:

1. **Trove System**: Individual vaults where users deposit FIL collateral and mint USDFC
2. **Stability Pool**: A reserve of USDFC that absorbs liquidations of under-collateralized Troves
3. **Redemption Mechanism**: Allows USDFC holders to exchange their tokens for FIL at face value
4. **Recovery Mode**: A special state that activates when the system's overall collateral ratio falls below 150%
5. **Price Oracle**: Provides accurate FIL/USD price data to determine collateral values

## System Architecture

### Normal Mode

<figure><img src="../../.gitbook/assets/image (5).png" alt="Normal Mode Architecture"><figcaption><p>USDFC Protocol Architecture in Normal Mode</p></figcaption></figure>

### Recovery Mode

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="Recovery Mode Architecture"><figcaption><p>USDFC Protocol Architecture in Recovery Mode</p></figcaption></figure>

## Key Parameters

| Parameter                      | Description                                        | Default Value |
| ------------------------------ | -------------------------------------------------- | ------------- |
| Minimum Collateral Ratio (MCR) | Minimum required ratio of collateral to debt       | 110%          |
| Recovery Mode Threshold        | TCR level that triggers Recovery Mode              | 150%          |
| Liquidation Reserve            | USDFC reserved for potential liquidation gas costs | 20 USDFC      |
| Minimum Borrow Amount          | Minimum USDFC that can be borrowed                 | 180 USDFC     |
| Base Rate                      | Variable component of minting and redemption fees  | 0% to 4.5%    |

## Common Questions

**What happens if the price of FIL drops significantly?**\
If FIL price drops, Troves with lower collateral ratios may become eligible for liquidation. The protocol prioritizes liquidating the riskiest Troves first to maintain system solvency.

**How does the protocol maintain the USDFC peg?**\
The redemption mechanism allows USDFC holders to exchange their tokens for FIL at face value, creating arbitrage opportunities that help maintain the peg.

**What is the difference between Normal Mode and Recovery Mode?**\
In Normal Mode, Troves require a minimum 110% collateral ratio. In Recovery Mode, stricter rules apply, including higher liquidation thresholds and restrictions on borrowing.

[Learn more in the FAQs section](../faqs.md)

## Related Topics

* [The Trove System](the-trove-system.md)
* [Mint & Borrow](mint-and-borrow.md)
* [Liquidation](liquidation.md)
* [Redemption](redemption.md)
* [Recovery Mode](../advanced-topics/recovery-mode.md)
