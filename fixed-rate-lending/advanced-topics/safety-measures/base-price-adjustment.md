---
description: A mechanism that ensures fair pricing and adequate collateralization during market stress
icon: 🪄
---

# 🪄 Base Price Adjustment

## Overview

In the case of Zero Coupon Bonds, which begin trading at a significant discount and mature at par value (100 on our platform), borrowers are required to progressively increase their collateral over time.

**To safeguard borrowers from the risk of liquidation, while also minimizing insolvency risks for our protocol, we mandate a minimum collateral requirement that varies based on the currency and the duration of the loan.**

## How It Works

To secure user assets and protect the protocol from market exploitation, we introduce the <mark style="color:red;">minimum collateral base price</mark> (**Base Price: BP**). It will be used to calculate the required collateral for borrowers such that the input bond price is lower than the BP.&#x20;

The BP is determined according to the following formula and pre-set reference base prices, categorized by the asset's yield range. It is an interpolated value with the corresponding duration of the bonds **t: time to maturity**, using two reference base prices, BP at Maturity and BP of 1y Duration.

#### Formulaic:&#x20;

$$
BP(t) = P_{M} - t/(secondsPerYear) * (P_{M} - P_{1Y})
$$

<table data-header-hidden><thead><tr><th width="239"></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>BP (t)</td><td>Minimum collateral required base price </td><td></td></tr><tr><td>P_M</td><td>Reference Base Price at Maturity (0y Duration)</td><td></td></tr><tr><td>P_1Y</td><td>Reference Base Price of 1y Duration</td><td></td></tr><tr><td>t</td><td>Time to maturity in seconds</td><td></td></tr><tr><td>secondsPerYear</td><td>365 * 24 * 60 * 60</td><td></td></tr></tbody></table>



<table><thead><tr><th width="123" align="center">Category</th><th width="185" align="center">Yield range</th><th width="207" align="center">BP at Maturity</th><th align="center">BP of 1y Duration</th></tr></thead><tbody><tr><td align="center">A</td><td align="center">0%~3%</td><td align="center">96.00</td><td align="center">93.00</td></tr><tr><td align="center">B</td><td align="center">3%~5%</td><td align="center">96.00</td><td align="center">91.00</td></tr><tr><td align="center">C</td><td align="center">5%~7.5%</td><td align="center">96.00</td><td align="center">89.00</td></tr><tr><td align="center">D</td><td align="center">7.5%~10%</td><td align="center">96.00</td><td align="center">87.00</td></tr><tr><td align="center">E</td><td align="center">10%~15%</td><td align="center">96.00</td><td align="center">84.00</td></tr><tr><td align="center">F</td><td align="center">15%~</td><td align="center">96.00</td><td align="center">81.00</td></tr></tbody></table>

## Key Parameters

| Parameter | Description | Default Value |
|-----------|-------------|---------------|
| BP at Maturity | Reference Base Price at maturity (0y Duration) | 96.00 |
| BP of 1y Duration | Reference Base Price at 1 year duration | Varies by category (81.00-93.00) |
| Category Review Period | How often categories are reviewed | Quarterly |
| Category Assignment | How currencies are assigned to yield categories | Based on APR range |
| Interpolation Method | How BP is calculated between reference points | Linear interpolation |
| Time Unit | Base time unit for calculations | Seconds |

## Examples

### Example 1: Calculating Base Price for Short-Term Bonds

For a Category A bond (0-3% yield range) with 0.25 years to maturity:

$$
BP(0.25y) = 96.00 - 0.25y/1y * (96.00-93.00) = 95.25
$$

This means that for this short-term bond, the minimum collateral base price is 95.25. Any borrowing against this bond would use this value to calculate the required collateral, ensuring adequate protection as the bond approaches maturity.

### Example 2: Calculating Base Price for Medium-Term Bonds

For a Category C bond (5-7.5% yield range) with exactly 1 year to maturity:

$$
BP(1y) = 96.00 - 1y/1y * (96.00-89.00) = 89.00
$$

This medium-term bond has a lower base price of 89.00, reflecting the higher yield and longer duration. Borrowers would need to maintain collateral based on this value to avoid liquidation.

### Example 3: Calculating Base Price for Long-Term Bonds

For a Category F bond (15%+ yield range) with 1.5 years to maturity:

$$
BP(1.5y) = 96.00 - 1.5y/1y * (96.00-81.00) = 73.50
$$

This long-term, high-yield bond has a significantly lower base price of 73.50, reflecting the higher risk and longer time to maturity. Borrowers using this bond as collateral would need to be particularly vigilant about maintaining adequate collateralization.

{% hint style="info" %}
In the examples above, we simplified the calculations by using annualized Duration. However, it's important to note that the actual calculations for our contract are based on seconds.
{% endhint %}

### Setting Category

Category will be set depending on the APR of the currency.

#### Current Category

<table><thead><tr><th width="120">Currency</th><th width="110" align="center">Category</th><th data-hidden></th></tr></thead><tbody><tr><td>BTC</td><td align="center">A</td><td></td></tr><tr><td>ETH</td><td align="center">B</td><td></td></tr><tr><td>FIL</td><td align="center">F</td><td></td></tr><tr><td>USDFC</td><td align="center">C</td><td></td></tr><tr><td>USDC</td><td align="center">C</td><td></td></tr></tbody></table>



We review the category in quarterly basis and revise if needed with community vote on the APR movement during the observing period.

## FAQ

### Why is Base Price Adjustment necessary?

Base Price Adjustment is necessary for several important reasons:
1. **Protection Against Liquidation**: It protects borrowers from unexpected liquidations as bond prices naturally approach par value near maturity
2. **Risk Management**: It ensures the protocol maintains adequate collateralization as market conditions change
3. **Price Manipulation Prevention**: It prevents malicious actors from manipulating prices to trigger unfair liquidations
4. **Market Stability**: It contributes to overall market stability by setting reasonable minimum collateral requirements
5. **Yield Curve Alignment**: It aligns collateral requirements with the natural yield curve of different assets

### How are yield categories determined?

Yield categories are determined through the following process:
1. **Historical Analysis**: Analysis of historical yield ranges for each supported asset
2. **Market Benchmarks**: Comparison with market benchmarks and similar assets
3. **Risk Assessment**: Evaluation of the asset's volatility and liquidity characteristics
4. **Protocol Governance**: Final approval through protocol governance mechanisms
5. **Quarterly Review**: Regular review and potential adjustment based on market conditions

### What happens if market yields change significantly between quarterly reviews?

If market yields change significantly between quarterly reviews:
1. **Emergency Review**: Protocol governance can initiate an emergency review if necessary
2. **Gradual Adjustment**: Any changes to categories are typically implemented gradually
3. **Safety Buffer**: The category system includes built-in buffers to accommodate some yield fluctuation
4. **Monitoring Systems**: Continuous monitoring alerts governance to significant deviations
5. **User Communication**: Users are notified of any potential category changes in advance

### How does Base Price affect my borrowing position?

Base Price affects your borrowing position in several ways:
1. **Minimum Collateral**: It determines the minimum amount of collateral you must maintain
2. **Liquidation Threshold**: It influences when your position becomes eligible for liquidation
3. **Borrowing Capacity**: It affects how much you can borrow against your collateral
4. **Position Management**: You may need to add more collateral as maturity approaches
5. **Risk Exposure**: Lower Base Price (higher category) means higher collateral requirements

### Can I predict how my collateral requirements will change over time?

Yes, you can predict collateral requirement changes:
1. **Formula Transparency**: The Base Price formula is publicly available and deterministic
2. **Time-Based Calculation**: Requirements change based on time to maturity, which is known
3. **Category Stability**: Categories typically remain stable during the quarterly periods
4. **Simulation Tools**: The protocol provides tools to simulate future collateral requirements
5. **Advance Notice**: Any category changes are announced in advance through governance

## Related Resources

- [Safety Measures](README.md)
- [Circuit Breaker](circuit-breaker/README.md)
- [Emergency Global Settlement](emergency-global-settlement.md)
- [Minimum Collateral](../../../core-mechanics/collateralization.md)
