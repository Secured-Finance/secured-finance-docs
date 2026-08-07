---
description: Turn lending positions into transferable ERC-20 ZC Tokens
---

# 🪙 Tokenization (ZC Tokens)

Lending positions can be **tokenized as standard ERC-20 tokens** — called **ZC Tokens** — and withdrawn from the platform. A ZC Token is a portable claim on the underlying position: transfer it to another wallet, trade it on secondary markets, or use it in other DeFi protocols. Deposit it back at any time to manage the position inside the app again.

## How it works

* **Withdraw as token**: select a lending position and mint the corresponding ZC Token to your wallet. Partial amounts are supported.
* **Deposit back**: the token is burned and the position is credited to your protocol account.
* **Two token types**:
  * **ZC Tokens** carry a specific maturity (e.g. _ZC ETH DEC2026_) and are minted from the FutureValueVault.
  * **ZC perpetual tokens** (maturity = 0, e.g. _ZC ETH_) represent auto-rolled positions in [Genesis Value](../advanced-topics/orderbook-deep-dive/genesis-value-and-compound-factor.md) terms and are minted from the GenesisValueVault.

<figure><img src="../../.gitbook/assets/ZCToken mint.png" alt=""><figcaption><p>ZC Token minting process</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/ZCToken burn.png" alt=""><figcaption><p>ZC Token burning process</p></figcaption></figure>

## Naming conventions

Example for a December 2026 expiry:

| Asset | ZC Token name   |     Symbol     | Perpetual name | Perpetual symbol |
| ----- | --------------- | :------------: | :------------: | :--------------: |
| ETH   | ZC ETH DEC2026  |  zcETH-2026-12 |     ZC ETH     |       zcETH      |
| WBTC  | ZC WBTC DEC2026 | zcWBTC-2026-12 |     ZC WBTC    |      zcWBTC      |
| USDC  | ZC USDC DEC2026 | zcUSDC-2026-12 |     ZC USDC    |      zcUSDC      |

Wallets with short symbol limits (e.g. MetaMask, 11 characters) display a compact form: `zcETH26D` (month codes: M=Mar, J=Jun, S=Sep, D=Dec). If a token doesn't appear automatically, import it manually using the contract address shown in the app.

## What happens at maturity

A ZC Token's claim reaches par at maturity, but — as everywhere in the protocol — **there is no automatic settlement**. Deposit the token back into the platform, where the position follows the standard [Auto-Roll / unwind](fixed-maturity-and-auto-roll.md) flow.

## Common questions

<details>

<summary>Can I tokenize part of a position?</summary>

Yes. Mint ZC Tokens for any portion; the remainder stays as a regular position in your account.

</details>

<details>

<summary>Are ZC Tokens tradable outside Secured Finance?</summary>

They are standard ERC-20s, so yes — subject to whatever liquidity exists on external venues. They can also serve as collateral in protocols that choose to accept them.

</details>

<details>

<summary>What's the difference between a ZC Token and a ZC perpetual token?</summary>

A ZC Token references one maturity and converges to par on that date. A perpetual ZC token represents a continuously auto-rolled position (accounted in Genesis Value), with no single maturity date.

</details>

## Related

* [Zero-Coupon Bonds](zero-coupon-bonds.md) — the underlying instrument
* [Genesis Value & Compound Factor](../advanced-topics/orderbook-deep-dive/genesis-value-and-compound-factor.md) — perpetual token accounting
