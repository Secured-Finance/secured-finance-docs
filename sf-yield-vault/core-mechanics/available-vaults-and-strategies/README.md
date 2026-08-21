---
description: The vaults live today and the strategies behind them
---

# 📏 Available Vaults and Strategies

A strategy defines how a vault's deposits are put to work. Two vaults are live today, each running a single lending strategy that deploys into Secured Finance's [Fixed-Rate Lending](../../../fixed-rate-lending/overview.md) markets.

| Vault | Asset | Network | Strategy | Performance fee |
| --- | --- | --- | --- | --- |
| [**JPYC Vault**](https://vaults.secured.finance/1/0x7a6E3635694952dC00F6bA4d4AD1a7B892028789) | JPYC | Ethereum | [JPYC Lending Strategy](jpyc-lending-strategy.md) | 5% performance |
| [**USDFC Vault**](https://vaults.secured.finance/314/0x9f59bB0A1dbfad10443Fba08D41c75b0664Bf41B) | USDFC | Filecoin | [USDFC Lending Strategy](usdfc-lending-strategy.md) | 5% performance |

Each strategy page documents the strategy's **rules as encoded in the deployed contract** — allocation, eligibility, order placement, rebalancing, and capacity — along with fees, liquidity limitations, governance, and risks. The shared mechanics — allocation, reporting, fees, liquidity — are described once in [Vault System Overview](../vault-system-overview.md) and [Strategy Framework and Allocation Model](../strategy-framework-and-allocation-model.md).

Strategies are not static: they can be added, updated, paused, or deprecated over time. Because the vault interface never changes, such changes never require you to alter how you interact with a vault. New strategies will be listed here as they go live.
