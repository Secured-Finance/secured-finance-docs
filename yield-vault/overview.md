# 📢 Overview

The [**Yield Vault**](https://vaults.secured.finance/) is an automated yield management module within the **Secured Finance** ecosystem.

Yield Vaults are designed to provide users with a simple way to earn yield by depositing assets into a Vault, without the need to actively manage positions, strategies, or market timing. In return for a deposit, users receive Vault shares that represent their proportional ownership of the Vault. The value of these shares changes over time based on the performance of the underlying strategies.

The Yield Vault architecture is built by forking **Yearn V3** and follows the ERC-4626 standard. This modular design separates asset custody and accounting (Vaults) from yield generation (Strategies), allowing strategies to be updated or expanded while maintaining a consistent user interface.

From a user perspective, interaction with Yield Vaults is intentionally minimal. Users can deposit assets, monitor the value of their position, and withdraw assets at any time by redeeming Vault shares. All strategy selection and allocation decisions are handled at the Vault level.

At launch, Secured Finance introduces the [**JPYC Yield Vault**](https://vaults.secured.finance/1/0x7a6E3635694952dC00F6bA4d4AD1a7B892028789), which accepts JPYC deposits and allocates them to a lending strategy to generate variable yield. Over time, additional Vaults and strategies may be introduced to support different assets and yield sources.

For a practical walkthrough of how to use Yield Vaults, please refer to the **Getting Started** section.
