---
description: Fees, price limits, collateral settings and supported markets
---

# 🔢 Protocol Parameters

Use this page as a reference for trading fees, price limits, collateral requirements and supported markets. To find the check for your intended action, start with [Trading Limits and Collateral Checks](trading-limits-and-collateral-checks.md).

Some settings vary by asset, market or network and may change. The figures below are documented reference settings, not a live market feed. Review the current quote, fees and collateral effect in the app before confirming a transaction.

{% hint style="info" %}
Technical lookup details are grouped under For integrators. Changes to the safeguards are explained in [Contract Upgrade History](contracts-and-security/contract-upgrade-history.md).
{% endhint %}

## Trading fees

| Parameter                                    | Value                                      | Notes                                                                              |
| -------------------------------------------- | ------------------------------------------ | ---------------------------------------------------------------------------------- |
| Taker fee (volume that executes immediately) | 1.00% p.a., prorated by duration           | 0.25% for 3 months, 0.50% for 6 months, …                                          |
| Maker fee (volume that rests on the book)    | 0%                                         | A limit order pays the taker fee on any portion that crosses and fills immediately |
| Itayose (pre-open) fill                      | 0%                                         | Waived for orders matched at market opening                                        |
| Auto-Roll fee                                | Same as taker fee (0.25% per 3-month roll) | Charged in Future Value at each quarterly roll                                     |

## Collateral & liquidation

| Parameter                        | Value                         | Notes                                                                                                                               |
| -------------------------------- | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Liquidation threshold            | Loan-to-value (LTV) above 80% | Position becomes liquidatable                                                                                                       |
| Liquidation amount               | Up to 50% of outstanding debt | While LTV is between the liquidation and full-liquidation thresholds; actual amount depends on the request and available collateral |
| Full liquidation threshold       | Approximately 85% LTV         | Past this point, up to 100% of the outstanding debt can be liquidated.                                                              |
| Liquidation fee (total)          | 7% of liquidated value        | Slashed from borrower's collateral                                                                                                  |
| — Liquidator share               | 5%                            | Paid to the liquidator                                                                                                              |
| — Protocol reserve share         | 2%                            | Sent to the Reserve Fund                                                                                                            |
| ZC bond haircut (same currency)  | 20%                           | ZC bonds count for up to 80% of PV                                                                                                  |
| ZC bond haircut (cross currency) | 100%                          | Cross-currency ZC collateral not accepted                                                                                           |

## Minimum collateral base price (by yield category)

This is a floor used in debt/collateral valuation, not a universal minimum executable order price. It is interpolated linearly by time to maturity; see [Base Price Adjustment](advanced-topics/base-price-adjustment.md). The same configured minimum-debt parameter also supplies the fallback order-price reference when market/opening history is unavailable, evaluated at opening time for that purpose.

The floor changes with the time remaining until maturity. A configured value of zero disables it. Technical lookup details are included below.

| Category | Yield range | BP at maturity | BP at 1y duration |
| :------: | :---------: | :------------: | :---------------: |
|     A    |     0–3%    |      96.00     |       93.00       |
|     B    |     3–5%    |      96.00     |       91.00       |
|     C    |    5–7.5%   |      96.00     |       89.00       |
|     D    |   7.5–10%   |      96.00     |       87.00       |
|     E    |    10–15%   |      96.00     |       84.00       |
|     F    |     15%+    |      96.00     |       81.00       |

Reference category assignment: BTC — A · ETH — B · JPYC — B · USDC — C · USDFC — C · FIL / axlFIL — F.

## Circuit breaker

The thresholds constrain different sides: the LEND side has an upper execution threshold and the BORROW side has a lower execution threshold. See [Circuit Breaker](advanced-topics/circuit-breaker.md) for formulas, examples and limitations.

| Parameter                      | Value or source                                                                                                           |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| Reference for both sides       | Average of up to 3 previous reliable block prices; excludes current-block trading for circuit-breaker checks              |
| Base percentage                | Configurable for each market                                                                                              |
| Percentage allowance           | The base percentage downward for BORROW; twice that percentage upward for LEND. A 5% base gives allowances of 5% and 10%. |
| Minimum downward allowance     | 2.00 displayed price points, with a 0.01 lower floor                                                                      |
| Minimum upward allowance       | 5.00 displayed price points, with a 100.00 upper cap                                                                      |
| Exact thresholds and reference | Calculated for the selected market; see Circuit Breaker for examples and the technical details below for exact values.    |

Execution also requires liquidity and, for a limit order, an accepted placement price.

## Order-price validation

A LEND limit sets the highest bond price you will pay; a BORROW limit sets the lowest bond price you will accept. Each side has its own permitted range. A price outside that range is rejected before any part of the order fills.

An accepted limit price does not guarantee execution. The order may fill immediately, fill partly or remain open. Pre-open markets use a separate shared range for lending and borrowing.

<details>

<summary>For integrators: exact order-price ranges</summary>

Use `LendingMarketController.getOrderUnitPriceRange(currency, maturity)` rather than deriving a common two-sided band in the client. It returns:

1. `minLendUnitPrice`
2. `maxLendUnitPrice`
3. `minBorrowUnitPrice`
4. `maxBorrowUnitPrice`
5. `referenceUnitPrice`
6. `isMinDebtUnitPriceReference`

`isMinDebtUnitPriceReference` is true when the fallback branch was selected, including when minimum debt pricing is disabled and the returned reference is zero.

Prices are integer unit prices: **10,000 = 100.00**, **500 = 5.00** and **1 = 0.01**. Divide an integer price by 100 to obtain the displayed price. A submitted unit price of zero denotes a market order, not a zero-price limit order.

### Continuous trading with a market reference

When the circuit-breaker reference R is nonzero, the accepted maximum LEND price is the lower of the LEND circuit-breaker threshold and R + 10.00, capped at par. The accepted minimum BORROW price is the higher of the BORROW threshold and R − 10.00, floored at 0.01.

The other limits remain 0.01 for minimum LEND and 100.00 for maximum BORROW. A limit order outside its own side's accepted range reverts with `InvalidOrderUnitPrice` before execution. Market orders bypass that placement check but remain subject to execution thresholds and other checks.

### Pre-open orders

Both LEND and BORROW pre-order prices use the same accepted range. Where available, the reference is the immediately preceding order book's finalized Itayose opening price, converted to the new market's opening-to-maturity duration. The range is reference ±10.00, bounded by 0.01 and 100.00.

The contract does not scan older books if that preceding reference is unavailable. It falls back to the currency's minimum debt unit price evaluated at the new market's opening time, through that reference +20.00, capped at 100.00. If minimum debt pricing is disabled, the fallback is the full 0.01–100.00 range.

These pre-open price rules are separate from the minimum pre-order amount, single-side pre-order restriction and freeze period.

### Continuous trading without a circuit-breaker reference

When continuous trading has no nonzero circuit-breaker reference, the fallback reference F is the currency's minimum debt unit price evaluated at the market's opening time. LEND accepts 0.01 through min(100.00, F + 20.00), while BORROW accepts F through 100.00. If F is zero, both sides accept 0.01–100.00. The R ± 10.00 rule is not applied to this fallback.

Refresh the applicable range and simulate the exact transaction before submitting.

</details>

## Market structure

| Parameter                 | Value                                                                                   |
| ------------------------- | --------------------------------------------------------------------------------------- |
| Order books per currency  | 8 active + 1 inactive (pre-open) — standard full set; some markets run fewer maturities |
| Maturity cycle            | Quarterly — last Friday of Mar / Jun / Sep / Dec                                        |
| Longest tenor             | 2 years                                                                                 |
| Itayose pre-open period   | 7 days; order book frozen 1 hour before opening                                         |
| Bond par value            | 100                                                                                     |
| Maximum order price       | 100.00 (no negative yields)                                                             |
| Price precision           | 2 decimal places                                                                        |
| Mark Price minimum volume | 100 USD equivalent per block                                                            |

## Minimum pre-order amount

Minimum pre-order amounts are configurable per currency. The latest configured minimum applies to newly submitted pre-orders across that currency’s maturities. A value of zero disables the restriction.

Check the selected currency’s current minimum when entering a pre-order.

## Supported assets by network

See the canonical [supported-assets table in Collateral](core-concepts/collateral.md#supported-assets-by-network) for trading and collateral eligibility by network. Select the network in the app to check current availability. Dated verification records are in [Contract Upgrade History](contracts-and-security/contract-upgrade-history.md#configuration-observations).

## For integrators

<details>

<summary>Contract lookups and validation</summary>

Use the selected network's addresses and active ABI from [Contracts & Security](contracts-and-security/). Use the lookups below.

* Liquidation configuration: `TokenVault.getLiquidationConfiguration()`
* Order fee rate: `LendingMarket.getOrderFeeRate()`
* Circuit breaker percentage: `LendingMarket.getCircuitBreakerLimitRange()`
* Circuit breaker execution thresholds and reference: `LendingMarket.getCircuitBreakerThresholds(orderBookId)`
* Accepted limit-order price ranges: `LendingMarketController.getOrderUnitPriceRange(currency, maturity)`
* Minimum pre-order amount: `LendingMarket.getMinPreOrderAmount()`
* Configured minimum debt unit price: `LendingMarketController.getMinDebtUnitPrice(currency)`
* Current maturity-adjusted minimum debt unit price: `LendingMarketController.getCurrentMinDebtUnitPrice(currency, maturity)`
* Coverage of any account: `TokenVault.getCoverage(address)`

The asset registry lists configured currencies; market availability and collateral eligibility require the corresponding market and collateral checks.

Implementation changes and their execution references are maintained in [Contract Upgrade History](contracts-and-security/contract-upgrade-history.md).

Contract units: getCoverage() reports debt-to-collateral coverage scaled by 10,000 and rounded down. Liquidation uses a separate, rounded collateral-to-debt ratio and a strict comparison with the configured threshold. With liquidationThresholdRate 12500, exactly 80% LTV is not liquidatable. Do not use a rounded display value as the eligibility check. The reference fullLiquidationThresholdRate of 11765 corresponds to approximately 85% LTV. Divide getCircuitBreakerLimitRange() by 10,000 to obtain the base percentage as a decimal.

</details>
