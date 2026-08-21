---
description: Automated, variable-yield vaults built on the Yearn V3 standard
---

# 📢 Overview

The [**SF Yield Vault**](https://vaults.secured.finance/) is Secured Finance's automated yield product. You deposit an asset into a vault, receive **vault shares** that represent your proportional ownership, and earn variable yield as the vault's strategies put the assets to work — no order placement, maturity management, or market timing required.

## How it works in brief

* Each vault accepts a **single base asset** and allocates it to one or more yield strategies.
* Your share count stays constant; the **value per share** rises as yield accrues (and can fall if the strategy takes losses).
* You can redeem shares at any time, but a withdrawal depends on available strategy liquidity — if the underlying order book cannot absorb the unwind, the transaction reverts and no funds move. You can try a smaller amount, or try again once liquidity recovers; withdrawal is not guaranteed at any given moment.

The vaults run on **Yearn V3** and follow the **ERC-4626** vault standard: custody and accounting live in the vault, yield generation lives in the strategies, so strategies can evolve without changing how you interact.

## Available vaults

| Vault | Asset | Network | Strategy |
| --- | --- | --- | --- |
| [**JPYC Vault**](https://vaults.secured.finance/1/0x7a6E3635694952dC00F6bA4d4AD1a7B892028789) | JPYC | Ethereum | [JPYC Lending Strategy](core-mechanics/available-vaults-and-strategies/jpyc-lending-strategy.md) |
| [**USDFC Vault**](https://vaults.secured.finance/314/0x9f59bB0A1dbfad10443Fba08D41c75b0664Bf41B) | USDFC | Filecoin | [USDFC Lending Strategy](core-mechanics/available-vaults-and-strategies/usdfc-lending-strategy.md) |

The current strategies lend into Secured Finance's own [Fixed-Rate Lending](../fixed-rate-lending/overview.md) markets, handling order placement and maturities automatically. More vaults and strategies may be added over time.

## SF Yield Vault or Fixed-Rate Lending?

| | SF Yield Vault | Fixed-Rate Lending |
| --- | --- | --- |
| Yield | Variable | Fixed at trade time |
| Maturity | None — no user-facing fixed maturity; withdrawals depend on strategy liquidity and may revert | Fixed terms up to 2 years |
| Management | Fully automated | You place and manage orders |

Both products coexist: the vault is the hands-off way to access lending yield; Fixed-Rate Lending gives you direct control over rate and term.

{% hint style="warning" %}
**Returns are variable and not guaranteed.** The value of your position can go down as well as up — see [Risks](faqs.md#risks), each strategy's risk notes, and the [Risk Disclaimer](../resources/legal/risk-disclaimer.md) before depositing.
{% endhint %}

## Where next

| You are | Start here |
| --- | --- |
| New to vaults | [Getting Started](getting-started/README.md) |
| Ready to deposit | [Deposit assets](getting-started/deposit-assets.md) |
| Curious how it works inside | [Core Mechanics](core-mechanics/README.md) |
| Looking for addresses | [Contracts and Security](contracts-and-security.md) |
