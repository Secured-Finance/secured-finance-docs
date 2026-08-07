---
description: Why the protocol quotes APR, and how to compare rates across venues
---

# 📈 APR vs APY

**APR** (Annual Percentage Rate) is simple interest — the periodic rate scaled to a year, ignoring compounding. **APY** (Annual Percentage Yield) is the effective annual return _including_ compounding:

$$
APY = \left(1 + \frac{APR}{n}\right)^{n} - 1 \qquad (n = \text{compounding periods per year})
$$

## Why Secured Finance quotes APR

* **Fixed-income convention** — bond markets quote simple rates; participants from traditional finance expect APR.
* **Nothing to compound** — a Zero-Coupon bond has exactly two cash flows. There are no interim payments to reinvest, so a compounding assumption would be fiction.
* **Exact by construction** — buy at 98.04, redeem at 100: your return _is_ the discount. The APR label just annualizes it (see [Zero-Coupon Bonds](../core-concepts/zero-coupon-bonds.md) for the formulas).

Most variable-rate DeFi protocols quote APY because their rates float and compound continuously — the APY figure assumes today's rate holds for 365 days, which it never does. When comparing rates across venues, convert to a common basis first.

## The difference in numbers

Bob invests 100 USD at "10%" for 6 months:

* **10% APR** → 100 × (1 + 0.10 × 0.5) = **105.00**
* **10% APY** (compounded semi-annually) → equivalent APR is lower: 100 × (1.10)^0.5 ≈ **104.88**

The same nominal "10%" differs by how compounding is counted. At 12% nominal for one year:

| Compounding | Effective APY |
| ----------- | ------------- |
| Annual      | 12.00%        |
| Quarterly   | 12.55%        |
| Monthly     | 12.68%        |
| Daily       | 12.75%        |

## Converting for comparison

* APR → APY: `APY = (1 + APR/n)^n − 1`
* APY → APR: `APR = n × ((1 + APY)^(1/n) − 1)`

When comparing a Secured Finance fixed APR with a variable APY elsewhere, remember the fixed rate is **guaranteed to maturity**, while the APY is an extrapolation of a moment's rate.

## Related

* [Zero-Coupon Bonds](../core-concepts/zero-coupon-bonds.md) — price → APR math used by the app
* [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md) — quarterly reinvestment via Auto-Roll
