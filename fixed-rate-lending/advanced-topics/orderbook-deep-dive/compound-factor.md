---
description: Understanding how Compound Factors bridge Genesis and Future Values in the Fixed-Rate Lending Protocol
icon: 🔄
---

# 🔄 Compound Factor

## Overview

The Compound Factor is a value derived from the interest rate at the time one Orderbook reaches maturity and until the maturity of the next Orderbook. This value is determined by the Price Waterfall Mechanism during the Auto-roll process. In other words, the protocol continuously records a series of discount rates every three months.

By using the Compound Factor, you can calculate the value of the Genesis Date retrospectively. Conversely, it allows you to convert the Genesis Value into Future Value or present value.

## What You'll Learn

- How Compound Factors are calculated and used in the Fixed-Rate Lending Protocol
- The difference between Lending Compound Factor (LCF) and Borrowing Compound Factor (BCF)
- How Genesis Value (GV) is calculated for lenders and borrowers
- How to calculate Future Value (FV) using Compound Factors
- How Compound Factors contribute to efficient value calculation and transaction execution

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
_a: Additional Roll periods_

In essence, the GV serves as a reflection of your role (lender or borrower) and the changes in your obligations over time within the protocol.

### Future Value Calculation

To calculate your Future Value (FV), you simply need to multiply the Genesis Value (GV) by the Compound Factor from the lending side. This formula allows you to determine the projected value of your assets or obligations in the future, based on the current Genesis Value and the Compound Factor.

**Future Value (FV):**

$$
FV_{n} = GV_{n} \times LCF_{n}
$$

_n: Number of Rolls_

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Lending Compound Factor (LCF) | Factor used to calculate lender's future value | Calculated per formula |
| Borrowing Compound Factor (BCF) | Factor used to calculate borrower's future obligations | Calculated per formula |
| AutoRollPrice | Price at which auto-roll occurs | Determined by Price Waterfall Mechanism |
| AutoRollFeeRate | Fee rate applied during auto-roll | Protocol-defined percentage |
| Genesis Value (GV) | Initial value of an asset or obligation | Positive for lenders, negative for borrowers |
| Future Value (FV) | Projected value of an asset or obligation | Calculated as GV × LCF |

## Related Resources

- [Orderbook Deep Dive](README.md)
- [Genesis Value](genesis-value.md)
- [Orderbook Rotation](orderbook-rotation.md)
- [Auto-Rolling](../../market-dynamics/auto-rolling/README.md)
