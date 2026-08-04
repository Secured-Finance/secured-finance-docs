---
description: Every fee in the protocol, and how to minimize them
---

# Fees

The protocol charges three fees. Current values are maintained in [Protocol Parameters](../protocol-parameters.md); the structure is explained here.

## 1. Trading fee (takers only)

**The fee depends on how your order executes, not on the order type.** Volume that rests on the order book and waits (**maker**) pays nothing. Volume that takes an existing order and executes immediately (**taker**) pays the fee — this includes the portion of a **limit order** that crosses the book and fills right away.

The fee is **1% per annum of the notional, prorated by time to maturity**, and is charged in Future Value terms:

| Time to maturity | Fee |
| --- | --- |
| 3 months | 0.25% |
| 6 months | 0.50% |
| 9 months | 0.75% |
| 12 months | 1.00% |

*Example:* borrowing 100 ETH for 6 months with a market order costs 0.50 ETH; the same trade as a limit order costs nothing.

{% hint style="info" %}
Orders filled during the [Itayose](../advanced-topics/itayose.md) opening auction are also **fee-free** — an incentive to participate in price discovery for new markets.
{% endhint %}

## 2. Auto-Roll fee

Each quarterly [Auto-Roll](fixed-maturity-and-auto-roll.md) charges the same rate as the taker fee (0.25% per 3-month roll), embedded in the roll price. In exchange, positions are re-invested at a close-to-mid price with no manual action and no counterparty search.

## 3. Liquidation fee

Charged to liquidated borrowers: **7% of the liquidated value**, taken from collateral — **5% to the liquidator, 2% to the protocol Reserve Fund**. Details: [Liquidation](liquidation/README.md).

## Where fees go

Trading fees and Auto-Roll fees accrue to the protocol's **Reserve Fund**, the buffer that protects the protocol in extreme events. Of the liquidation fee, only the **2% protocol share** goes to the Reserve Fund; the 5% goes to the liquidator who executed the call. The Reserve Fund contract address is listed in [Contracts & Security](../contracts-and-security.md).

## Minimizing fees

* Use **limit orders** priced so they rest on the book rather than cross it — resting volume pays no trading fee, and it earns [SFP points](../getting-started/platform-guide/points-and-campaigns.md) for providing liquidity
* Participate in **Itayose** pre-open windows — zero fee fills
* If you don't want quarterly roll fees, **unwind before maturity** rather than letting positions roll
* Avoid liquidation entirely by managing your [collateral](collateral.md) — the 7% fee is by far the most expensive in the protocol
