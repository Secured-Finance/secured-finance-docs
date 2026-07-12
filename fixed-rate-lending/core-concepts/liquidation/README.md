---
description: How under-collateralized positions are handled — the single source of truth
---

# Liquidation

Liquidation keeps the protocol solvent. When a borrower's collateral no longer sufficiently covers their debt, anyone may repay part of that debt in exchange for the borrower's collateral plus a fee. This protects lenders from default risk without credit checks or intermediaries.

{% hint style="info" %}
This page covers the **Fixed-Rate Lending Protocol**. The USDFC Stablecoin Protocol uses a different mechanism (Stability Pool) — see [USDFC Liquidation](../../../usdfc-stablecoin/core-mechanics/liquidation.md).
{% endhint %}

## When does liquidation happen?

A position becomes liquidatable when its **Loan-to-Value (LTV)** ratio reaches the liquidation threshold (current value in [Protocol Parameters](../../protocol-parameters.md) — 80% at time of writing):

$$
LTV = \frac{\text{Value of Debt}}{\text{Value of Collateral}} \times 100\%
$$

Two situations push LTV up:

1. **Collateral value falls** — e.g. you borrowed USDC against ETH and ETH drops.
2. **Debt value rises** — e.g. you borrowed FIL against USDC and FIL rallies.

Positions are valued with [Mark to Market](mark-to-market.md) pricing for ZC bonds and Chainlink oracle feeds for spot prices.

## What happens during liquidation

1. A liquidator repays **up to 50%** of the outstanding debt.
2. Collateral equal to the repaid debt **plus the liquidation fee** is transferred from the borrower. The fee — currently **7% total: 5% to the liquidator, 2% to the protocol's Reserve Fund** ([Protocol Parameters](../../protocol-parameters.md)) — compensates liquidators and builds the protocol's safety buffer.
3. The position returns to a healthier LTV, typically around 70%.

### Worked example

Alice deposits 10 ETH ($20,000) and borrows 12,000 USDC (LTV 60%).

| Event | Collateral value | LTV | Status |
| --- | --- | --- | --- |
| Entry | $20,000 | 60% | Healthy |
| ETH → $1,600 | $16,000 | 75% | At risk |
| ETH → $1,500 | $15,000 | 80% | **Liquidatable** |

A liquidator repays 6,000 USDC (50% of debt). Collateral seized: 6,000 × 1.07 = $6,420 of ETH (4.28 ETH). Alice keeps 5.72 ETH against 6,000 USDC of debt — LTV back to ~70%.

More scenarios, including liquidation caused by the *borrowed* asset rallying: [Liquidation Case Study](liquidation-case-study.md).

## How to avoid liquidation

* Watch the **risk indicator** in [Portfolio](../../getting-started/platform-guide/portfolio.md) — green → yellow → red as LTV climbs.
* **Add collateral** or **partially unwind** debt before the threshold.
* Remember ZC bond prices move with rates — your debt's present value changes even when spot prices don't.
* Leave a buffer around quarterly [Auto-Rolls](../fixed-maturity-and-auto-roll.md), which restate positions at the roll price.
* The [Base Price Adjustment](../../advanced-topics/base-price-adjustment.md) mechanism sets minimum collateral requirements that rise as bonds approach par — factor it into long-dated borrows.

## For liquidators

Liquidation is **permissionless** — any address or contract can liquidate an eligible position and earn the liquidator fee. See the [Liquidator's Guide](liquidators-guide.md) for the contract-level flow and a reference bot implementation.

## In this section

* [Mark to Market](mark-to-market.md) — how positions are valued
* [Liquidation Case Study](liquidation-case-study.md) — full numerical scenarios
* [Liquidator's Guide](liquidators-guide.md) — running liquidations, technically
