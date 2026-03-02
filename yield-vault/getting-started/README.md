---
description: Vault Basic
---

# 🧙 Getting Started

#### What is a Vault?

A Vault is an ERC-4626–compliant smart contract that:

* Accepts deposits of a specific asset
* Issues Vault shares representing proportional ownership
* Allocates deposited assets to one or more yield strategies

Users do not interact with strategies directly. Instead, they hold Vault shares, whose value increases as yield is generated.

***

#### Supported Assets

Each Vault supports a single base asset.

* JPYC Vault: JPYC

Additional Vaults with different base assets may be introduced in the future.

***

#### Depositing into a Vault

When a user deposits assets into a Vault:

1. The Vault receives the asset
2. Vault shares are minted to the user
3. Assets are allocated to one or more strategies according to the Vault configuration

Deposits are permissionless unless explicitly restricted.

***

#### Withdrawing from a Vault

Users can withdraw by redeeming their Vault shares.

* Withdrawals return the underlying asset
* The amount received depends on the current share price
* Withdrawals may be subject to limits or delays, depending on strategy liquidity
