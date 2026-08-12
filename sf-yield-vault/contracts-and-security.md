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

The vaults are a fork of **Yearn V3** and follow the **ERC-4626** standard — the vault and tokenized-strategy contracts build on Yearn's extensively audited and battle-tested codebase. The strategies deploy into Secured Finance's [Fixed-Rate Lending protocol](../fixed-rate-lending/contracts-and-security.md), whose own audits and security resources are documented in that section.

Vaults are **non-custodial**: you interact with the contracts directly from your wallet, and every action requires your signature.

{% hint style="warning" %}
Smart contract risk can never be fully eliminated, and vault positions additionally carry strategy and market risk. Review the [Risk notes](core-mechanics/available-vaults-and-strategies/README.md) before depositing.
{% endhint %}
