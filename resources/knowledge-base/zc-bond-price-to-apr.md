---
description: APR calculation
---

# ZC Bond Price to APR

On our platform, the execution of bond transactions is determined by the bond price. However, we recognize that users may find it more convenient to reference the Annual Percentage Rate (APR) when assessing yields. To accommodate this, we provide the APR as a reference rate, which is based on a linear calculation up to a 1-year tenor using an Act/365 basis. For tenors exceeding 1 year, we utilize annual compounding to determine the yield.

{% hint style="info" %}
**What is Act/365?**

Act/365 is a day count convention used in bond math to calculate the accrued interest on a bond. It stands for Actual/365 and is also known as the Actual/365 Fixed convention.

Note that the Act/365 convention assumes a fixed year of 365 (or 366) days, regardless of the actual number of days in the year. This is different from other day count conventions, such as the 30/360 convention, which assumes a fixed 30-day month and a 360-day year.
{% endhint %}

## Maturity < 1y

$$
FV = PV * (1 + r*Act/365)
$$

* PV: Present Value
* FV: Future Value
* r: APR (Annuale Percentage Rate)
* Act: Actual duration to Maturity &#x20;

As an inherent characteristic of the ZC bond market, the present value (PV) of a bond is equivalent to its bond price, while the future value (FV) is fixed at 100, as per the design of our protocol. Duration is calculated using the seconds to maturity compared to seconds per year, enabled by our smart contract technology.

$$
APR = (100/BondPrice - 1)*secondsPerYear/secondsToMaturity
$$

* secondsPerYear: 365 \* 24 \* 60 \* 60 = 31,536,000

## Maturity >1y

$$
FV = PV *(1 + r)^n
$$

* PV: Present Value
* FV: Future Value
* r: APR (Annuale Percentage Rate)
* n: Years to Maturity

Similar to the formulaic approach for tenors less than 1 year, the present value (PV) of a bond equals its bond price, while the future value (FV) remains fixed at 100, in accordance with our protocol design.

$$
APR =(100/BondPrice)^{(1/YearsToMaturity)}-1
$$

* Years to Maturity: Seconds to Maturity/Seconds Per Year



## **During Pre-Open Period**

**What is the Pre-Open Period?**

The pre-open period is a specific time frame before the official opening of a new bond market. During this period, we invite users to place their orders in the pre-open order book. This allows market participants to gauge interest and liquidity before the market officially starts. For more detailed explanation, please visit to [Fair Price Discovery.](../../fixed-rate-lending-protocol/protocol-features/new-market-listing-and-delisting/itayose-fair-price-discovery.md)

**How is APR Displayed During the Pre-Open Period?**

During the pre-open period, the APR displayed is based on the estimated 'opening price' at the time the market starts. It's important to note that the APR is not calculated from the spot date to the end of maturity. Instead, it is calculated from the start trading date to the end of maturity.

{% hint style="info" %}
The formula for APR during the pre-open period would be similar to the existing APR calculation, but the 'Actual duration to Maturity' (Act) and 'Years to Maturity' would be replaced by the 'Actual Bond Duration from Start Trading Date to End of Maturity' and 'PV' will be 'estimated opening price'.&#x20;
{% endhint %}
