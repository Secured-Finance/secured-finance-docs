---
description: Understanding the fee structure that sustains the Fixed-Rate Lending Protocol
icon: 🧀
---

# 🧀 Protocol Fees

## Overview

The Fixed-Rate Lending Protocol implements various fees to sustain operations, incentivize participants, and ensure protocol security. These fees are carefully designed to balance user experience with protocol sustainability.

## What You'll Learn

- How trading fees are structured for market takers vs. limit orders
- How liquidation fees help secure the protocol
- How Auto Roll fees work for reinvestment at maturity
- How fees are reserved and distributed within the ecosystem
- How fee structures vary based on loan duration

## Trading Fees

**Only the price taker** **will pay the transaction fee** of 0.25% (25 basis points) of the loan notional amount for a 3-month duration on our loan platform. **You pay 'No' transaction fee if you place a limit order.** While you place the market order, you pay 0.25 ETH (or equivalent currency) when you borrow or lend 100 ETH for a 3-month duration.

The market taker fee will linearly increase/decrease depending on the duration (1% annum), included in the transaction, and charged by Future Value.

{% hint style="info" %}
No fee will be charged for 'pre-open orders' that are filled during the order book opening process as the trade fee will be waived for the '[Itayose](../../fixed-rate-lending-protocol/broken-reference/)' process!!
{% endhint %}

## Liquidation Fees

As a DeFi project, Collateral Management is critical to secure the protocol. Hence, we ask borrowers to pledge over-collateral before borrowing the fund. And the liquidation mechanism is similarly crucial for our protocol to secure the lenders' money. We charge 7% of the liquidated notional value as a fee slashing from collateral, which will be split between the recovery fund and the liquidators depending on the duration.

## Auto Roll Fees

Our protocol designed the automated rolling feature when the loan matures. This benefits users since you can reinvest without any action at the mid-price with little market impact (see '[Auto Roll](../advanced-topics/market-dynamics/auto-rolling/)'). The roll fee will be the same as the trade fee at 0.25% of the notional amount for a 3-month duration.

## Fee Reserve and Distribution

We reserve part of the fee above to our 'Reserve Fund' to secure the protocol from the incidents, i.e., the black swan event. The rest of the fee will be distributed to the community depending on the contribution.

## Related Resources

- [Liquidation](liquidation/README.md)
- [Order Book System](order-book-system/README.md)
- [Auto-Rolling](../advanced-topics/market-dynamics/auto-rolling/README.md)
- [Safety Measures](../advanced-topics/safety-measures/README.md)
