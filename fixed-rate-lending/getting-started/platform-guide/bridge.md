---
description: Move assets between networks, powered by Axelar
---

# Bridge

The [**Bridge**](https://app.secured.finance/bridge/) tab performs cross-chain swaps inside the app — for example, swapping USDC on Ethereum into FIL on Filecoin — without using an external exchange. It is powered by **Axelar**.

Typical uses: obtaining native gas tokens for another network (e.g. FIL for Filecoin transactions), or moving collateral to the chain where you want to trade.

## How to bridge

1. Connect your wallet and open the Bridge tab.
2. Choose the **From** network and token, and the **To** network and token.
3. Enter the amount and review the estimated output after fees, the rate, and the estimated completion time.
4. First time with this token? Approve it (**Give Permission to Use Token**) and confirm in your wallet.
5. Click **Swap** and confirm. Transfers usually complete within minutes.
6. Verify the tokens arrived on the destination network (switch your wallet's network to check).

<!-- screenshot: bridge-interface -->

## Under the hood

Axelar locks your tokens in a smart contract on the source chain, generates a proof, verifies it on the destination chain, and mints or releases the equivalent tokens there.

## Troubleshooting

* **Pending for a long time** — check the transaction on Axelar's explorer; congestion can add delays. Contact [support](../../../community/support-and-contacts.md) if nothing moves after ~30 minutes.
* **Tokens not visible** — confirm your wallet is on the destination network and the token is added to the wallet's token list.
* **Gas errors** — keep enough native tokens on the source chain; reduce the swap amount if needed.
