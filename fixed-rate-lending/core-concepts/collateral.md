---
description: Accepted assets per network, and how collateral secures every loan
---

# Collateral

Borrowing on the Fixed-Rate Lending Protocol requires **over-collateralization**: you deposit assets worth more than you borrow. This replaces credit checks — anyone can borrow, and lenders are protected because under-collateralized positions are [liquidated](liquidation/README.md).

## Supported assets by network

| Network | Lend / Borrow | Accepted as collateral |
| --- | --- | --- |
| **Ethereum** | WBTC, ETH, USDC, axlFIL, JPYC | WBTC, ETH, USDC, JPYC, uMINT |
| **Arbitrum** | WBTC, ETH, USDC | WBTC, ETH, USDC |
| **Filecoin (FVM)** | FIL, USDFC | FIL, iFIL, wpFIL, USDFC |

{% hint style="info" %}
Asset availability last confirmed with the team on 2026-07-16 (JPYC lending markets: Ethereum only; wpFIL collateral: Filecoin only; uMINT/RWA collateral: Ethereum only). The live list can be read per network from `CurrencyController.getCurrencies()`.
{% endhint %}

{% hint style="warning" %}
Avalanche support is **deprecated**. Polygon zkEVM has been **sunset and is no longer operational**. Legacy deployment addresses are retained for historical reference only: [Contracts & Security](../contracts-and-security.md).
{% endhint %}

Current haircuts, thresholds, and the authoritative asset list: [Protocol Parameters](../protocol-parameters.md).

## Asset notes

* **USDFC** — Secured Finance's own FIL-backed stablecoin, minted via CDP on FVM. [Learn more](../../usdfc-stablecoin/overview.md).
* **iFIL / wpFIL (liquid staking tokens)** — represent staked FIL that keeps earning staking rewards *while* serving as collateral. For example, stake FIL on [GLIF](https://glif.io/) to receive iFIL, then deposit the iFIL as collateral — a dual-yield position. Both are accepted on Filecoin.
* **axlFIL** — Axelar-bridged FIL on Ethereum.
* **JPYC** — JPY-pegged stablecoin; fixed-rate JPY lending markets are live on **Ethereum** (as of July 2026).
* **RWA collateral** — tokenized money-market fund collateral (uMINT, via DigiFT), accepted as collateral on **Ethereum** (as of July 2026).

## How collateral is monitored

* The protocol values collateral continuously using **Chainlink price feeds**, plus [Mark-to-Market](liquidation/mark-to-market.md) pricing for ZC bond positions.
* Your **Loan-to-Value (LTV)** ratio — debt value over collateral value — is visible in the [Portfolio](../getting-started/platform-guide/portfolio.md) risk panel.
* If LTV reaches the liquidation threshold, the position can be [liquidated](liquidation/README.md).

**Multi-collateral is supported**: you can back a single borrowing book with several asset types, diversifying against any one asset's volatility.

## Common questions

<details>

<summary>What happens if my collateral value drops?</summary>

Your LTV rises. If it reaches the liquidation threshold, 50% of your debt can be liquidated — or **100%** if LTV deteriorates past the full-liquidation threshold — with a fee taken from your collateral. Prevent this by adding collateral or reducing debt early (unwind the position, or place an opposite order for part of the amount) — see [Liquidation](liquidation/README.md).

</details>

<details>

<summary>Can I withdraw collateral while I have open borrows?</summary>

Yes, as long as the remaining collateral keeps your LTV safely below the threshold. The app blocks withdrawals that would put your position at immediate risk.

</details>

<details>

<summary>Can ZC bonds themselves be used as collateral?</summary>

Yes — lending positions can serve as collateral for borrowing in the same currency, enabling yield-spread strategies. See [ZC Bonds as Collateral](zc-bonds-as-collateral.md).

</details>
