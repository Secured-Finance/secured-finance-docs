---
description: Understanding the liquidation process through practical examples in the Fixed-Rate Lending Protocol
icon: 📋
---

# 📋 Case Study

## Overview

There are two main patterns that trigger liquidation in the Fixed-Rate Lending Protocol. One is when your collateral value decreases against your borrowed asset, typically represented by currency exchange rate fluctuations. The other is when the borrowed asset value increases compared to your collateral, which might occur when borrowing rates go lower. This case study explores these scenarios through practical examples.

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

## Examples

### Example 1: Liquidation Due to Exchange Rate Change

**Initial Position:**
- Alice deposits 10 ETH (worth $20,000) as collateral
- Alice borrows 12,000 USDC
- Initial LTV: 60% ($12,000 / $20,000)
- Liquidation threshold: 80%

**Market Change:**
- ETH price drops from $2,000 to $1,600 per ETH
- Collateral value decreases to $16,000 (10 ETH × $1,600)
- New LTV: 75% ($12,000 / $16,000)

**Further Market Change:**
- ETH price drops further to $1,500 per ETH
- Collateral value decreases to $15,000 (10 ETH × $1,500)
- New LTV: 80% ($12,000 / $15,000)
- Position becomes eligible for liquidation

**Liquidation Process:**
- 50% of the position is liquidated (6,000 USDC debt)
- Liquidator repays 6,000 USDC
- Alice loses 4.28 ETH as collateral (6,000 USDC × 1.07 penalty / $1,500 per ETH)
- Remaining position: 5.72 ETH collateral and 6,000 USDC debt
- Post-liquidation LTV: ~70% ($6,000 / ($1,500 × 5.72))

### Example 2: Liquidation Due to Interest Rate Changes

**Initial Position:**
- Charlie deposits 100,000 USDC as collateral
- Charlie borrows 10 BTC (worth $600,000 at $60,000 per BTC)
- Initial LTV: 60% ($600,000 / $1,000,000)

**Market Change:**
- BTC price increases to $75,000 per BTC
- Borrowed value increases to $750,000 (10 BTC × $75,000)
- New LTV: 75% ($750,000 / $1,000,000)

**Further Market Change:**
- BTC price increases to $80,000 per BTC
- Borrowed value increases to $800,000 (10 BTC × $80,000)
- New LTV: 80% ($800,000 / $1,000,000)
- Position becomes eligible for liquidation

**Liquidation Process:**
- 50% of the position is liquidated (5 BTC debt)
- Liquidator repays 5 BTC (worth $400,000)
- Charlie loses 42,800 USDC as collateral ($400,000 × 1.07 penalty)
- Remaining position: 57,200 USDC collateral and 5 BTC debt
- Post-liquidation LTV: ~70% ($400,000 / $57,200)

## FAQ

### What triggers a liquidation in the Fixed-Rate Lending Protocol?

Liquidations are triggered when a borrower's Loan-to-Value (LTV) ratio reaches or exceeds 80%. This can happen in two main ways:
1. When the value of the collateral decreases relative to the borrowed asset (e.g., collateral price drops)
2. When the value of the borrowed asset increases relative to the collateral (e.g., borrowed asset price rises)

### How much of my position gets liquidated if I reach the liquidation threshold?

When your position reaches the liquidation threshold, 50% of your borrowed amount will be liquidated. This partial liquidation approach helps to bring your position back to a safer LTV ratio (typically around 70%) while minimizing the amount of collateral you lose.

### What is the liquidation penalty and why does it exist?

The liquidation penalty is currently set at 7% of the liquidated debt value. This penalty serves several purposes:
1. It incentivizes liquidators to participate in the liquidation process
2. It discourages borrowers from taking excessive risk
3. It provides a buffer for the protocol against potential losses during volatile market conditions

### Can I prevent my position from being liquidated?

Yes, you can prevent liquidation by:
1. Adding more collateral to decrease your LTV ratio
2. Repaying part of your debt to decrease your LTV ratio
3. Monitoring market conditions and taking proactive action before reaching the liquidation threshold

### What happens to my remaining position after liquidation?

After liquidation, you will have:
1. 50% of your original borrowed amount remaining as debt
2. Your original collateral minus the amount taken during liquidation (including the 7% penalty)
3. A healthier LTV ratio (typically around 70%)
4. The ability to continue using the protocol with your remaining position

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

