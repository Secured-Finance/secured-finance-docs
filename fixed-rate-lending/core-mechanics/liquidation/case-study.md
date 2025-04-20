---
description: Understanding the liquidation process through practical examples in the Fixed-Rate Lending Protocol
icon: 📋
---

# 📋 Case Study

## Overview

There would be 2 main patterns that trigger the liquidation. One is your collateral value decrease against your borrowed asset. The currency exchange rate represents this. The other is the borrowed asset value increase compared to your collateral. This might occur when the borrowing rates go lower.&#x20;

## What You'll Learn

- How collateral value decreases can trigger liquidation
- How borrowed asset value increases can trigger liquidation
- How the liquidation process works in practice
- How LTV (Loan-to-Value) ratios are calculated before and after liquidation
- How liquidation penalties are applied to borrower positions

## How It Works

Let's examine a practical example of how liquidation works in the Fixed-Rate Lending Protocol:

### Example Scenario

Bob borrowed 1,000 FIL with 15,000 USDC for 1y (365 days) at 20% at FILUSDC 10.0. Hence Bob's borrowed value is 10,000 USDC (= 1,000 FIL \* 10.0 FILUSDC FX rate), and his LTV is 66.7% (10,000/15,000).&#x20;

### Liquidation Trigger

IF the FILUSDC exchange rate spike to 12.0 from 10.0 right after he borrowed, the value of his collateral decreases against his liability. In other words, his liability increased to 12,000 USDC (=1,000 FIL \* 12.0 FILUSDC FX rate). As a result, 50% of his position will be subject to liquidation since LTV reached 80% (12,000/15,000).&#x20;

### Liquidation Process

Our Smart-contract will repay half of his obligation, helped by the liquidator, which is 500 FIL. Instead, Bob will lose his collateral of 6,420 USDC (=500 FIL \* 12.0 FILUSDC FX rate \* 107% penalty).&#x20;

### Post-Liquidation Position

After the liquidation process, Bob's position will be 500 FIL cash, 500 FIL borrowed with 8,580 USDC collateral (15,000 - 6,420 USDC). His LTV recovered to 69.9% (=500 FIL \* 12.0 FILUSDC FX rate / 8,580 collateral).

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Liquidation Threshold | LTV ratio at which a position becomes eligible for liquidation | 80% |
| Liquidation Penalty | Additional fee applied to liquidated collateral | 7% |
| Liquidation Amount | Portion of the position that gets liquidated when threshold is reached | 50% |
| Post-Liquidation Target | Target LTV ratio after liquidation | ~70% |
| Exchange Rate Impact | How exchange rate changes affect LTV calculations | Direct impact on borrowed value |


{% embed url="http://www.plantuml.com/plantuml/png/RL9TRu8m57tlhxWnCT644J3JAG-BWMN9acOFulPUuSgQb9QLglFVxu8IQxOdeEVZt7lekdN2kaEjM4DFMSX6Q0UZrEn685f8xu_pchuWCzfPKRYUaMVt52w_3x8KpjWUveobyF1Cj0HIOwqvGHn4KGIlRnmccL5AEBH29H3F-_EF_2MRCdANHq8w-pph3D91ZwNlmBUV2ImMuTDuoahqPKmRUZ57j906VJu9EdV0d-9Bw0h1TbIf2ukYnHRsrjGGHs44pa0y2oDlzdSy0MN1P4du-By1UG9RAwkAyjIr0saqx8s5-MNQcuWpFXXli17dWU4t0WrgeToPrWiUPqCntexyrWpt0WjJDme9dsom5b9BNS7ksbmo10Lm0mll9oo3-V8I5GmhK_ugNFsfTuswf6lp2m00" %}

## Related Resources

- [Liquidation](README.md)
- [Mark to Market](mark-to-market.md)
- [Collateralization](../../collateralization.md)
- [Safety Measures](../../../advanced-topics/safety-measures/README.md)

