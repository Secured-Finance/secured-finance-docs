---
description: Understanding how Zero-Coupon Bond prices are converted to Annual Percentage Rates
icon: ➗
---

# ➗ ZC Bond Price to APR

## Overview

On our platform, the execution of bond transactions is determined by the bond price. However, we recognize that users may find it more convenient to reference the Annual Percentage Rate (APR) when assessing yields. To accommodate this, we provide the APR as a reference rate, which is based on a linear calculation up to a 1-year tenor using an Act/365 basis. For tenors exceeding 1 year, we utilize annual compounding to determine the yield.

## How It Works

The conversion between Zero-Coupon Bond prices and Annual Percentage Rates (APR) is a fundamental calculation in our platform. The method varies depending on the maturity period of the bond.

{% hint style="info" %}
**What is Act/365?**

Act/365 is a day count convention used in bond math to calculate the accrued interest on a bond. It stands for Actual/365 and is also known as the Actual/365 Fixed convention.

Note that the Act/365 convention assumes a fixed year of 365 (or 366) days, regardless of the actual number of days in the year. This is different from other day count conventions, such as the 30/360 convention, which assumes a fixed 30-day month and a 360-day year.
{% endhint %}

### Bonds with Maturity Less Than 1 Year

For Zero-Coupon Bonds with maturities less than one year, we use a linear calculation with the Act/365 day count convention:

$$
FV = PV * (1 + r*Act/365)
$$

Where:
* PV: Present Value
* FV: Future Value
* r: APR (Annual Percentage Rate)
* Act: Actual duration to Maturity in days

As an inherent characteristic of the ZC bond market, the present value (PV) of a bond is equivalent to its bond price, while the future value (FV) is fixed at 100, as per the design of our protocol. Duration is calculated using the seconds to maturity compared to seconds per year, enabled by our smart contract technology.

To calculate APR from the bond price:

$$
APR = (100/BondPrice - 1)*secondsPerYear/secondsToMaturity
$$

Where:
* secondsPerYear: 365 \* 24 \* 60 \* 60 = 31,536,000

### Bonds with Maturity Greater Than 1 Year

For Zero-Coupon Bonds with maturities greater than one year, we use annual compounding:

$$
FV = PV *(1 + r)^n
$$

Where:
* PV: Present Value
* FV: Future Value
* r: APR (Annual Percentage Rate)
* n: Years to Maturity

Similar to the formulaic approach for tenors less than 1 year, the present value (PV) of a bond equals its bond price, while the future value (FV) remains fixed at 100, in accordance with our protocol design.

To calculate APR from the bond price:

$$
APR =(100/BondPrice)^{(1/YearsToMaturity)}-1
$$

Where:
* Years to Maturity: Seconds to Maturity/Seconds Per Year

### During Pre-Open Period

The pre-open period is a specific time frame before the official opening of a new bond market. During this period, we invite users to place their orders in the pre-open order book. This allows market participants to gauge interest and liquidity before the market officially starts. For more detailed explanation, please visit [Fair Price Discovery](market-dynamics/new-market-listing-and-delisting/itayose-fair-price-discovery.md).

During the pre-open period, the APR displayed is based on the estimated 'opening price' at the time the market starts. It's important to note that the APR is not calculated from the spot date to the end of maturity. Instead, it is calculated from the start trading date to the end of maturity.

{% hint style="info" %}
The formula for APR during the pre-open period would be similar to the existing APR calculation, but the 'Actual duration to Maturity' (Act) and 'Years to Maturity' would be replaced by the 'Actual Bond Duration from Start Trading Date to End of Maturity' and 'PV' will be 'estimated opening price'.
{% endhint %}

## Key Parameters

| Parameter | Description | Impact on APR Calculation |
|-----------|-------------|---------------------------|
| Bond Price | Current market price of the Zero-Coupon Bond | Lower price → Higher APR |
| Time to Maturity | Time remaining until the bond matures | Shorter maturity → Different calculation method |
| Day Count Convention | Method for counting days (Act/365) | Standardizes time calculation |
| Calculation Method | Linear vs. Compounding based on maturity | Affects APR for different time horizons |
| Pre-Open Status | Whether the bond is in pre-open period | Changes time basis for calculation |
| Seconds Per Year | Standard time basis (31,536,000 seconds) | Standardizes annualization |

## Examples

### Example 1: Calculating APR for a 3-Month Bond

Let's calculate the APR for a 3-month Zero-Coupon Bond with a price of 98.50:

1. Since the maturity is less than 1 year, we use the linear calculation formula
2. Calculate seconds to maturity: 3 months = 90 days = 7,776,000 seconds
3. Apply the APR formula:
   ```
   APR = (100/98.50 - 1) * 31,536,000/7,776,000
   APR = (1.0152 - 1) * 4.0552
   APR = 0.0152 * 4.0552
   APR = 0.0617 or 6.17%
   ```
4. This means a bond priced at 98.50 with 3 months to maturity has an implied APR of 6.17%

### Example 2: Calculating APR for an 18-Month Bond

For an 18-month Zero-Coupon Bond with a price of 85.00:

1. Since the maturity is greater than 1 year, we use the annual compounding formula
2. Calculate years to maturity: 18 months = 1.5 years
3. Apply the APR formula:
   ```
   APR = (100/85.00)^(1/1.5) - 1
   APR = (1.1765)^(0.6667) - 1
   APR = 1.1122 - 1
   APR = 0.1122 or 11.22%
   ```
4. This means a bond priced at 85.00 with 18 months to maturity has an implied APR of 11.22%

### Example 3: APR During Pre-Open Period

During a pre-open period for a new 6-month Zero-Coupon Bond:

1. The estimated opening price based on current orders is 97.00
2. The bond will start trading in 5 days
3. The actual duration from start trading to maturity is 175 days (180 - 5)
4. Apply the modified APR formula:
   ```
   APR = (100/97.00 - 1) * 365/175
   APR = (1.0309 - 1) * 2.0857
   APR = 0.0309 * 2.0857
   APR = 0.0644 or 6.44%
   ```
5. During the pre-open period, this bond would display an estimated APR of 6.44%

## Common Questions

### Why does Secured Finance use different calculation methods for different maturities?

We use different calculation methods for different maturities because:
1. **Market Convention**: This approach aligns with standard market practices in traditional finance
2. **Accuracy**: Linear calculations are simpler and sufficiently accurate for short-term bonds
3. **Compounding Effects**: For longer maturities, compounding effects become more significant
4. **Yield Curve Representation**: Different methods better represent the yield curve across various time horizons
5. **User Expectations**: Users familiar with traditional finance expect these calculation methods

### How does the APR calculation relate to the actual yield I'll receive?

The relationship between APR and actual yield:
1. **Exact Return**: For bonds held to maturity, your actual return will be exactly as calculated (bond price to 100)
2. **Annualized Representation**: APR standardizes returns to an annual basis for comparison
3. **No Compounding Assumption**: APR doesn't account for reinvestment of returns (unlike APY)
4. **Trading Impact**: If you sell before maturity, market conditions will determine your actual return
5. **Fee Consideration**: Transaction fees are not included in the APR calculation

### Can I compare APRs across different maturity periods?

Yes, you can compare APRs across different maturity periods:
1. **Standardized Basis**: APR converts all returns to an annual basis, enabling comparison
2. **Yield Curve Analysis**: Comparing APRs across maturities reveals the yield curve shape
3. **Risk Assessment**: Higher APRs for longer maturities typically indicate higher risk premiums
4. **Investment Strategy**: Comparing APRs helps determine optimal investment horizons
5. **Market Expectations**: Differences in APRs across maturities reflect market expectations for future rates

### Why might the APR change during the pre-open period?

The APR might change during the pre-open period due to:
1. **Order Flow**: New orders affect the estimated opening price, which changes the APR
2. **Market Sentiment**: Shifting market sentiment can alter bidding patterns
3. **External Factors**: News or events during the pre-open period may influence pricing
4. **Liquidity Dynamics**: Increasing order book depth can stabilize or shift the expected price
5. **Time Passage**: As the start trading date approaches, the time component in the calculation changes

### How accurate is the displayed APR during the pre-open period?

The accuracy of the pre-open APR:
1. **Estimation**: It's based on the current estimated opening price, which may change
2. **Order Book Depth**: More orders generally lead to more accurate estimates
3. **Market Conditions**: Stable market conditions produce more reliable estimates
4. **Historical Correlation**: Previous pre-open APRs have shown good correlation with actual opening APRs
5. **Indicative Only**: It should be considered indicative rather than guaranteed

## Related Resources

- [APR vs APY](apr-vs-apy.md)
- [Discount Factor](discount-factor.md)
- [Market Dynamics](market-dynamics/README.md)
