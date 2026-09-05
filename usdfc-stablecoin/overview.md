---
description: A decentralized, over-collateralized stablecoin backed by Filecoin
---

# 📢 Overview

<figure><img src="../.gitbook/assets/Color Light Background.svg" alt=""><figcaption></figcaption></figure>

[**USDFC**](https://app.usdfc.net) is a USD-pegged stablecoin backed entirely by Filecoin (FIL) and running on the Filecoin Virtual Machine (FVM). You lock FIL as collateral in a **Trove**, mint USDFC against it, and repay whenever you like — no counterparty, no credit check, and no ongoing interest. It is the first decentralized stablecoin fully collateralized by FIL.

## How it works in brief

* **Open a Trove and mint.** Deposit FIL, choose how much USDFC to borrow, and keep your collateral ratio above the **110% minimum**. A one-time borrowing fee (0.5% or more) is added to your debt; there is no interest.
* **Stay collateralized.** If FIL falls and a Trove drops below 110%, it is liquidated: its debt is repaid from the **Stability Pool** and its collateral is distributed to the pool's depositors.
* **Redeem at face value.** Any holder can redeem USDFC for $1 worth of FIL directly from the protocol. This is what anchors the peg — if USDFC trades below $1, redemption arbitrage pushes it back.
* **Recovery Mode.** If the whole system's collateral ratio falls below 150%, stricter rules kick in until it recovers.

The mechanics are covered in depth in [Core Mechanics](core-mechanics/README.md).

## Key parameters

| Parameter | Value |
| --- | --- |
| Minimum Collateral Ratio (MCR) | 110% |
| Recovery Mode threshold (system-wide) | 150% |
| Minimum debt per Trove | 200 USDFC |
| Liquidation Reserve (refunded on close) | 20 USDFC |
| Borrowing fee (one-time) | 0.5% – 5%, varies with the Base Rate |
| Redemption fee | 0.5% + Base Rate |
| Interest | None |

## Putting USDFC to work

Once minted, USDFC is the liquidity layer of Secured Finance's products on Filecoin — and usable across the wider ecosystem:

| Use | Where |
| --- | --- |
| Earn liquidation gains by backing the protocol | [Stability Pool](getting-started/using-the-stability-pool.md) |
| Lend at a fixed rate | [Fixed-Rate Lending](../fixed-rate-lending/overview.md) |
| Earn automated, variable yield | [SF Yield Vault — USDFC Vault](../sf-yield-vault/core-mechanics/available-vaults-and-strategies/usdfc-lending-strategy.md) |
| Trade or provide liquidity | SushiSwap on Filecoin |
| Move to other chains | Bridge (Squid) in the USDFC app |

For a side-by-side view of all Secured Finance products, see [Protocol at a Glance](../introduction/protocol-at-a-glance.md).

## Token standards

USDFC is an ERC-20 token that also implements **EIP-2612** (`permit`) and **EIP-3009** (`transferWithAuthorization` / `receiveWithAuthorization`). Both let a holder authorize a transfer with a signature instead of an on-chain transaction, so a third party can submit it and pay the gas. This is what makes USDFC usable in gasless flows and **x402** (HTTP 402) payment flows. Developers can find the interfaces in the [USDFC SDK](../developer-portal/sdk-reference/usdfc-sdk.md).

## Why Filecoin

FIL is the native asset of the Filecoin network, whose storage economy is growing with AI-era data demand — yet until USDFC there was no way to unlock dollar liquidity from FIL without selling it. USDFC gives storage providers, FIL holders, and DeFi users a decentralized stablecoin native to the FVM, in the way DAI did for Ethereum. Every USDFC in circulation is backed by FIL locked on-chain, adding a layer of utility and composability to the Filecoin economy.

{% hint style="warning" %}
**Borrowing against volatile collateral carries liquidation risk.** If FIL falls far enough, your Trove can be liquidated and you lose your collateral. Read [Liquidation](core-mechanics/liquidation.md) and the [Risk Disclaimer](../resources/legal/risk-disclaimer.md) before opening a Trove.
{% endhint %}

## Where next

| You are | Start here |
| --- | --- |
| New to USDFC | [Getting Started](getting-started/README.md) |
| Ready to mint | [Creating Your First Trove](getting-started/creating-your-first-trove.md) |
| Curious how it works inside | [Core Mechanics](core-mechanics/README.md) |
| Looking for addresses and audits | [Contracts and Security](deployed-contracts.md) |
