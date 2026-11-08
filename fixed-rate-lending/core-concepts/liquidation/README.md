---
description: When liquidation can occur, how it works, and how to manage risk
---

# 🚰 Liquidation

When a borrower's collateral no longer sufficiently covers their debt, a liquidator can repay eligible debt and receive collateral plus a fee. The remaining debt stays open unless the liquidation closes it in full.

{% hint style="info" %}
This page covers the **Fixed-Rate Lending Protocol**. The USDFC Stablecoin Protocol uses a different mechanism (Stability Pool) — see [USDFC Liquidation](../../../usdfc-stablecoin/core-mechanics/liquidation.md).
{% endhint %}

## When does liquidation happen?

A position becomes liquidatable when its **Loan-to-Value (LTV)** ratio rises above the liquidation threshold. The documented reference is 80% LTV; check [Protocol Parameters](../../protocol-parameters.md) for the applicable settings. Leave a buffer below the threshold rather than relying on a rounded app value.

$$
LTV = \frac{\text{Value of Debt}}{\text{Value of Collateral}} \times 100\%
$$

Two situations push LTV up:

1. **Collateral value falls** — e.g. you borrowed USDC against ETH and ETH drops.
2. **Debt value rises** — e.g. you borrowed ETH against USDC and ETH rallies.

ZC bonds use [Mark to Market](mark-to-market.md) pricing. Token values come from the feeds configured for your asset and network. See [price sources for Ethereum, Arbitrum and Filecoin](../collateral.md#price-sources-and-verification) for the differences and verification steps.

{% hint style="warning" %}
Protocol valuations may differ from sale prices. For assets with fixed feeds, a market-price drop may not reduce the protocol's valuation. Check [valuation risks for your asset](../collateral.md#price-sources-and-verification) and monitor market liquidity alongside Collateral Utilization and Liquidation Risk.
{% endhint %}

<figure><img src="../../../.gitbook/assets/risk-v2.gif" alt="" width="563"><figcaption><p>LTV and liquidation risk visualization</p></figcaption></figure>

## What happens during liquidation

1. A liquidation can repay up to **50%** of the outstanding debt, or up to **100%** if the position has deteriorated past the **full-liquidation threshold** (≈ LTV 85%; see [Protocol Parameters](../../protocol-parameters.md)).
2. Collateral equal to the repaid debt **plus the liquidation fee** is transferred from the borrower. The fee — currently **7% total: 5% to the liquidator, 2% to the protocol's Reserve Fund** ([Protocol Parameters](../../protocol-parameters.md)) — compensates liquidators and builds the protocol's safety buffer.
3. The amount repaid depends on the liquidation request and available collateral. A partial liquidation reduces debt but leaves the remaining position open; check its updated LTV.

### Worked example

Alice deposits 10 ETH ($20,000) and borrows 12,000 USDC (LTV 60%).

| Event        | Collateral value | LTV    | Status           |
| ------------ | ---------------- | ------ | ---------------- |
| Entry        | $20,000          | 60%    | Healthy          |
| ETH → $1,600 | $16,000          | 75%    | At risk          |
| ETH → $1,480 | $14,800          | 81.08% | **Liquidatable** |

In this example, a liquidator repays 6,000 USDC (50% of debt). Collateral taken: 6,000 × 1.07 = $6,420 of ETH, or about 4.3378 ETH at $1,480. Alice keeps about 5.6622 ETH, worth $8,380, against 6,000 USDC of debt. Her LTV falls to about 71.60%. The example excludes other positions, other fees and price changes.

More scenarios, including liquidation caused by the _borrowed_ asset rallying: [Liquidation Case Study](liquidation-case-study.md).

## How to avoid liquidation

* Watch Collateral Utilization and Liquidation Risk in [Portfolio](../../getting-started/platform-guide/portfolio.md). See [Managing Your Positions](../../getting-started/managing-positions.md) for what each app indicator means; use the liquidation thresholds rather than color alone.
* **Add collateral** or **reduce debt** before the threshold. To reduce debt, unwind the position or execute an opposite trade for part of the amount ([Managing Positions](../../getting-started/managing-positions.md)).
* Remember ZC bond prices move with rates — your debt's present value changes even when spot prices don't.
* Leave a buffer around quarterly [Auto-Rolls](../fixed-maturity-and-auto-roll.md), which restate positions at the roll price.
* The [Base Price Adjustment](../../advanced-topics/base-price-adjustment.md) mechanism sets minimum collateral requirements that rise as bonds approach par — factor it into long-dated borrows.

## For liquidators

Liquidation is **permissionless** — any address or contract can liquidate an eligible position and earn the liquidator fee. See the [Liquidator's Guide](liquidators-guide.md) for the contract-level flow and a reference bot implementation.

## In this section

* [Mark to Market](mark-to-market.md) — how positions are valued
* [Liquidation Case Study](liquidation-case-study.md) — full numerical scenarios
* [Liquidator's Guide](liquidators-guide.md) — running liquidations, technically
