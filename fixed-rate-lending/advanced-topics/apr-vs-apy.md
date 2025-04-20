---
description: Understanding the difference between Annual Percentage Rate and Annual Percentage Yield
icon: 📊
---

# 📊 APR vs APY

## Overview

APR (Annual Percentage Rate) and APY (Annual Percentage Yield) are two common measures of interest rates that are used in the DeFi loan and deposit markets. While they may seem similar, there are key differences between them, particularly in how they account for compounding interest.

## What You'll Learn

- The difference between APR and APY in interest rate calculations
- How compounding affects interest rate calculations
- How to convert between APR and APY
- Why the Fixed-Rate Lending Protocol uses APR rather than APY
- How these concepts apply in practical lending scenarios

## What is APY?

APY stands for Annual Percentage Yield, which is a measure of the interest earned on a deposit or investment over a year, taking into account the effect of **compounding** interest.

## How about APR?

APR is the interest rate that is charged on a loan or credit card balance. It is the annual rate of interest that is applied to the outstanding balance on the loan, expressed as a percentage. The APR does **not** take **compounding** into account.

## Examples

### Example 1: Comparing APR and APY for a 6-Month Loan

Bob lends 100 USD with a fixed rate of 10% for 6 months. How much will he earn after 6 months?

#### With 10% APR:

<div align="left"><figure><img src="../../.gitbook/assets/image (47).png" alt="" width="349"><figcaption><p>APR Calculation for 6-Month Loan</p></figcaption></figure></div>

He earns 5% interest for 6 months (half of the annual 10% rate), and his future value will be 105 USD, meaning he earns 5 dollars.

#### With 10% APY:

In case this 10% APY is compounded every 6 months, the relationship between 10% APY and the equivalent APR 'r' would be:

<div align="left"><figure><img src="../../.gitbook/assets/image (48).png" alt="" width="563"><figcaption><p>APY to APR Conversion Formula</p></figcaption></figure></div>

Hence his 100 USD will grow to 104.88 USD, meaning he earns 4.88 dollars.

### Example 2: Different Compounding Frequencies

Let's examine how different compounding frequencies affect the effective yield on a 12% APR loan of 1,000 USD for one year:

| Compounding Frequency | Calculation | Final Amount | Effective APY |
|-----------------------|-------------|--------------|---------------|
| Annual (1×) | 1,000 × (1 + 0.12) | 1,120.00 USD | 12.00% |
| Semi-annual (2×) | 1,000 × (1 + 0.12/2)² | 1,123.60 USD | 12.36% |
| Quarterly (4×) | 1,000 × (1 + 0.12/4)⁴ | 1,125.51 USD | 12.55% |
| Monthly (12×) | 1,000 × (1 + 0.12/12)¹² | 1,126.83 USD | 12.68% |
| Daily (365×) | 1,000 × (1 + 0.12/365)³⁶⁵ | 1,127.47 USD | 12.75% |
| Continuous | 1,000 × e^(0.12) | 1,127.50 USD | 12.75% |

This example demonstrates that more frequent compounding results in a higher effective yield (APY) for the same stated APR.

### Example 3: Converting Between APR and APY

To convert between APR and APY:

**From APR to APY:**
```
APY = (1 + APR/n)^n - 1
```
Where n is the number of compounding periods per year.

**From APY to APR:**
```
APR = n × ((1 + APY)^(1/n) - 1)
```

For example, with monthly compounding (n=12):
- A 12% APR yields an APY of (1 + 0.12/12)^12 - 1 = 12.68%
- A 12% APY corresponds to an APR of 12 × ((1 + 0.12)^(1/12) - 1) = 11.39%

## How It Works

The difference between APR and APY lies in how they account for compounding:

1. **APR (Annual Percentage Rate)** is a simple interest rate calculated by multiplying the periodic rate by the number of periods in a year. It does not account for compounding effects.

2. **APY (Annual Percentage Yield)** accounts for compounding by calculating the effective annual rate of return. It represents the actual return you would receive after accounting for the effects of compounding.

The mathematical relationship between APR and APY is:

$$
APY = \left(1 + \frac{APR}{n}\right)^n - 1
$$

Where n is the number of compounding periods per year.

{% hint style="info" %}
The use of APY is widespread in DeFi projects because of the variable nature of their quoted interest, leading to the representation of compounded interest. APY assumes that the current variable rate remains constant for the next 365 days and compounds daily. Moreover, fixed-term projects that depend on variable rates as their underlying interest rate also utilize APY.

However, adhering to the prevailing market conventions, our protocol naturally displays APR rather than APY.
{% endhint %}

## FAQ

### Why does the Fixed-Rate Lending Protocol use APR instead of APY?

The Fixed-Rate Lending Protocol uses APR for several reasons:
1. **Market Convention**: Fixed-rate markets traditionally quote rates as APR, making it easier for traditional finance participants to understand
2. **Simplicity**: APR provides a straightforward calculation without the complexity of compounding assumptions
3. **Transparency**: With fixed terms, the exact return is known upfront without needing to make assumptions about reinvestment
4. **Consistency**: Using APR allows for direct comparison between different maturity periods
5. **Zero-Coupon Bond Structure**: Our protocol uses Zero-Coupon Bonds which naturally align with APR calculations

### How do I compare rates between protocols that use different conventions?

To compare rates between protocols:
1. **Identify the Convention**: Determine whether each protocol quotes rates as APR or APY
2. **Convert to the Same Basis**: Use the conversion formulas to convert all rates to either APR or APY
3. **Consider Compounding Frequency**: Take into account how often interest is compounded in each protocol
4. **Account for Term Length**: For fixed-term protocols, consider the duration of the investment
5. **Factor in Additional Rewards**: Some protocols offer additional token rewards that aren't reflected in the quoted rates

### Does compounding frequency matter for Zero-Coupon Bonds?

For Zero-Coupon Bonds:
1. **No Periodic Payments**: Zero-Coupon Bonds don't make periodic interest payments, so traditional compounding doesn't apply
2. **Implicit Compounding**: The discount at which the bond is purchased implicitly accounts for the time value of money
3. **APR Representation**: The yield is typically expressed as an APR based on the purchase price and face value
4. **Single Payment at Maturity**: Investors receive the full face value at maturity, with no reinvestment decisions needed
5. **Direct Comparison**: This structure allows for direct comparison of rates across different maturity periods

### What happens if I withdraw before maturity in a fixed-rate protocol?

If you withdraw before maturity:
1. **Market Price Exposure**: You'll need to sell your position at the current market price, which may be higher or lower than your entry price
2. **Yield Calculation Changes**: Your actual yield will be determined by the price at which you sell, not the original APR
3. **No Guaranteed Rate**: The guaranteed rate only applies if you hold until maturity
4. **Potential Slippage**: Depending on market liquidity, you may experience slippage when exiting your position
5. **Transaction Costs**: Additional fees may apply when closing a position early

### How does inflation affect APR and APY?

Inflation affects both APR and APY in similar ways:
1. **Real Returns**: To calculate real returns, subtract the inflation rate from the nominal APR or APY
2. **Purchasing Power**: Higher inflation reduces the purchasing power of your returns
3. **Fixed vs. Variable Rates**: Fixed rates provide certainty but may not adjust for changing inflation
4. **Term Premium**: Longer-term fixed rates typically include a premium to account for inflation uncertainty
5. **Inflation-Protected Options**: Some protocols offer inflation-protected options that adjust returns based on inflation metrics

## Key Parameters

| Parameter | Description | Relevance to Protocol |
|-----------|-------------|----------------------|
| Compounding Frequency | How often interest is compounded | N/A for Zero-Coupon Bonds |
| Term Length | Duration of the investment | Determines the fixed rate period |
| Nominal Rate | Stated interest rate before compounding | Used in APR calculations |
| Effective Rate | Actual yield after accounting for compounding | Equivalent to APY |
| Day Count Convention | Method of calculating days for interest accrual | Actual/365 used in protocol |
| Reinvestment Assumption | Assumption about reinvesting proceeds | Auto-rolling handles reinvestment |
| Market Convention | Standard way rates are quoted in a market | Protocol follows fixed-income market conventions |

## Related Resources

- [Discount Factor](discount-factor.md)
- [ZC Bond Price to APR](zc-bond-price-to-apr.md)
- [Market Dynamics](market-dynamics/README.md)
- [Auto-Rolling](market-dynamics/auto-rolling/README.md)
