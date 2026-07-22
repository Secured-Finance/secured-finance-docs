---
description: Move assets between networks with the in-app Swap, powered by Squid Router (built on Axelar)
---

# Swap (Bridge)

The [**Swap**](https://app.secured.finance/swap/) tab performs cross-chain swaps inside the app — for example, swapping USDC on Ethereum into FIL on Filecoin — without using an external exchange. It is powered by **Squid Router**, built on the Axelar network.

Typical uses: obtaining native gas tokens for another network (e.g. FIL for Filecoin transactions), or moving collateral to the chain where you want to trade.

## How to bridge

1. Connect your wallet and open the **Swap** tab.
2. Choose the **From** network and token, and the **To** network and token.
3. Enter the amount and review the estimated output after fees, the rate, and the estimated completion time.
4. First time with this token? Approve it when prompted and confirm in your wallet.
5. Confirm the swap and approve the transaction in your wallet. Transfers usually complete within minutes.
6. Verify the tokens arrived on the destination network (switch your wallet's network to check).

<!-- screenshot: bridge-interface -->

## Under the hood

The in-app Swap uses **Squid Router** to route transfers over the **Axelar** network: your tokens are locked in a smart contract on the source chain, a proof is generated and verified on the destination chain, and the equivalent tokens are minted or released there.

## Troubleshooting

* **Pending for a long time** — check the transaction on Axelar's explorer; congestion can add delays. Contact [support](../../../community/support-and-contacts.md) if nothing moves after ~30 minutes.
* **Tokens not visible** — confirm your wallet is on the destination network and the token is added to the wallet's token list.
* **Gas errors** — keep enough native tokens on the source chain; reduce the swap amount if needed.
