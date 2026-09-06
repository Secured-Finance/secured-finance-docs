---
description: Try everything risk-free on the Filecoin Calibration testnet
---

# 🧪 Getting Test USDFC on Testnet

Everything in the previous guides can be practiced with worthless test tokens on the Filecoin Calibration testnet. The testnet app lives at [**stg.usdfc.net**](https://stg.usdfc.net) — a separate deployment from mainnet ([app.usdfc.net](https://app.usdfc.net)). All you need is a web3 wallet.

## Step 1 — Get test FIL (tFIL) from the faucet

1. Visit the [Calibration testnet faucet](https://faucet.calibnet.chainsafe-fil.io/funds.html).
2. Enter your wallet address and complete any verification.
3. Request tFIL — the faucet dispenses about 100 tFIL per request and limits how often you can request, so grab it once and it will cover plenty of testing.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-27 20.49.16.png" alt=""><figcaption><p>The Calibration faucet</p></figcaption></figure>

## Step 2 — Connect to the testnet app

Open [stg.usdfc.net](https://stg.usdfc.net), click **Connect Wallet**, and make sure your wallet is on the **Filecoin Calibration** network — the app will prompt you to add it if it's missing.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-27 21.48.02.png" alt=""><figcaption><p>Connecting and adding the Calibration network</p></figcaption></figure>

## Step 3 — Open a Trove and mint test USDFC

On the **Trove** page, deposit tFIL and mint USDFC exactly as described in [Creating Your First Trove](creating-your-first-trove.md) — same minimums, same fees, same collateral ratio rules, just with valueless tokens.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-27 21.52.09.png" alt=""><figcaption><p>Minting test USDFC</p></figcaption></figure>

## Step 4 — Add test USDFC to your wallet

On the Dashboard, find "Add USDFC to Wallet" and click **Click here**; approve the token in your wallet.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-27 21.54.45.png" alt=""><figcaption><p>Adding USDFC to the wallet</p></figcaption></figure>

## Step 5 — Practice closing the Trove

Closing is worth practicing on testnet because of one catch: you must repay your **total debt**, which includes the borrowing fee — so the USDFC you minted isn't quite enough on its own.

1. On the **Trove** page, open the **Close Trove** tab.
2. If the app says you need more USDFC to cover the fees, get the shortfall from another account or a swap.
3. Click **Repay & Close Trove** and confirm. Your collateral returns, and the 20 USDFC Liquidation Reserve is refunded as part of closing.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-27 21.56.26.png" alt=""><figcaption><p>Closing a Trove repays the borrowed amount plus fees</p></figcaption></figure>

## What else works on testnet

* **Stability Pool** — deposit your test USDFC exactly as in [Using the Stability Pool](using-the-stability-pool.md).
* **Fixed-Rate Lending** — the testnet market runs at [stg.secured.finance](https://stg.secured.finance/?chain_id=314159); see the [lending quick-start](../../fixed-rate-lending/getting-started/quick-start-lend.md).

**Bridge and SushiSwap are mainnet-only.** And testnet tokens can never move to mainnet — they're separate networks.

## Troubleshooting

* **Faucet says you've already claimed** — it rate-limits per address; wait for the cooldown or test with a different address.
* **App shows the wrong network** — switch your wallet to Filecoin Calibration (chain ID 314159) and reconnect.
* **Can't close the Trove** — you need slightly more USDFC than you minted to cover the borrowing fee; see Step 5.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-27 21.57.06.png" alt=""><figcaption><p>The Stability Pool on testnet</p></figcaption></figure>
