---
description: Deployed contract addresses and the security model
---

# 📔 Contracts and Security

## Contract addresses

| Contract | Network | Address |
| --- | --- | --- |
| **JPYC Vault** | Ethereum Mainnet | `0x7a6E3635694952dC00F6bA4d4AD1a7B892028789` |
| **Secured Finance JPYC Lender** | Ethereum Mainnet | `0x6F6046e59501E484152d46045bA5eECf1Cab8935` |
| **USDFC Vault** | Filecoin | `0x9f59bB0A1dbfad10443Fba08D41c75b0664Bf41B` |
| **Secured Finance USDFC Lender** | Filecoin | `0xE77d238A707762073836351c6E83245C0aE4339d` |

Always verify addresses against this page before interacting with contracts directly.

## Security model

The vaults and strategies run on **Yearn V3** — they are not a fork of it. They follow the **ERC-4626** standard, and share accounting is delegated to Yearn's audited `TokenizedStrategy` implementation, used as-is. Yearn's audits cover those upstream components, not Secured Finance's own strategy logic, deployments, or configuration. The strategies deploy into Secured Finance's [Fixed-Rate Lending protocol](../fixed-rate-lending/contracts-and-security.md), which has its own [audit reports](../fixed-rate-lending/contracts-and-security.md#audit-reports). **The SF Yield Vault strategies have not been separately audited.**

Vaults are **non-custodial**: you interact with the contracts directly from your wallet, and every action you take — deposits, withdrawals, approvals — requires your signature. Automated maintenance calls (`tend` / `report`) are made by the strategy's keeper role and never move funds out of the vault; see [Automated execution and governance](core-mechanics/available-vaults-and-strategies/jpyc-lending-strategy.md#automated-execution-and-governance).

{% hint style="warning" %}
Smart contract risk can never be fully eliminated, and vault positions additionally carry strategy and market risk. Review the [Risk notes](core-mechanics/available-vaults-and-strategies/README.md) before depositing.
{% endhint %}
