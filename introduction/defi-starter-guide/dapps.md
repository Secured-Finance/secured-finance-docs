---
description: Guide to using decentralized applications
---

# 🤝 DApps

## Overview

A decentralized application (DApp) lets you use blockchain-based services through a website and your wallet. Follow the steps below to connect, review permissions, submit an action and verify its result.

Before starting, complete [Wallet Setup](wallet-setup.md) and choose your product's network. You can browse many app screens without connecting or sending a transaction.

## How It Works

<details>

<summary>Optional background: what happens on the blockchain</summary>

DApps consist of two main components:

1. **Smart Contracts**: Self-executing code deployed on the blockchain that contains the application's logic
2. **Frontend Interface**: The user interface that allows you to interact with the underlying smart contracts

You can read many DApp screens without making a transaction. When you change an on-chain position, the process typically works as follows:

1. You connect your wallet to the DApp's interface
2. You initiate an action through the interface
3. Your wallet presents a transaction for you to review and sign
4. Once signed, the transaction is broadcast to the blockchain
5. Miners/validators process the transaction and update the blockchain state
6. The DApp interface updates to reflect the new state

</details>

## Step-by-Step Guide to Using DApps

### 1. Connect Your Wallet

Open the app from its official product guide, choose **Connect Wallet**, and select your wallet. Check which account the connection request exposes before accepting. Then confirm that the connected address and selected network match the ones you intend to use.

On mobile, use your wallet's in-app browser or the app's supported wallet connection method. If the wallet is not detected, check that you installed the official app or extension and that it is unlocked.

**Security Note**: When connecting your wallet, verify you're on the correct website to avoid phishing attacks. Always check the URL carefully.

### 2. Review Permissions

Identify what each wallet prompt authorizes:

* **Connection:** Shares the selected public account with the site and lets it request actions. A basic connection alone does not authorize spending.
* **Token approval:** Allows a specified contract to spend a specified token up to an allowance. Check the spender, token and amount.
* **Message signature:** May be a sign-in request, but can also authorize later actions, including token spending. No gas fee does **not** mean no risk. See [MetaMask's signature safety guide](https://support.metamask.io/stay-safe/protect-yourself/wallet-and-hardware/signature-phishing/).
* **Transaction:** Requests an on-chain change, such as a deposit or repayment, and normally requires gas.

Reject any request you cannot match to the action you intended. Never enter a recovery phrase or private key into a DApp.

For Secured Finance apps, compare the token, spender or destination contract with the official address list for the **same product and network**: [Fixed-Rate Lending](../../fixed-rate-lending/contracts-and-security/), [USDFC](../../usdfc-stablecoin/deployed-contracts/), or [SF Yield Vault](../../sf-yield-vault/contracts-and-security.md). Do not use testnet or deprecated-network addresses for mainnet. If you cannot verify a request, stop before signing.

### 3. Navigate the Interface

DApp interfaces typically include:

* Dashboard showing your assets or positions
* Action buttons for key functions (swap, deposit, borrow, etc.)
* Information panels displaying rates, fees, and other important data

Check the selected network, asset and product before entering an amount. A balance shown on another network or account is not automatically available here.

### 4. Initiate Transactions

When you click an action button, you'll typically see a form for the amount and other details. Read the product guide's prerequisites, fees and exit conditions first. For token-based deposits, approval and deposit may be separate steps; completing an approval does not mean a deposit has happened.

### 5. Review and Confirm

Before executing any transaction:

* Double-check the network, account, asset, amount and destination contract.
* Review the estimated gas fee and leave native tokens for later transactions.
* Read the product's resulting balance, debt or position and any limits or warnings.
* Stop if the wallet request differs from the action you selected or contains permissions you did not expect.

### 6. Sign the Transaction

Review the request in the wallet itself, then confirm only if you understand and accept it. Rejecting a prompt before submission does not send the transaction. After submission, record the transaction hash so you can check its status.

### 7. Wait for Confirmation

Submission is not confirmation. Check the wallet's activity view and its link to the network's block explorer:

* **Pending:** Wait or follow the wallet's official pending-transaction guidance. Do not submit the same action again just because the app is slow.
* **Failed or reverted on-chain:** The intended operation did not complete, but gas may have been charged. Read the error and correct the cause before retrying.
* **Successful:** Return to the app, check the same account and network, and verify the expected balance or position. A successful approval is not a completed deposit, and a submitted order is not necessarily a fully filled trade.

If the explorer shows success but the app has not updated, refresh and check the transaction and position before attempting another action.

## Continue to Your Product

Follow the specific transaction and verification steps for [Fixed-Rate Lending](../../fixed-rate-lending/getting-started/), [USDFC](../../usdfc-stablecoin/getting-started/), or [SF Yield Vault](../../sf-yield-vault/getting-started/).

## Common DApp Interactions

### Token Approvals

Many ERC-20 token interactions require a spending approval before the main action. Native-token transfers, such as sending ETH or FIL, do not use the same ERC-20 approval step. Follow the product's instructions rather than expecting every action to require an approval.

{% hint style="warning" %}
**Important**: Approvals let the specified spender move tokens within the allowance, potentially without another approval prompt. Limit the amount where possible. Disconnecting the wallet does not revoke existing token approvals; see [MetaMask's permission guide](https://support.metamask.io/more-web3/dapps/manage-dapp-permissions).
{% endhint %}

### Transaction Batching

<details>

<summary>When an app combines several actions</summary>

Some DApps combine multiple actions into a single transaction. Review every included action and the total gas estimate before signing.

</details>

### Canceling Transactions

Some wallets offer **Speed up** or **Cancel** for a pending transaction. Availability depends on the wallet, network and transaction type. Follow [MetaMask's official pending-transaction guide](https://support.metamask.io/manage-crypto/transactions/how-to-speed-up-or-cancel-a-pending-transaction/) rather than sending a duplicate action.

Cancellation is an attempt to replace a transaction that has not yet confirmed; it is not guaranteed and can cost gas. It cannot reverse a confirmed transaction or cancel an order already recorded by a protocol. Use the product's order-cancellation or exit flow for those cases.

## Security Considerations

* **Verify Smart Contract Addresses**: Check that you're interacting with legitimate contracts
* **Start with Small Amounts**: Test new DApps with minimal funds first
* **Check for Audits**: Check which contracts and versions were reviewed; an audit does not guarantee safety
* **Be Wary of High APYs**: Unusually high returns often indicate higher risk
* **Understand the Risks**: DeFi involves various risks including smart contract vulnerabilities, market volatility, and liquidation

## Common Questions

<details>

<summary>Failed transactions, permissions and finding legitimate apps</summary>

**What if a transaction fails?**\
A transaction rejected in the wallet before submission is different from one that reverts on-chain. A reverted on-chain transaction does not complete its intended state changes, but can still consume gas. Check its status and error before retrying.

**Do I need to connect my wallet every time?**\
Most DApps will remember your connection between sessions, but you may need to reconnect after clearing browser data or using a different device.

**Can DApps access all my funds once connected?**\
A basic connection alone does not grant access to spend your funds. Token approvals, signed permissions and other authorizations can allow later actions without a new prompt for each movement. Review each request, and remember that disconnecting does not revoke token approvals.

**What's the difference between DApps and websites?**\
A DApp's smart contracts may remain on-chain even when its website is unavailable. The website, data services and other dependencies can still fail, so continued access to every feature is not guaranteed.

**How can I tell if a DApp is legitimate?**\
Research the project's team, check for security audits, look for community feedback, and verify smart contract addresses against official sources.

</details>

## Related Resources

* [Wallet Setup & Management](wallet-setup.md)
* [Understanding Gas](gas-fees.md)
* [USDFC Stablecoin Overview](../../usdfc-stablecoin/overview.md)
* [Fixed-Rate Lending Overview](../../fixed-rate-lending/overview.md)
