# 💰 Withdrawing Assets

#### Overview

This page explains how to **withdraw assets from a Vault**.

Withdrawing assets involves redeeming your **Vault Shares** in exchange for the underlying asset. The amount you receive depends on the current **value per share** at the time of withdrawal.

***

### Before You Withdraw

Before withdrawing from a Vault, please note the following:

* You must have an active Vault position
* Your wallet must be connected to the correct network
* The amount you receive may differ from your original deposit
* Vault withdrawals are **not fixed-rate** and **not guaranteed**

Withdrawals are processed on-chain and are subject to network conditions and strategy liquidity.

***

### What Happens When You Withdraw

When you withdraw assets from a Vault:

1. Your Vault Shares are redeemed
2. The Vault retrieves assets from the underlying strategy
3. The corresponding amount of the base asset is transferred to your wallet

If yield has been generated, you may receive **more** than your initial deposit.\
If losses occurred, you may receive **less**.

***

### Step-by-Step: Withdrawing Assets

#### Step 1: Connect Your Wallet

* Open the Secured Finance application
* Click **Connect Wallet**
* Confirm the connection in your wallet

Your active Vault positions will be displayed once connected.

***

#### Step 2: Locate Your Vault Position

* Navigate to **Vaults** or **Portfolio**
* Select the Vault you wish to withdraw from
  * For example: **JPYC Vault**
* Review your current:
  * Vault Share balance
  * Estimated asset value

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.15.34.png" alt=""><figcaption></figcaption></figure>

***

#### Step 3: Choose Withdrawal Amount

* Enter the amount you wish to withdraw
  * Some interfaces allow withdrawing by **asset amount**
  * Others allow withdrawing by **share amount**
* Review the estimated amount you will receive

The estimate is based on the current Vault share price.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.15.54.png" alt=""><figcaption></figcaption></figure>

***

#### Step 4: Confirm Withdrawal

* Click **Withdraw**
* Confirm the transaction in your wallet
* Wait for the transaction to be confirmed on-chain

Once confirmed, the redeemed assets will be sent to your wallet.

***

### Partial vs Full Withdrawals

* **Partial withdrawal**
  * Redeems a portion of your Vault Shares
  * Remaining shares continue to earn yield
* **Full withdrawal**
  * Redeems all Vault Shares
  * Closes your Vault position

Both options follow the same withdrawal process.

***

### Liquidity Considerations

Withdrawals depend on the liquidity available within the strategy.

In certain market conditions:

* Withdrawals may take longer to process
* The amount received may be affected by liquidity constraints

These behaviors are strategy-dependent and are covered in more detail in the **Core Mechanics** section.

***

### After Withdrawing

After a successful withdrawal:

* Your Vault Share balance will be updated
* Your wallet will receive the withdrawn assets
* Any remaining shares will continue to accrue yield

All transactions can be reviewed on-chain using a block explorer.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.21.09.png" alt=""><figcaption></figcaption></figure>

***

### Important Notes

* Withdrawals incur blockchain transaction fees
* Vaults do not enforce fixed lock-up periods by default
* Share value may fluctuate between deposit and withdrawal
* Withdrawing does not retroactively lock in past yields

***

### Next Steps

After withdrawing assets, you may want to:

* Monitor remaining Vault positions
* Re-deposit assets
* Learn how to manage and track your Vault performance

These topics are covered in the following sections.
