---
description: How strategies plug into vaults, and how capital and liquidity move
---

# 💿 Strategy Framework and Allocation Model

A **strategy** is a contract that generates yield with vault assets. It accepts capital from the vault, deploys it according to its own logic, and reports balances and performance back. Strategies are independent and reusable — one strategy can serve multiple vaults.

From the vault's perspective, every strategy must be able to receive assets, return them on request (subject to liquidity), report its current balance accurately, and reflect gains or losses over time. How it achieves that is deliberately abstract at the vault level.

## Allocation

Vaults allocate capital to strategies based on configuration — allocation limits, strategy capacity, liquidity characteristics, and risk considerations. A vault may run a single strategy or split capital across several, and allocations can change over time without altering the vault interface. The current split is visible in the app's **Strategies** tab, including any unallocated balance awaiting deployment.

Both current vaults run a single lending strategy at 100% target allocation — see [Available Vaults and Strategies](available-vaults-and-strategies/README.md).

## Strategy lifecycle

Strategies move through a managed lifecycle: deployment → registration → activation → ongoing operation and reporting → allocation reduction or pause → removal if necessary. Because the vault interface never changes, none of these steps require you to migrate or exit.

Each strategy periodically **reports** its gains or losses to the vault — the app shows the time of the last report. Reporting is when the [strategy performance fee](vault-system-overview.md#fees) is charged and when the price per share updates to reflect performance.

## Liquidity and withdrawals

A strategy keeps part of its capital deployed in yield-generating positions, so instant liquidity can be lower than total assets. When you withdraw, the vault first uses idle balances, then frees capital from the strategy. Under normal conditions this is seamless. In stressed conditions — when deployed positions cannot be unwound against the live order book — **the withdrawal transaction reverts** rather than executing at a distorted price: no funds move and your position stays in the vault. You can try a smaller amount, or try again once liquidity recovers. Withdrawal availability is therefore not guaranteed at any given moment.

{% hint style="info" %}
The current lending strategies deploy into [Fixed-Rate Lending](../../fixed-rate-lending/overview.md) order books, so their liquidity ultimately depends on those markets — the strategy unwinds positions there to free capital for withdrawals.
{% endhint %}

{% hint style="warning" %}
**Risk is shared, not eliminated.** Vaults guarantee neither principal nor yield — a strategy can gain, earn nothing, or lose, and every outcome flows through to the price per share, borne collectively by the vault's participants.
{% endhint %}

## Related

* [Vault System Overview](vault-system-overview.md) — the accounting model strategies report into
* [Available Vaults and Strategies](available-vaults-and-strategies/README.md) — live strategies and their specifics
