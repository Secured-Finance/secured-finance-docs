---
description: How assets join and leave the platform in an orderly way
---

# 🗓️ Market Listing & Delisting

## Listing a new asset

1. **Pre-open orders** — 7 days before the new asset's markets launch, users can place one-sided limit orders. The book freezes 1 hour before opening.
2. **Itayose** — the opening auction sets a fair initial price. See [Itayose](itayose.md).
3. **Order book expansion** — a newly listed asset typically starts with **four order books** (\~1 year of maturities). One additional 3-month book is added **each week** until the full set of eight books (2 years) is reached, matching other assets. The starting count is decided per market: depending on liquidity, a market may open with fewer books (for example two, covering six months).

## Delisting an asset

Delisting is gradual — no forced closures:

1. **Auto-Roll stops** for the asset: matured positions no longer roll into the next market.
2. **Loans expire naturally** at their maturity dates.
3. **Repayment window** — after maturity, borrowers have **1 week** to repay. Unrepaid debt is then covered by liquidating the borrower's collateral, protecting lenders.
4. **Redemption** — after the repayment window, lenders redeem their principal plus interest in full.

{% hint style="info" %}
Trading remains available throughout the delisting process so users can unwind or clean up positions at any point.
{% endhint %}

## Related

* [Itayose](itayose.md) — opening price discovery
* [Fixed Maturity & Auto-Roll](../core-concepts/fixed-maturity-and-auto-roll.md) — normal maturity behavior
* [Protocol Parameters](../protocol-parameters.md) — currently supported assets
