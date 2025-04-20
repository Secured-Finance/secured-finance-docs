---
description: Protective mechanisms that ensure the stability and security of the Fixed-Rate Lending Protocol
icon: 🛡️
---

# 🛡️ Safety Measures

## Overview

Safety Measures in the Fixed-Rate Lending Protocol are critical mechanisms designed to protect the system from extreme market conditions, price manipulation, and other potential risks. These features work together to ensure the protocol remains stable, secure, and reliable for all participants.

Protocol Safety Measures are a critical aspect of our protocol. We have implemented robust mechanisms to ensure the safety and stability of our platform, including Mark to Market valuation, Circuit Breaker, Minimum Collateral requirements, and Emergency Termination Procedure.

## What You'll Learn

- How Mark to Market provides realistic appraisal of financial positions
- How Circuit Breaker prevents price manipulation and extreme volatility
- How Base Price Adjustment maintains fair pricing during market stress
- How Emergency Global Settlement protects the protocol in extreme scenarios
- How these safety mechanisms work together to ensure system stability

## Key Components

- [**Mark to Market**](../../core-mechanics/liquidation/mark-to-market.md): Standard accounting practice for fair value assessment
- [**Circuit Breaker**](circuit-breaker/README.md): Limits price deviations to prevent manipulation
- [**Base Price Adjustment**](base-price-adjustment.md): Ensures fair pricing during market stress
- [**Emergency Global Settlement**](emergency-global-settlement.md): Protocol-wide safety mechanism for extreme scenarios

## Mark to Market

Mark to Market is a standard accounting practice adopted at Secured Finance, which entails recording the fair value of assets and liabilities, thereby providing a realistic appraisal of the financial health and the risk profile of positions on our platform. This practice is indispensable for maintaining transparency and accuracy in financial reporting, which in turn fosters trust and confidence among our users. The Mark to Market mechanism also plays a pivotal role in ensuring that the pricing of assets is aligned with the current market conditions, which is vital for effective risk management.

## Circuit Breaker

The Circuit Breaker is a protective mechanism used in the bond market to prevent excessive price movements and maintain stability. It is an automatic mechanism that temporarily suspends trading if there is a sudden and significant price movement. The Circuit Breaker is triggered when the price of bonds rises or falls beyond a certain pre-determined limit during one block.

For more details, see the [Circuit Breaker documentation](circuit-breaker/README.md).

## Minimum Collateral

The Minimum Collateral mechanism is a crucial safeguard designed to ensure that every position on our platform is sufficiently backed by collateral. This practice minimizes the risk of financial loss, both to the individual trader and the broader market, especially in volatile market conditions. By stipulating a minimum collateral requirement, we create a buffer against adverse market fluctuations, ensuring that positions remain solvent and the system resilient.

For more details, see the [Base Price Adjustment documentation](base-price-adjustment.md).

## Emergency Termination Procedure

Emergency termination is a crucial functionality designed to address unforeseen situations that could compromise the integrity of our protocol. This includes scenarios such as hacks or unexpected bugs. When this functionality is executed, all markets are immediately halted, and the protocol becomes non-operational. Users can then only redeem their positions and withdraw their tokens.

For more details, see the [Emergency Global Settlement documentation](emergency-global-settlement.md).

## Related Resources

- [Market Dynamics](../market-dynamics/README.md)
- [Orderbook Deep Dive](../orderbook-deep-dive/README.md)
- [Core Mechanics](../../core-mechanics/README.md)
