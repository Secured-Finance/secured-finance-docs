---
description: Duration-aware minimum collateral requirements
---

# 🪄 Base Price Adjustment

Zero-Coupon bonds start at a deep discount and converge to par (100) at maturity — which means a borrower's obligation _grows_ in present-value terms over time. To keep positions safely collateralized along that path (and to stop attackers from using artificially low prices to compute collateral requirements), the protocol enforces a **minimum collateral base price (BP)**: when an order's price is below the BP, required collateral is computed from the BP instead.

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

## What it means for borrowers

* Your **minimum collateral** is computed from BP when market prices are below it — a spike-proof floor.
* As maturity approaches, BP rises toward 96.00, so **collateral requirements gradually increase**. Plan buffers for long-dated, high-yield (high-category) borrows.
* The formula is deterministic — you can project your future requirements exactly.

## Related

* [Collateral](../core-concepts/collateral.md) · [Liquidation](../core-concepts/liquidation/)
* [Circuit Breaker](circuit-breaker.md) — complementary per-block price protection
