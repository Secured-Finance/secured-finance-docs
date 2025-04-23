---
description: >-
  Understanding how Compound Factors bridge Genesis and Future Values in the
  Fixed-Rate Lending Protocol
---

# 🔄 Compound Factor

## Overview

The Compound Factor is a value derived from the interest rate at the time one Orderbook reaches maturity and until the maturity of the next Orderbook. This value is determined by the Price Waterfall Mechanism during the Auto-roll process. In other words, the protocol continuously records a series of discount rates every three months.

By using the Compound Factor, you can calculate the value of the Genesis Date retrospectively. Conversely, it allows you to convert the Genesis Value into Future Value or present value.

## How It Works

The Compound Factor mechanism is central to tracking and calculating values across different time periods in the protocol. It accounts for interest rates, fees, and the passage of time.

### Compound Factor Calculation

On the protocol, considering the fees, two types of Compound Factors for borrowers and lenders are continuously stored. Below are the formulas for each:

**Lending Compound Factor (LCF):**

$$
LCF_{n+1} = LCF_{n} \times (\frac{1}{AutoRollPrice_{n} } - AutoRollFeeRate)
$$

**Borrowing Compound Factor (BCF):**

$$
BCF_{n+1} = BCF_{n} \times (\frac{1}{AutoRollPrice_{n} } + AutoRollFeeRate)
$$

_n: Number of Rolls_

### Genesis Value Calculation

If you are a lender, the GV number will be positive and will remain the same. However, if you are a borrower of the asset, the GV will be negative, and your obligation will increase after each roll.

The GV for borrowers is calculated from the GV of lenders and Compound Factors. The calculation of Genesis Value (GV) for each user in our protocol is as follows:

**Genesis Value (GV):**

$$
GV_{n+a} =
\begin{cases}
GV_{n} & (GV_{n} \geq 0)\\
 GV_{n} + x & (GV_{n} < 0)
\end{cases}
\\[3mm]
x = GV_{n} \times (\frac{BCF_{n+a}}{BCF_{n}} \times \frac{LCF_{n}}{LCF_{n+a}} - 1)
$$

_n: Number of Rolls_\
&#xNAN;_&#x61;: Additional Roll periods_

In essence, the GV serves as a reflection of your role (lender or borrower) and the changes in your obligations over time within the protocol.

### Future Value Calculation

To calculate your Future Value (FV), you simply need to multiply the Genesis Value (GV) by the Compound Factor from the lending side. This formula allows you to determine the projected value of your assets or obligations in the future, based on the current Genesis Value and the Compound Factor.

**Future Value (FV):**

$$
FV_{n} = GV_{n} \times LCF_{n}
$$

_n: Number of Rolls_

## Key Parameters

| Parameter                       | Description                                            | Value                                        |
| ------------------------------- | ------------------------------------------------------ | -------------------------------------------- |
| Lending Compound Factor (LCF)   | Factor used to calculate lender's future value         | Calculated per formula                       |
| Borrowing Compound Factor (BCF) | Factor used to calculate borrower's future obligations | Calculated per formula                       |
| AutoRollPrice                   | Price at which auto-roll occurs                        | Determined by Price Waterfall Mechanism      |
| AutoRollFeeRate                 | Fee rate applied during auto-roll                      | Protocol-defined percentage                  |
| Genesis Value (GV)              | Initial value of an asset or obligation                | Positive for lenders, negative for borrowers |
| Future Value (FV)               | Projected value of an asset or obligation              | Calculated as GV × LCF                       |

## Examples

### Example 1: Calculating Compound Factors After Auto-Roll

Let's calculate how Compound Factors change after an Auto-Roll event:

1. Initial values before Auto-Roll:
   * Lending Compound Factor (LCF₀) = 1.05
   * Borrowing Compound Factor (BCF₀) = 1.07
   * Auto-Roll Price = 98.00
   * Auto-Roll Fee Rate = 0.001 (0.1%)
2.  Calculate the new Lending Compound Factor:

    ```
    LCF₁ = LCF₀ × (1/AutoRollPrice₀ - AutoRollFeeRate)
    LCF₁ = 1.05 × (1/0.98 - 0.001)
    LCF₁ = 1.05 × (1.0204 - 0.001)
    LCF₁ = 1.05 × 1.0194
    LCF₁ = 1.0704
    ```
3.  Calculate the new Borrowing Compound Factor:

    ```
    BCF₁ = BCF₀ × (1/AutoRollPrice₀ + AutoRollFeeRate)
    BCF₁ = 1.07 × (1/0.98 + 0.001)
    BCF₁ = 1.07 × (1.0204 + 0.001)
    BCF₁ = 1.07 × 1.0214
    BCF₁ = 1.0929
    ```
4. The updated Compound Factors after Auto-Roll are:
   * LCF₁ = 1.0704
   * BCF₁ = 1.0929

### Example 2: Calculating Genesis Value for a Borrower After Multiple Rolls

Let's calculate how a borrower's Genesis Value changes after multiple rolls:

1. Initial values:
   * Initial Genesis Value (GV₀) = -1000 (negative because it's a borrower)
   * Initial Lending Compound Factor (LCF₀) = 1.00
   * Initial Borrowing Compound Factor (BCF₀) = 1.00
   * After 2 rolls: LCF₂ = 1.06, BCF₂ = 1.08
2.  Calculate the adjustment factor x:

    ```
    x = GV₀ × (BCF₂/BCF₀ × LCF₀/LCF₂ - 1)
    x = -1000 × (1.08/1.00 × 1.00/1.06 - 1)
    x = -1000 × (1.08 × 0.9434 - 1)
    x = -1000 × (1.0189 - 1)
    x = -1000 × 0.0189
    x = -18.9
    ```
3.  Calculate the new Genesis Value:

    ```
    GV₂ = GV₀ + x
    GV₂ = -1000 + (-18.9)
    GV₂ = -1018.9
    ```
4. The borrower's Genesis Value has increased in magnitude to -1018.9, reflecting the increased obligation due to interest accrual.

### Example 3: Calculating Future Value Using Compound Factors

Let's calculate the Future Value for both a lender and a borrower:

1.  For a lender with GV = 500 and current LCF = 1.12:

    ```
    FV = GV × LCF
    FV = 500 × 1.12
    FV = 560
    ```

    The lender's Future Value is 560, representing their initial investment plus accrued interest.
2.  For a borrower with GV = -800 and current LCF = 1.12:

    ```
    FV = GV × LCF
    FV = -800 × 1.12
    FV = -896
    ```

    The borrower's Future Value is -896, representing their debt obligation including accrued interest.

## Common Questions

### How do Compound Factors differ from traditional interest rates?

Compound Factors differ from traditional interest rates in several ways:

1. **Cumulative Nature**: Compound Factors accumulate over time, representing the total growth factor since inception
2. **Protocol-Specific**: They are specifically designed for the Fixed-Rate Lending Protocol's auto-rolling mechanism
3. **Dual Factors**: The protocol maintains separate factors for lenders and borrowers to account for fees
4. **Value Calculation**: They directly translate Genesis Values to Future Values without requiring complex calculations
5. **Efficiency**: They enable efficient on-chain calculations with minimal computational overhead

### Why are there separate Compound Factors for lenders and borrowers?

Separate Compound Factors exist for several reasons:

1. **Fee Incorporation**: The difference accounts for protocol fees that create a spread between lending and borrowing rates
2. **Risk Management**: The spread helps cover potential defaults and maintain protocol solvency
3. **Protocol Revenue**: Part of the spread contributes to protocol revenue and sustainability
4. **Market Efficiency**: The dual factors create a transparent pricing mechanism for the lending market
5. **Accurate Accounting**: Separate factors ensure precise tracking of obligations for both sides of the market

### How do Compound Factors change during market stress?

During market stress, Compound Factors may be affected in these ways:

1. **Auto-Roll Price Impact**: Market volatility can lead to higher or lower Auto-Roll prices, affecting the Compound Factor calculation
2. **Fee Adjustments**: The protocol might adjust Auto-Roll fee rates in response to market conditions
3. **Governance Intervention**: In extreme cases, governance might implement emergency measures affecting Compound Factors
4. **Liquidity Effects**: Reduced liquidity can lead to wider spreads between lending and borrowing Compound Factors
5. **Circuit Breaker Activation**: If circuit breakers are triggered, this may affect the Auto-Roll price determination

### What happens to Compound Factors if I enter the market between Auto-Rolls?

When entering the market between Auto-Rolls:

1. **Immediate Application**: The current Compound Factors apply to your position immediately
2. **Pro-Rated Interest**: You effectively receive or pay interest based on the time remaining until the next Auto-Roll
3. **Genesis Value Calculation**: Your Genesis Value is calculated based on the current market price and Compound Factors
4. **Future Value Projection**: Your Future Value is calculated using the current Compound Factors
5. **Next Roll Impact**: Your position will be subject to the next Auto-Roll like all other positions

### How do Compound Factors ensure fair interest distribution?

Compound Factors ensure fair interest distribution through:

1. **Transparent Calculation**: The formula is transparent and applied consistently to all participants
2. **Market-Driven Rates**: Auto-Roll prices are determined by market forces, ensuring rates reflect supply and demand
3. **Continuous Tracking**: The protocol continuously tracks and updates Compound Factors
4. **Proportional Application**: Interest is applied proportionally to all positions based on their Genesis Values
5. **Historical Record**: The protocol maintains a historical record of all Compound Factors for accurate accounting

## Related Resources

* [Orderbook Deep Dive](./)
* [Genesis Value](genesis-value.md)
* [Orderbook Rotation](orderbook-rotation.md)
* [Auto-Rolling](../../market-dynamics/auto-rolling/)
