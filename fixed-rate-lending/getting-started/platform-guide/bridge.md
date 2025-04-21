---
description: A step-by-step guide to transferring assets between blockchain networks
icon: 🌉
---

# 🌉 Bridge

## Prerequisites

- A connected wallet with assets to transfer
- Basic understanding of blockchain networks
- Access to the Secured Finance platform

## Overview

The [**Bridge tab**](https://app.secured.finance/bridge/) lets you easily transfer assets between different blockchain networks directly within the Secured Finance platform. Powered by **Axelar**, it provides a simple and secure way to perform cross-chain swaps without the need for external exchanges.

## What You Can Do with the Bridge

* **Cross-Chain Swaps**: Exchange tokens from one blockchain network to another (e.g., swap USDC on Ethereum for FIL on the Filecoin network)
* **Obtain Native Tokens**: Acquire native tokens required for transaction fees on other networks, such as FIL for the Filecoin network or ETH for Ethereum
* **Expand Your Portfolio**: Access assets and opportunities available on multiple blockchain networks

## Step 1: Connect Your Wallet

1. Navigate to the [Bridge tab](https://app.secured.finance/bridge/)
2. Click **Connect Wallet** at the top right corner
3. Select your wallet provider (MetaMask, WalletConnect, etc.)
4. Approve the connection request in your wallet

## Step 2: Select Networks and Tokens

1. In the **From Network** dropdown, choose the blockchain and token you are swapping from (e.g., Ethereum and USDC)
2. In the **To Network** dropdown, select the destination blockchain and token you want to receive (e.g., Filecoin and FIL)
3. Ensure both networks are supported by your wallet

![Bridge Interface](../../../.gitbook/assets/bridge-interface.png)

## Step 3: Enter the Amount

1. Specify the amount of the token you wish to swap in the input field
2. Review the estimated amount you will receive after fees
3. Ensure you have sufficient balance in your wallet

## Step 4: Approve Token Use

1. If this is your first time using this token with the bridge, click **Give Permission to Use Token**
2. Confirm the approval transaction in your wallet
3. Wait for the approval transaction to be confirmed on the blockchain

## Step 5: Review and Confirm

1. Check the transaction details, including:
   - Estimated time for completion
   - Network fees
   - Exchange rate
2. Click **Swap** to initiate the transfer
3. Confirm the transaction in your wallet
4. Wait for the transaction to be processed

## Step 6: Verify Receipt

1. Once completed, check your wallet on the destination network
2. Confirm the arrival of your tokens
3. The transaction history will be available in the Bridge tab

{% hint style="info" %}
Need more detailed guidance? Here is the step-by-step Medium article: [**How to Obtain Filecoin Using Cross-Chain Swap**](https://medium.com/secured-finance/how-to-obtain-filecoin-using-cross-chain-swap-4364eeeacbbe).
{% endhint %}

## Next Steps

After successfully bridging assets, you might want to:

- [Deposit your assets as collateral](../../borrowing-assets.md)
- [Start lending your assets](../../lending-assets.md)
- [Explore trading opportunities](../trading/README.md)

## Troubleshooting

### Transaction Pending for Too Long

If your transaction has been pending for an extended period:
- Check the network status for congestion
- Verify the transaction status on the blockchain explorer
- Contact support if the issue persists after 30 minutes

### Tokens Not Received

If you don't see your tokens in the destination wallet:
- Ensure you're connected to the correct network in your wallet
- Check the transaction status on Axelar Explorer
- Allow up to 15 minutes during periods of high network congestion
- Verify that your wallet supports the token you're receiving

### Insufficient Gas Fees

If you encounter gas fee errors:
- Ensure you have enough native tokens (ETH, FIL, etc.) to cover gas fees
- Try reducing the amount you're swapping to leave room for gas fees
- Consider bridging during off-peak hours when gas fees are lower

## Technical Details

The Bridge feature utilizes **Axelar's cross-chain technology** to ensure secure and efficient asset transfers between supported networks. The process involves:

1. Locking your tokens in a smart contract on the source chain
2. Generating proof of this lock
3. Verifying the proof on the destination chain
4. Minting or releasing equivalent tokens on the destination chain

This process typically completes within a few minutes but may vary based on network conditions.
