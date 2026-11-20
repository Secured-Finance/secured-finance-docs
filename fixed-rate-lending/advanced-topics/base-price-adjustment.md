---
description: Duration-aware minimum collateral requirements
---

# 🪄 Base Price Adjustment

Zero-Coupon bonds converge to par (100) at maturity, so a borrower's obligation can grow in present-value terms over time. The protocol enforces a minimum collateral base price (BP): when a market's price is below the BP, debt in that market is valued at the BP instead.

## The formula

BP is linearly interpolated by time to maturity _t_ between two reference points — the BP at maturity and the BP at 1-year duration:

$$
BP(t) = P_{M} - \frac{t}{\text{secondsPerYear}} \times (P_{M} - P_{1Y})
$$

Reference points depend on the asset's **yield category**:

| Category | Yield range | BP at maturity | BP at 1y duration |
| :------: | :---------: | :------------: | :---------------: |
|     A    |     0–3%    |      96.00     |       93.00       |
|     B    |     3–5%    |      96.00     |       91.00       |
|     C    |    5–7.5%   |      96.00     |       89.00       |
|     D    |   7.5–10%   |      96.00     |       87.00       |
|     E    |    10–15%   |      96.00     |       84.00       |
|     F    |     15%+    |      96.00     |       81.00       |

Current category assignments (BTC — A, ETH/JPYC — B, USDC/USDFC — C, FIL/axlFIL — F) are reviewed **quarterly** and revised with community input based on observed APRs. Live values: [Protocol Parameters](../protocol-parameters.md).

## Examples

* **Category A, 3 months to maturity:** BP = 96.00 − 0.25 × (96.00 − 93.00) = **95.25**
* **Category C, 1 year:** BP = 96.00 − 1.0 × (96.00 − 89.00) = **89.00**
* **Category F, 18 months:** BP = 96.00 − 1.5 × (96.00 − 81.00) = **73.50**

(Illustrative annualized math; contracts compute in seconds.)

## Where the floor applies

* **Debt only.** BP is a floor for borrowing positions; it does not raise the value of lending positions.
* **Per maturity.** Before a position rolls, its source maturity's floor applies. After conversion, the destination maturity's floor applies.
* **Net positions.** A vault balance and filled orders in the same maturity are netted before valuation, keeping valuation consistent before and after cleanup.
* **Unpriced markets.** Where no market price has been established, positions are valued at par (100.00), not at BP.

## What it means for borrowers

* Debt valuation uses BP when the relevant maturity's market price is below it.
* As maturity approaches, BP rises toward 96.00, so **collateral requirements gradually increase**. Plan buffers for long-dated, high-yield (high-category) borrows.
* The formula lets you project BP over time. Actual collateral requirements also depend on your positions, market prices and protocol parameters.

## Related

* [Collateral](../core-concepts/collateral.md) · [Liquidation](../core-concepts/liquidation/)
* [Circuit Breaker](circuit-breaker.md) — complementary per-block price protection
