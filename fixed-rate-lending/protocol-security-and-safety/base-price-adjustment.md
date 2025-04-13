---
description: Secure Assets and Protocol
---

# 🪄 Base Price Adjustment

In the case of Zero Coupon Bonds, which begin trading at a significant discount and mature at par value (100 on our platform), borrowers are required to progressively increase their collateral over time.

**To safeguard borrowers from the risk of liquidation, while also minimizing insolvency risks for our protocol, we mandate a minimum collateral requirement that varies based on the currency and the duration of the loan.**

To secure user assets and protect the protocol from market exploitation, we introduce the <mark style="color:red;">minimum collateral base price</mark> (**Base Price: BP**). It will be used to calculate the required collateral for borrowers such that the input bond price is lower than the BP.&#x20;

The BP is determined according to the following formula and pre-set reference base prices, categorized by the asset's yield range. It is an interpolated value with the corresponding duration of the bonds **t: time to maturity**, using two reference base prices, BP at Maturity and BP of 1y Duration.

#### Formulaic:&#x20;

$$
BP(t) = P_{M} - t/(secondsPerYear) * (P_{M} - P_{1Y})
$$

<table data-header-hidden><thead><tr><th width="239"></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>BP (t)</td><td>Minimum collateral required base price </td><td></td></tr><tr><td>P_M</td><td>Reference Base Price at Maturity (0y Duration)</td><td></td></tr><tr><td>P_1Y</td><td>Reference Base Price of 1y Duration</td><td></td></tr><tr><td>t</td><td>Time to maturity in seconds</td><td></td></tr><tr><td>secondsPerYear</td><td>365 * 24 * 60 * 60</td><td></td></tr></tbody></table>



<table><thead><tr><th width="123" align="center">Category</th><th width="185" align="center">Yield range</th><th width="207" align="center">BP at Maturity</th><th align="center">BP of 1y Duration</th></tr></thead><tbody><tr><td align="center">A</td><td align="center">0%~3%</td><td align="center">96.00</td><td align="center">93.00</td></tr><tr><td align="center">B</td><td align="center">3%~5%</td><td align="center">96.00</td><td align="center">91.00</td></tr><tr><td align="center">C</td><td align="center">5%~7.5%</td><td align="center">96.00</td><td align="center">89.00</td></tr><tr><td align="center">D</td><td align="center">7.5%~10%</td><td align="center">96.00</td><td align="center">87.00</td></tr><tr><td align="center">E</td><td align="center">10%~15%</td><td align="center">96.00</td><td align="center">84.00</td></tr><tr><td align="center">F</td><td align="center">15%~</td><td align="center">96.00</td><td align="center">81.00</td></tr></tbody></table>

### Example:&#x20;

1\) Category A, 0.25y Duration:&#x20;

$$
BP(0.25y) = 96.00 - 0.25y/1y * (96.00-93.00) = 95.25
$$

2\) Category C, 1.0 Duration:&#x20;

$$
BP(1y) = 96.00 - 1y/1y * (96.00-89.00) = 89.00
$$

3\) Category F, 1.5y Duration:&#x20;

$$
BP(1.5y) = 96.00 - 1.5y/1y * (96.00-81.00) = 73.50
$$

{% hint style="info" %}
In the examples above, we simplified the calculations by using annualized Duration. However, it's important to note that the actual calculations for our contract are based on seconds.
{% endhint %}

### Setting Category

Category will be set depending on the APR of the currency.

#### Current Category

<table><thead><tr><th width="120">Currency</th><th width="110" align="center">Category</th><th data-hidden></th></tr></thead><tbody><tr><td>BTC</td><td align="center">A</td><td></td></tr><tr><td>ETH</td><td align="center">B</td><td></td></tr><tr><td>FIL</td><td align="center">F</td><td></td></tr><tr><td>USDFC</td><td align="center">C</td><td></td></tr><tr><td>USDC</td><td align="center">C</td><td></td></tr></tbody></table>



We review the category in quarterly basis and revise if needed with community vote on the APR movement during the observing period.
