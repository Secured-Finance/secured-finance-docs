---
description: Understanding the fee structure that sustains the Fixed-Rate Lending Protocol
icon: 🧀
---

# 🧀 Protocol Fees

## Overview

The Fixed-Rate Lending Protocol implements various fees to sustain operations, incentivize participants, and ensure protocol security. These fees are carefully designed to balance user experience with protocol sustainability. The fee structure is transparent and predictable, allowing users to accurately calculate costs when interacting with the protocol.



## How It Works

### Trading Fees

**Only the price taker** **will pay the transaction fee** of 0.25% (25 basis points) of the loan notional amount for a 3-month duration on our loan platform. **You pay 'No' transaction fee if you place a limit order.** While you place the market order, you pay 0.25 ETH (or equivalent currency) when you borrow or lend 100 ETH for a 3-month duration.

The market taker fee will linearly increase/decrease depending on the duration (1% annum), included in the transaction, and charged by Future Value.

{% hint style="info" %}
No fee will be charged for 'pre-open orders' that are filled during the order book opening process as the trade fee will be waived for the 'Itayose' process!
{% endhint %}

### Liquidation Fees

As a DeFi project, Collateral Management is critical to secure the protocol. Hence, we ask borrowers to pledge over-collateral before borrowing the fund. And the liquidation mechanism is similarly crucial for our protocol to secure the lenders' money. We charge 7% of the liquidated notional value as a fee slashing from collateral, which will be split between the recovery fund and the liquidators depending on the duration.

### Auto Roll Fees

Our protocol designed the automated rolling feature when the loan matures. This benefits users since you can reinvest without any action at the mid-price with little market impact (see '[Auto Roll](../advanced-topics/market-dynamics/auto-rolling/README.md)'). The roll fee will be the same as the trade fee at 0.25% of the notional amount for a 3-month duration.

### Fee Reserve and Distribution

We reserve part of the fee above to our 'Reserve Fund' to secure the protocol from the incidents, i.e., the black swan event. The rest of the fee will be distributed to the community depending on the contribution.

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Market Taker Fee (3-month) | Fee charged to market orders for 3-month duration | 0.25% |
| Annual Fee Rate | Rate used to calculate fees for different durations | 1.00% |
| Limit Order Fee | Fee charged to limit orders | 0% |
| Liquidation Fee | Fee charged on liquidated positions | 7% |
| Auto Roll Fee (3-month) | Fee for automatic position rolling at maturity | 0.25% |
| Itayose Process Fee | Fee for orders filled during market opening | 0% |
| Reserve Fund Allocation | Portion of fees allocated to protocol safety reserve | Variable |

## Examples

### Example 1: Trading Fee Calculation for Different Durations

Let's calculate the trading fees for a market taker borrowing 100 ETH across different durations:

| Duration | Base Fee (3-month) | Annualized Rate | Actual Fee | Fee Amount (ETH) |
|----------|-------------------|-----------------|------------|------------------|
| 3 months | 0.25% | 1.00% | 0.25% | 0.25 ETH |
| 6 months | 0.25% | 1.00% | 0.50% | 0.50 ETH |
| 9 months | 0.25% | 1.00% | 0.75% | 0.75 ETH |
| 12 months | 0.25% | 1.00% | 1.00% | 1.00 ETH |

As shown, the fee scales linearly with the duration, based on an annualized rate of 1.00%.

### Example 2: Limit Order vs. Market Order Fee Comparison

**Scenario A: Limit Order**
- Alice places a limit order to lend 50 ETH for 6 months at a specific rate
- The order is filled when a borrower matches her offer
- Alice pays 0 ETH in trading fees (limit orders are fee-free)
- Total cost to Alice: 0 ETH

**Scenario B: Market Order**
- Bob places a market order to borrow 50 ETH for 6 months
- The order is immediately filled by matching with existing limit orders
- Bob pays 0.50% of 50 ETH = 0.25 ETH in trading fees
- Total cost to Bob: 0.25 ETH

### Example 3: Liquidation Fee Distribution

When a position is liquidated, the 7% liquidation fee is distributed as follows:

**For a 100 ETH liquidation:**
- Total liquidation fee: 7 ETH (7% of 100 ETH)
- Portion to Recovery Fund: 3.5 ETH (50%)
- Portion to Liquidator: 3.5 ETH (50%)

This distribution incentivizes liquidators to maintain the health of the protocol while building a safety reserve.

## Common Questions

### Why are there no fees for limit orders?

Limit orders provide liquidity to the protocol and help establish efficient price discovery. By exempting limit orders from fees, we incentivize users to provide liquidity rather than just consume it. This approach is common in traditional financial markets and helps ensure the orderbook remains deep and liquid.

### How are fees calculated for longer duration loans?

Fees scale linearly with the duration of the loan, based on an annualized rate of 1%. For example, a 3-month loan has a base fee of 0.25%, a 6-month loan has a fee of 0.50%, and a 12-month loan has a fee of 1.00%. This scaling ensures that longer commitments are appropriately priced relative to shorter ones.

### Are there any ways to reduce or avoid fees?

Yes, there are several strategies to minimize fees:
1. Use limit orders instead of market orders to avoid trading fees entirely
2. Participate in the Itayose process when new orderbooks are created, as these orders are exempt from fees
3. For shorter-term needs, consider using shorter duration markets to reduce the duration-based fee component

### What happens to the fees collected by the protocol?

Fees collected by the protocol are allocated to two main purposes:
1. A portion goes to the Reserve Fund, which acts as a safety buffer for the protocol in case of extreme market events or unforeseen circumstances
2. The remaining portion is distributed to the community based on their contributions to the protocol ecosystem, which may include governance participants, liquidity providers, and other stakeholders

### How do Auto Roll fees compare to manually rolling over a position?

Auto Roll fees (0.25% for 3-month duration) are the same as the standard trading fees. However, Auto Roll provides several advantages over manual rollovers:
1. No need to monitor and execute transactions at maturity
2. Execution at mid-price with minimal market impact
3. Reduced gas costs compared to executing multiple transactions
4. Protection against unfavorable price movements during the rollover period

## Key Parameters

| Parameter | Description | Value |
|-----------|-------------|-------|
| Market Taker Fee (3-month) | Fee charged to market orders for 3-month duration | 0.25% |
| Annual Fee Rate | Rate used to calculate fees for different durations | 1.00% |
| Limit Order Fee | Fee charged to limit orders | 0% |
| Liquidation Fee | Fee charged on liquidated positions | 7% |
| Auto Roll Fee (3-month) | Fee for automatic position rolling at maturity | 0.25% |
| Itayose Process Fee | Fee for orders filled during market opening | 0% |
| Reserve Fund Allocation | Portion of fees allocated to protocol safety reserve | Variable |

## Related Resources

- [Liquidation](liquidation/README.md)
- [Order Book System](order-book-system/README.md)
- [Auto-Rolling](../advanced-topics/market-dynamics/auto-rolling/README.md)
- [Safety Measures](../advanced-topics/safety-measures/README.md)
