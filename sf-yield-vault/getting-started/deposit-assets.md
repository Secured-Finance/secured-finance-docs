---
description: Make your first vault deposit in five steps
---

# 💴 Deposit assets

Depositing into a vault mints **vault shares** to your wallet — your claim on the vault's assets, whose value changes with strategy performance. How shares work is covered in [Vault System Overview](../core-mechanics/vault-system-overview.md); this page is the hands-on walkthrough.

Before you start, make sure:

* Your wallet is connected to the right network (Ethereum for JPYC, Filecoin for USDFC)
* You hold the vault's base asset, plus a little native token for gas

{% hint style="warning" %}
**A vault is not a savings account.** Returns are variable and not guaranteed — the value of your position can decrease if the strategy takes losses. Review the strategy's risk notes and the [Risk Disclaimer](../../resources/legal/risk-disclaimer.md), and deposit only what fits your risk tolerance.
{% endhint %}

## Step 1 — Connect your wallet

Open the [**SF Yield Vault app**](https://vaults.secured.finance/), click **Connect Wallet**, and approve the connection. Your address and balances appear once connected.

## Step 2 — Select a vault

Pick the vault for your asset — for example, **JPYC Vault**.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.22.17.png" alt="Vault list in the SF Yield Vault app"><figcaption><p>Selecting a vault</p></figcaption></figure>

## Step 3 — Enter the amount

Enter how much you want to deposit and review the estimated vault shares you will receive.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.10.23.png" alt="Deposit amount entry"><figcaption><p>Entering a deposit amount</p></figcaption></figure>

## Step 4 — Approve the asset

Before your first deposit, approve the vault to use your asset: click **Approve**, confirm in your wallet, and wait for confirmation. This is needed only once per asset per vault.

## Step 5 — Confirm the deposit

Click **Deposit** and confirm in your wallet. Once the transaction finalizes, your vault shares are credited.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.12.47.png" alt="Deposit confirmation"><figcaption><p>Confirming the deposit</p></figcaption></figure>

## What happens next

Your position appears in the app and yield starts accruing automatically — no further action needed. Your share count stays the same; it is the **value per share** that grows as the strategy earns.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 23.13.57.png" alt="Position shown after deposit"><figcaption><p>Your position after depositing</p></figcaption></figure>

## Troubleshooting

* **Approve succeeds but Deposit stays disabled** — refresh the page and re-check the amount against your balance and any deposit limit shown.
* **Transaction pending for a long time** — network congestion; wait, or speed the transaction up in your wallet.
* **Asset not showing in the app** — confirm the wallet is on the vault's network (Ethereum for JPYC, Filecoin for USDFC).

## Related

* [Withdraw assets](withdrawing-assets.md) — redeeming shares for the underlying asset
* [Manage your position](managing-position.md) — what to watch after depositing
* [Vault System Overview](../core-mechanics/vault-system-overview.md) — how shares and accounting work
