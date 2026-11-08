---
description: Side-specific execution limits and accepted limit-order prices
---

# 🚦 Circuit Breaker

The circuit breaker limits execution prices for each side of an order book. A **LEND** order buys ZC bonds and has an upper execution-price limit. A **BORROW** order sells ZC bonds and has a lower execution-price limit.

Market orders may fill partly before reaching the applicable limit. A new limit order whose price is outside its accepted **side-specific order-price range** is rejected before execution. These are different outcomes: see [Order Life Cycle](../core-concepts/order-life-cycle.md).

## One reference for both sides

Both thresholds use the same reference price: the arithmetic average of up to the **three most recent previous reliable block prices**: block-level trade prices that qualify for the protocol’s stored price history. Trading in the current block does not update this reference for circuit-breaker checks within that block.

Each block price is calculated as total Present Value divided by total Future Value, scaled to the bond-price units. A traded block normally qualifies once its accumulated amount meets the configured reliable-volume threshold. An initialized opening or roll price can seed the history; with no stored price history, a positive traded amount can qualify the first block even below the reliable-volume threshold. This does not make current-block trades part of that block’s circuit-breaker reference. See [Mark to Market](../core-concepts/liquidation/mark-to-market.md) for valuation context.

The reference uses available history, which may contain fewer than three prices. It does not necessarily represent the previous three consecutive blockchain blocks.

## Execution thresholds

The lending ceiling and borrowing floor are calculated from the shared reference price. They combine a percentage allowance with a minimum price-point allowance; bond prices remain between 0.01 and 100.00.

For example, with a reference price of 80.00 and a base percentage of 5%, the lending ceiling is 88.00 and the borrowing floor is 76.00. A LEND order cannot execute above 88.00, and a BORROW order cannot execute below 76.00. Each threshold applies only to its order side.

With a reference price of 16.00 and a base percentage of 5%, the minimum allowances set the lending ceiling at 21.00 and the borrowing floor at 14.00. The ceiling is always capped at 100.00. If no reference exists, the execution limits fall back to 100.00 for LEND and 0.01 for BORROW; separate order-price validation still applies.

## Accepted limit-order prices

During continuous trading, when the circuit-breaker reference is nonzero:

| Order side | Accepted minimum                                                         | Accepted maximum                                                         |
| ---------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| LEND       | 0.01                                                                     | The lower of the lending ceiling and reference + 10.00, capped at 100.00 |
| BORROW     | The higher of the borrowing floor and reference − 10.00, floored at 0.01 | 100.00                                                                   |

A LEND limit below the borrowing floor or a BORROW limit above the lending ceiling can therefore be valid. Check the order against its own side's range, not both circuit-breaker thresholds.

A limit price outside the permitted range is rejected before any part fills or a resting order is created. A failed transaction may still cost gas.

Pre-open markets and markets without recent price history use separate rules. See [Protocol Parameters](../protocol-parameters.md#order-price-validation) for the accepted ranges.

## Market orders and unfilled amounts

A market order matches available liquidity within its side’s execution threshold. For Filled, Blocked, Killed and rejected outcomes, and how to replace an order safely, see [Order Life Cycle](../core-concepts/order-life-cycle.md).

Refresh the quote and accepted range before retrying; conditions can change between blocks.

## Protection and limitations

Using a previous-block reference prevents current-block trades from moving their own circuit-breaker reference. Price moves across multiple blocks, limited liquidity and collateral valuation can still expose users to losses or liquidation.

<details>

<summary>For integrators: formulas and exact limits</summary>

Let **R** be the shared reference and **r** be the configured base circuit-breaker percentage. On the displayed 0.01–100.00 price scale, the thresholds are approximately:

{% code collapsedlinecount="10" %}
```
LEND upper threshold U = min(100.00, max(R × (1 + 2r), R + 5.00))
BORROW lower threshold D = max(0.01, min(R × (1 − r), R − 2.00))
```
{% endcode %}

The contracts perform integer arithmetic and rounding. Read the exact thresholds from `LendingMarket.getCircuitBreakerThresholds(orderBookId)` rather than recomputing them from rounded display values. It returns `maxLendUnitPrice`, `minBorrowUnitPrice` and `referenceUnitPrice`.

Read LendingMarketController.getOrderUnitPriceRange(currency, maturity) for accepted placement prices. Market orders use an input unit price of zero and bypass this placement check, while remaining subject to execution and other transaction checks.

</details>

## Related

* [Trading Limits and Collateral Checks](../trading-limits-and-collateral-checks.md): start with the operation you want to perform
* [Order Life Cycle](../core-concepts/order-life-cycle.md): accepted orders, rejections and partial fills
* [Protocol Parameters](../protocol-parameters.md): configuration and integration getters
* [Base Price Adjustment](base-price-adjustment.md): the separate floor used in collateral calculations

For changes to these safeguards and their deployment history, see [Contract Upgrade History](../contracts-and-security/contract-upgrade-history.md).
