---
description: Shares, accounting, capital flow, and fees — the model behind every vault
---

# 🎬 Vault System Overview

Every vault follows the same system model, independent of its strategy. This page is the canonical description of that model.

## The vault as capital container

A vault is an **ERC-4626** smart contract that accepts deposits of a single asset, issues **vault shares** representing ownership, tracks total assets, and delegates capital deployment to strategies. The vault itself does not generate yield — it is a capital coordinator and accounting layer. This separation comes from the **Yearn V3** architecture the vaults run on, and keeps the vault interface stable while strategies evolve.

Responsibilities are deliberately separated:

| Component | Role |
| --- | --- |
| **Vault** | Deposits, withdrawals, share issuance and redemption, asset accounting |
| **Strategy** | Deploys assets to generate yield; interacts with external markets |
| **Periphery modules** | Limits, fees, and configuration, without modifying core contracts |

## Vault shares

When you deposit, the vault mints shares at the current price per share. From then on:

* Your **share count stays constant** unless you deposit or withdraw.
* The **price per share** changes as strategies gain or lose — this is where yield appears.

No rebasing, no separate reward tokens: gains compound in the share price. The share token is visible in your wallet (for example, **yvJPYC** for the JPYC Vault).

## Capital flow

1. You deposit assets; the vault mints shares.
2. The vault allocates assets to one or more strategies.
3. Strategies generate yield over time and report back.
4. Yield increases the vault's total assets, raising the price per share.
5. You redeem shares to withdraw; the vault frees assets from strategies as needed.

The vault makes no assumptions about how a strategy earns — all strategy-specific logic lives outside it, which is what makes the system extensible.

## Fees

| Fee | Rate | Where it applies |
| --- | --- | --- |
| Deposit / withdrawal fee | **None** | — |
| Vault management fee | **0%** | Vault level |
| Vault performance fee | **0%** | Vault level |
| Strategy performance fee | **5%** of realized profits | Strategy level, both current strategies |

The strategy performance fee — **5% of realized profits** — is deducted when the strategy reports its gains, before those gains reach the vault, so the price per share you see is always **net of fees**. You pay no separate deposit or withdrawal fee; you pay blockchain gas for your own transactions, and the strategy's own order fees in the underlying fixed-rate market are reflected in its net returns. Current values are also shown in the app under each vault's **About** and **Strategies** tabs.

## Related

* [Strategy Framework and Allocation Model](strategy-framework-and-allocation-model.md) — how strategies plug into this model
* [Available Vaults and Strategies](available-vaults-and-strategies/README.md) — the strategies live today
* [Contracts and Security](../contracts-and-security.md) — deployed addresses
