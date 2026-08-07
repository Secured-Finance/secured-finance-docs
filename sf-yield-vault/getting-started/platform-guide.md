# 🎮 Platform Guide

#### Overview

This page explains the **Vault interface**.

At this stage, the Vault interface allows users to perform **two actions only**:

* Deposit assets into a Vault
* Withdraw assets from a Vault

All information shown on the screen relates directly to these actions or to the current Vault status.

***

### Vault Header

At the top of the Vault page, you will see the Vault header.

This section displays:

* **Vault name**\
  Example: `JPYC`
* **Vault contract address**\
  Example: `0x7a6E3635694952dC00F6bA4d4AD1a7B892028789`
* **Network and asset information**\
  Example: JPYC on Ethereum
* **Summary metrics**
  * **Total deposited**\
    The total amount of assets currently deposited into the Vault
  * **Historical APY**\
    The annualized yield based on past performance
  * **Value in asset**\
    The current estimated value of your position in the base asset

These values update automatically based on on-chain data.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.24.06.png" alt=""><figcaption></figcaption></figure>

***

### Deposit and Withdraw Tabs

Below the header, there are two tabs:

* **Deposit**
* **Withdraw**

These tabs define the actions you can take in the Vault.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.24.43.png" alt=""><figcaption></figcaption></figure>

***

### Deposit Tab

The **Deposit** tab is used to deposit assets from your wallet into the Vault.

#### Fields Explained

* **From wallet**\
  The asset that will be sent from your wallet\
  Example: `JPYC`
* **Amount**\
  The amount of the asset you want to deposit\
  You can click **Max** to use your full wallet balance
* **To vault**\
  The Vault share token you will receive\
  Example: `yvJPYC`
* **You will receive**\
  An estimate of how many Vault Shares you will receive\
  This value depends on the current share price

#### How Deposits Work

1. Enter the deposit amount
2. Approve the asset (if required)
3. Confirm the deposit transaction

Once completed, Vault Shares are credited to your wallet.

***

### Withdraw Tab

The **Withdraw** tab is used to redeem Vault Shares and receive assets back to your wallet.

#### Fields Explained

* **From vault**\
  The Vault share token you are redeeming\
  Example: `yvJPYC`
* **Amount**\
  The number of Vault Shares you want to redeem\
  You can click **Max** to withdraw all shares
* **To wallet**\
  The asset that will be returned to your wallet\
  Example: `JPYC`
* **You will receive**\
  An estimate of the asset amount you will receive\
  This value depends on the current share price

#### How Withdrawals Work

1. Enter the withdrawal amount
2. Confirm the transaction in your wallet

After confirmation, the asset is sent to your wallet.

***

### About Tab

The **About** tab provides general information about the Vault.

This section includes:

* A short Vault description
* Historical APY data
* Fee information, such as:
  * Management fee
  * Performance fee

All values shown reflect the current configuration of the Vault.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.25.58.png" alt=""><figcaption></figcaption></figure>

***

### Strategies Tab

The **Strategies** tab shows how assets deposited in the Vault are allocated.

In this section, you may see:

* The name of the strategy currently used by the Vault\
  Example: `Secured Finance JPYC Lender`
* **Allocation percentage**\
  The portion of Vault assets allocated to each strategy
* **Unallocated balance**\
  Assets that are not currently allocated to a strategy

This tab is **informational only**.\
Users cannot change strategy allocation.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.26.10.png" alt=""><figcaption></figcaption></figure>

***

### Info Tab

The **Info** tab displays additional Vault-related information, such as:

* Vault metadata
* On-chain references
* Supporting technical details

This tab is intended for users who want more context about the Vault.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.26.22.png" alt=""><figcaption></figcaption></figure>

***

### Risk Tab

The **Risk** tab outlines risks associated with depositing into the Vault.

This section typically includes:

* Smart contract risk
* Strategy-related risk
* Liquidity risk

Users are encouraged to review this information before depositing assets.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.26.31.png" alt=""><figcaption></figcaption></figure>

***

### Transaction Confirmation

All actions in the Vault require confirmation through your wallet.

* Deposits
* Withdrawals
* Approvals

Transactions are completed once confirmed on-chain.

***

### Summary

Using the current Vault interface, users can:

* Deposit assets from their wallet into a Vault
* Withdraw assets by redeeming Vault Shares
* View Vault status, allocation, and basic performance metrics

For details on how Vaults and strategies work internally, refer to the **Core Mechanics** section.
