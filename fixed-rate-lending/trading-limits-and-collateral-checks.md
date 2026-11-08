---
description: Find the price, execution and collateral checks for your next action
---

# Trading Limits and Collateral Checks

Use this page to find the check that applies to your action. Order placement, execution and collateral valuation use different rules.

## Using the app

| Action                             | Check and next step                                                                                                                                                                          |
| ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Place a limit order                | Confirm network, currency, maturity and side. Check the [accepted price range](protocol-parameters.md#order-price-validation), available funds and estimated collateral effect.              |
| Place a market order               | Review liquidity, estimated fill, fees and the side-specific [execution threshold](advanced-topics/circuit-breaker.md).                                                                      |
| Submit a pre-order                 | Check the [Itayose rules](advanced-topics/itayose.md), minimum amount and freeze period.                                                                                                     |
| Check or replace a submitted order | Verify the receipt, fills and current exposure in Portfolio. Follow [Order Life Cycle](core-concepts/order-life-cycle.md#can-i-modify-an-order) before replacing an unfilled remainder.      |
| Borrow or withdraw collateral      | Review [Collateral](core-concepts/collateral.md) coverage and the estimated effect of the transaction. Monitor [Liquidation](core-concepts/liquidation/) risk while a position remains open. |

## Which check applies?

| Check                               | What it controls                                                                          | When it matters                                                                 | Reference                                                                            |
| ----------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Limit-order price range             | Whether a submitted limit price is accepted for its side                                  | Before regular or pre-open order execution                                      | [Order-price validation](protocol-parameters.md#order-price-validation)              |
| Circuit-breaker execution threshold | Highest execution price for LEND; lowest execution price for BORROW                       | Market-order execution and taker matching                                       | [Circuit Breaker](advanced-topics/circuit-breaker.md)                                |
| Minimum collateral base price       | Floor used to value debt in collateral calculations                                       | Where the configured floor exceeds the applicable market price                  | [Base Price Adjustment](advanced-topics/base-price-adjustment.md)                    |
| Reliable-volume threshold           | When traded block prices qualify for price history                                        | Market-price and circuit-breaker reference formation, with initialization rules | [Mark to Market](core-concepts/liquidation/mark-to-market.md)                        |
| Pre-open restrictions               | Limit orders only, single-side participation, configured minimum amount and freeze period | Before continuous trading begins                                                | [Itayose](advanced-topics/itayose.md)                                                |
| Collateral coverage and liquidation | Whether collateral supports the transaction and whether debt is liquidatable              | Borrowing, withdrawals and ongoing position management                          | [Collateral](core-concepts/collateral.md), [Liquidation](core-concepts/liquidation/) |

## Integrating with the contracts

Use [Protocol Parameters](protocol-parameters.md#for-integrators) for getter names, units and exact placement rules. Verify the selected network’s active contracts and ABI, then simulate the intended transaction with the intended account and arguments.

## Scope and verification

Quotes, getter reads and simulations reflect a point in time. State changes, capacity limits or temporary pauses can still stop a transaction. Check app warnings and the confirmed result before retrying. Failed transactions may cost gas.

See [Contract Upgrade History](contracts-and-security/contract-upgrade-history.md) for dated safeguard changes.
