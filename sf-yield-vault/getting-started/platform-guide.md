---
description: Every tab and field of the SF Yield Vault interface
---

# 🎮 Platform guide

This page tours the vault view in the [**SF Yield Vault app**](https://vaults.secured.finance/) — what each tab shows and what the fields mean. For step-by-step walkthroughs, see [Deposit assets](deposit-assets.md) and [Withdraw assets](withdrawing-assets.md).

## Vault header

The top of the vault page shows the vault's identity and headline numbers: the vault name and contract address, the network and asset (for example, JPYC on Ethereum), **TVL**, **Estimated APY** (with the historical APY shown beneath it), and — once connected — **Your Holdings**, your position in asset terms. All values update from on-chain data.

<figure><img src="../../.gitbook/assets/yv-vault-header.png" alt="Vault header with summary metrics"><figcaption><p>Vault header</p></figcaption></figure>

## Deposit and Withdraw

Two tabs below the header handle the actions you can take.

<figure><img src="../../.gitbook/assets/yv-action-tabs.png" alt="Deposit and Withdraw tabs"><figcaption><p>The action tabs</p></figcaption></figure>

**Deposit** moves assets from your wallet into the vault:

| Field | Meaning |
| --- | --- |
| **From wallet** | The asset you send (e.g. JPYC). **Max** uses your full balance |
| **To vault** | The vault share token you receive (e.g. yvJPYC) |
| **You will receive** | Estimated shares at the current value per share |

**Withdraw** redeems shares back to your wallet:

| Field | Meaning |
| --- | --- |
| **From vault** | The share token you redeem (e.g. yvJPYC). **Max** redeems everything |
| **To wallet** | The asset returned (e.g. JPYC) |
| **You will receive** | Estimated assets at the current value per share |

Every action — approvals, deposits, withdrawals — is confirmed through your wallet and completes on-chain.

## About

A short description of the vault, its APY over **Last 7 days / Last 30 days / Inception**, and its **Fees** (management and performance). Current fee values for both vaults are listed in [Fees](../core-mechanics/vault-system-overview.md#fees).

<figure><img src="../../.gitbook/assets/yv-about-tab.png" alt="About tab with APY and fees"><figcaption><p>The About tab</p></figcaption></figure>

## Strategies

How the vault's assets are allocated: each strategy's name (for example, **Secured Finance JPYC Lender**), its **Allocation %**, allocation in dollar terms, and **Est. APY**. Expanding a strategy row reveals its contract address, per-strategy fees, and the time of the last report. Assets not yet deployed appear as an **Unallocated** balance. This tab is informational — allocation cannot be changed by users.

<figure><img src="../../.gitbook/assets/yv-strategies-tab.png" alt="Strategies tab with an expanded strategy and unallocated balance"><figcaption><p>The Strategies tab</p></figcaption></figure>

## Info

Vault metadata and on-chain references for those who want the technical context, including the current **Price Per Share**.

<figure><img src="../../.gitbook/assets/yv-info-tab.png" alt="Info tab"><figcaption><p>The Info tab</p></figcaption></figure>

## Risk

The risks of depositing — smart contract, strategy, and liquidity risk. Review this tab before depositing; it complements the strategy pages' [risk notes](../core-mechanics/available-vaults-and-strategies/README.md).

<figure><img src="../../.gitbook/assets/yv-risk-tab.png" alt="Risk tab"><figcaption><p>The Risk tab</p></figcaption></figure>

## Related

* [Deposit assets](deposit-assets.md) — first deposit, step by step
* [Withdraw assets](withdrawing-assets.md) — redeeming shares
* [Vault System Overview](../core-mechanics/vault-system-overview.md) — the mechanics behind the numbers
