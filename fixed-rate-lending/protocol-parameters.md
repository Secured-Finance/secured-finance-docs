---
description: The single source of truth for every protocol number
---

# Protocol Parameters

This page is the authoritative reference for all Fixed-Rate Lending Protocol parameters. Other pages link here instead of restating values. **Last verified: 2026-07-16** (liquidation configuration, Base Price values, Mark Price minimum volume, and the supported asset list confirmed with the engineering team against production; remaining values match the contracts repository).

{% hint style="info" %}
Parameters may change through protocol governance. For integrations, always confirm critical values on-chain — addresses in [Contracts & Security](contracts-and-security.md).
{% endhint %}

## Trading fees

| Parameter | Value | Notes |
| --- | --- | --- |
| Taker fee (volume that executes immediately) | 1.00% p.a., prorated by duration | 0.25% for 3 months, 0.50% for 6 months, … |
| Maker fee (volume that rests on the book) | 0% | A limit order pays the taker fee on any portion that crosses and fills immediately |
| Itayose (pre-open) fill | 0% | Waived for orders matched at market opening |
| Auto-Roll fee | Same as taker fee (0.25% per 3-month roll) | Charged in Future Value at each quarterly roll |

## Collateral & liquidation

| Parameter | Value | Notes |
| --- | --- | --- |
| Liquidation threshold | LTV above 80% (`getCoverage()` > 8000) | Position becomes liquidatable |
| Liquidation amount | 50% of outstanding debt | While LTV is between the liquidation and full-liquidation thresholds; targets ~70% post-liquidation LTV |
| Full liquidation threshold | ≈ LTV 85% (`fullLiquidationThresholdRate` = 11765) | Past this point, **100% of the outstanding debt** is liquidated in a single call. Protocol-wide setting — identical across networks and currencies (production value confirmed 2026-07-16; on-chain getter: `TokenVault.getLiquidationConfiguration()`) |
| Liquidation fee (total) | 7% of liquidated value | Slashed from borrower's collateral |
| — Liquidator share | 5% | Paid to the liquidator |
| — Protocol reserve share | 2% | Sent to the Reserve Fund |
| ZC bond haircut (same currency) | 20% | ZC bonds count for up to 80% of PV |
| ZC bond haircut (cross currency) | 100% | Cross-currency ZC collateral not accepted |

## Circuit breaker (per block)

| Parameter | Value |
| --- | --- |
| Max downward move | 5% below MA of last 5 reliable block prices |
| Max upward move | 10% above MA of last 3 reliable block prices |
| Minimum downward allowance | 2.00 (absolute price) |
| Minimum upward allowance | 7.00 (absolute price) |

## Market structure

| Parameter | Value |
| --- | --- |
| Order books per currency | 8 active + 1 inactive (pre-open) — standard full set; some markets run fewer maturities |
| Maturity cycle | Quarterly — last Friday of Mar / Jun / Sep / Dec |
| Longest tenor | 2 years |
| Itayose pre-open period | 7 days; order book frozen 1 hour before opening |
| Bond par value | 100 |
| Maximum order price | 100.00 (no negative yields) |
| Price precision | 2 decimal places |
| Mark Price minimum volume | 100 USD equivalent per block |

## Minimum collateral base price (by yield category)

Interpolated linearly by time to maturity — see [Base Price Adjustment](advanced-topics/base-price-adjustment.md).

| Category | Yield range | BP at maturity | BP at 1y duration |
| :-: | :-: | :-: | :-: |
| A | 0–3% | 96.00 | 93.00 |
| B | 3–5% | 96.00 | 91.00 |
| C | 5–7.5% | 96.00 | 89.00 |
| D | 7.5–10% | 96.00 | 87.00 |
| E | 10–15% | 96.00 | 84.00 |
| F | 15%+ | 96.00 | 81.00 |

**Current category assignment** (reviewed quarterly; production values confirmed 2026-07-16): BTC — A · ETH — B · JPYC — B · USDC — C · USDFC — C · FIL / axlFIL — F

## Supported assets by network

| Network | Lend / Borrow | Accepted as collateral |
| --- | --- | --- |
| Ethereum | WBTC, ETH, USDC, axlFIL, JPYC | WBTC, ETH, USDC, JPYC, uMINT |
| Arbitrum | WBTC, ETH, USDC | WBTC, ETH, USDC |
| Filecoin (FVM) | FIL, USDFC | FIL, iFIL, wpFIL, USDFC |

{% hint style="info" %}
Asset availability last confirmed with the team on 2026-07-16 (JPYC lending markets: Ethereum only; wpFIL collateral: Filecoin only; uMINT/RWA collateral: Ethereum only). The live list can be read per network from `CurrencyController.getCurrencies()`.
{% endhint %}

{% hint style="warning" %}
Avalanche support is **deprecated**. Polygon zkEVM has been **sunset and is no longer operational**. Legacy deployment addresses are retained for historical reference only: [Contracts & Security](contracts-and-security.md).
{% endhint %}

## Verifying on-chain

* Liquidation configuration: `TokenVault.getLiquidationConfiguration()`
* Order fee rate: `LendingMarket.getOrderFeeRate()`
* Circuit breaker range: `LendingMarket.getCircuitBreakerLimitRange()`
* Coverage of any account: `TokenVault.getCoverage(address)`
