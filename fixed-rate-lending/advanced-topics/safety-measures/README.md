---
description: Protective mechanisms that ensure the stability and security of the Fixed-Rate Lending Protocol
icon: 🛡️
---

# 🛡️ Safety Measures

## Overview

Safety Measures in the Fixed-Rate Lending Protocol are critical mechanisms designed to protect the system from extreme market conditions, price manipulation, and other potential risks. These features work together to ensure the protocol remains stable, secure, and reliable for all participants.

## What You'll Learn

- How Circuit Breaker prevents price manipulation and extreme volatility
- How Base Price Adjustment maintains fair pricing during market stress
- How Emergency Global Settlement protects the protocol in extreme scenarios
- How these safety mechanisms work together to ensure system stability

## Key Components

- [**Circuit Breaker**](circuit-breaker/README.md): Limits price deviations to prevent manipulation
- [**Base Price Adjustment**](base-price-adjustment.md): Ensures fair pricing during market stress
- [**Emergency Global Settlement**](emergency-global-settlement.md): Protocol-wide safety mechanism for extreme scenarios

## Related Resources

- [Market Dynamics](../market-dynamics/README.md)
- [Orderbook Deep Dive](../orderbook-deep-dive/README.md)
- [Core Mechanics](../../core-mechanics/README.md)

Protocol Safety Measures are a critical aspect of our protocol. We have implemented robust mechanisms to ensure the safety and stability of our platform. This includes the Emergency Termination Procedure and the Circuit Breaker.

### [Mark to Market](../../protocol-features/liquidation/mark-to-market.md)

Mark to Market is a standard accounting practice adopted at Secured Finance, which entails recording the fair value of assets and liabilities, thereby providing a realistic appraisal of the financial health and the risk profile of positions on our platform. This practice is indispensable for maintaining transparency and accuracy in financial reporting, which in turn fosters trust and confidence among our users. The Mark to Market mechanism also plays a pivotal role in ensuring that the pricing of assets is aligned with the current market conditions, which is vital for effective risk management.

***

### [Price Range Limit](circuit-breaker/) (Circuit Breaker)

The Circuit Breaker is a protective mechanism used in the bond market to prevent excessive price movements and maintain stability. It is an automatic mechanism that temporarily suspends trading if there is a sudden and significant price movement. The Circuit Breaker is triggered when the price of bonds rises or falls beyond a certain pre-determined limit during one block.

***

### [Minimum Collateral](base-price-adjustment.md)

The Minimum Collateral mechanism is a crucial safeguard designed to ensure that every position on our platform is sufficiently backed by collateral. This practice minimizes the risk of financial loss, both to the individual trader and the broader market, especially in volatile market conditions. By stipulating a minimum collateral requirement, we create a buffer against adverse market fluctuations, ensuring that positions remain solvent and the system resilient.

***

### [Emergency Termination Procedure](emergency-global-settlement.md)

Emergency termination is a crucial functionality designed to address unforeseen situations that could compromise the integrity of our protocol. This includes scenarios such as hacks or unexpected bugs. When this functionality is executed, all markets are immediately halted, and the protocol becomes non-operational. Users can then only redeem their positions and withdraw their tokens.
