---
description: Frequently asked questions about the Fixed-Rate Lending Protocol
---

# ❓ FAQs

## Platform basics

<details>

<summary>What is Secured Finance?</summary>

A DeFi platform for **fixed-rate, fixed-term lending and borrowing**, built on a fully on-chain order book and Zero-Coupon bonds, live on Ethereum, Arbitrum and Filecoin. Secured Finance also operates the [USDFC stablecoin](../usdfc-stablecoin/overview.md) on Filecoin and [SF Yield Vault](../sf-yield-vault/overview.md), which lends into these markets on your behalf.

</details>

<details>

<summary>What is a Zero-Coupon (ZC) bond?</summary>

A debt instrument that trades at a discount to its face value of 100. The gap between the price you pay and 100 is the fixed interest for the term: buy at 95 and the position is worth 100 at maturity. On Secured Finance that maturity value is the position's accounting value: at maturity the position auto-rolls into the next quarterly market, and you unwind it when you want the funds. Details: [Zero-Coupon Bonds](core-concepts/zero-coupon-bonds.md).

</details>

<details>

<summary>What asset underlies each ZC bond?</summary>

The currency of that market: lending ETH in the DEC2026 market gives you a claim denominated in ETH (_ZC ETH DEC2026_). Each bond is asset-specific and maturity-specific, and lending positions can be [tokenized as an ERC-20](core-concepts/tokenization.md) for use across DeFi.

</details>

## Trading

<details>

<summary>Is my money locked until maturity?</summary>

There is no fixed lock-up. You can unwind a position at any time, before or after maturity, by trading against the order book. How much you can close at once depends on the liquidity available at that time, and closing at the current price can realize a gain or a loss. If the book is thin, you can [request quotes in the official Discord](getting-started/managing-positions.md#community-liquidity-support). Lending positions can also be tokenized and transferred. Exiting always requires an action on your side: the protocol does not settle positions at maturity. See [Managing Your Positions](getting-started/managing-positions.md).

</details>

<details>

<summary>What happens to my position at maturity?</summary>

It **auto-rolls** into the nearest 3-month market at the roll price, with a roll fee. Auto-Roll is protocol-wide; there is no setting to enable or disable it. To receive your funds instead, unwind the position before or after maturity and withdraw. See [Fixed Maturity & Auto-Roll](core-concepts/fixed-maturity-and-auto-roll.md).

</details>

<details>

<summary>What happens to my open orders at maturity?</summary>

Unfilled orders **expire** and can no longer execute. The reserved funds are released back to your deposit balance through the protocol's accounting cleanup, which runs on your next interaction with that currency, so the balance may update only after your next action. Filled amounts are positions and follow the Auto-Roll rules above. See [Order Life Cycle](core-concepts/order-life-cycle.md).

</details>

<details>

<summary>Why does my order show Blocked, Killed or Partially Filled?</summary>

These labels describe what happened to the unfilled part of a market order. **Blocked** means the [Circuit Breaker](advanced-topics/circuit-breaker.md)'s execution limit stopped further matching; **Killed** means the opposite side of the book ran out; **Partially Filled** means part executed and the rest is in one of those states or, for a limit order, still resting. Completed fills are never reversed. A limit order with a price outside the permitted range is rejected before anything executes. See [Order Life Cycle](core-concepts/order-life-cycle.md).

</details>

<details>

<summary>What fees do I pay?</summary>

The **taker side** of a fill pays the trading fee (1% p.a. prorated: 0.25% for 3 months): market orders, and the portion of a limit order that crosses the book and fills immediately. **Volume resting on the book pays nothing.** Auto-Rolls charge the same rate each quarter. Liquidated borrowers pay a 7% liquidation fee. Full details: [Fees](core-concepts/fees.md) and [Protocol Parameters](protocol-parameters.md).

</details>

## Collateral & risk

<details>

<summary>Why do borrowers need collateral?</summary>

Collateral replaces credit checks. A borrower's position is liquidated while its collateral value still exceeds the debt, so that the debt can be repaid from collateral; the thresholds and haircuts are set to make a shortfall unlikely, and a [Reserve Fund](contracts-and-security/) exists for the case where one occurs. See [Collateral](core-concepts/collateral.md) and [Liquidation](core-concepts/liquidation/).

</details>

<details>

<summary>Which assets can be collateral?</summary>

It varies by network: WBTC, ETH, USDC, JPYC and uMINT (RWA) on Ethereum; WBTC, ETH and USDC on Arbitrum; FIL, iFIL, wpFIL and USDFC on Filecoin. The maintained list is in [Collateral](core-concepts/collateral.md#supported-assets-by-network); haircuts and thresholds are in [Protocol Parameters](protocol-parameters.md).

</details>

<details>

<summary>What happens if my collateral value falls?</summary>

Your LTV rises. Above the liquidation threshold (80%), up to 50% of your debt can be liquidated, with a 7% fee taken from collateral; past the full-liquidation threshold, up to 100%. Watch Collateral Utilization and Liquidation Risk in [Portfolio](getting-started/platform-guide/portfolio.md) and add collateral or reduce debt early. See [Liquidation](core-concepts/liquidation/).

</details>

## Security

<details>

<summary>How do I know I am on the official app?</summary>

Use only these domains: **app.secured.finance** (Fixed-Rate Lending and SF Yield Vault), **app.usdfc.net** (USDFC), **docs.secured.finance** (this documentation) and **secured.finance** (website). Before signing, compare the contract a wallet prompt names with the published addresses for the product you are using: [Fixed-Rate Lending](contracts-and-security/), [USDFC](../usdfc-stablecoin/deployed-contracts/) or [SF Yield Vault](../sf-yield-vault/contracts-and-security.md). Secured Finance never asks for your recovery phrase or private key.

</details>

<details>

<summary>Have the contracts been audited?</summary>

Quantstamp audited the Fixed-Rate Lending contracts in 2023 and 2024 and published a technical report on the September 2026 incident, including a fork-replay verification of the fix. Contract changes since the 2024 audit are listed with their pull requests and execution transactions in [Contract Upgrade History](contracts-and-security/contract-upgrade-history.md); no other audit report has been published for them. The reports and the current bug bounty scope are in [Contracts & Security](contracts-and-security/#audit-reports). USDFC and SF Yield Vault list their own audits on their contract pages.

</details>

<details>

<summary>What happened in September 2026?</summary>

An order-book accounting defect allowed attackers to withdraw about $176,000 of protocol funds across Ethereum, Arbitrum and Filecoin. Markets were paused within hours of detection, the defect was fixed and verified, affected positions were corrected, and markets reopened on 16 October 2026. The loss was borne by the protocol and absorbed by the Secured Finance Foundation; user deposits and positions were restored. The [Postmortem](https://medium.com/secured-finance/postmortem-the-september-2026-lending-protocol-incident-and-our-recovery-28bd48e68f22), the [Quantstamp technical report](https://github.com/Secured-Finance/contracts/blob/c1ef5ea873564f6f3cf6df49587733b166694ecd/audits/2026-09-Quantstamp-Incident-Technical-Report.pdf) and [Recovery & Verification](contracts-and-security/security-and-incident-reports/incident-recovery-and-verification.md) give the full record.

</details>

<details>

<summary>Where are protocol changes announced?</summary>

Every contract upgrade is recorded with its transactions in [Contract Upgrade History](contracts-and-security/contract-upgrade-history.md), and the [Monitoring System](contracts-and-security/monitoring-system.md) page describes the alerts in place. Announcements are posted on [X](https://twitter.com/Secured_Fi) and in the [official Discord](https://discord.com/invite/3kytCrv3qY).

</details>

## Advanced

<details>

<summary>What is Itayose?</summary>

The opening auction that sets a fair price whenever a new quarterly market launches: pre-open orders are collected for 7 days and matched simultaneously at the volume-maximizing price, with zero fees for filled pre-orders. See [Itayose](advanced-topics/itayose.md).

</details>

<details>

<summary>How can the order book be fully on-chain? Isn't that too expensive?</summary>

Three techniques make it economical: Red-Black Trees for O(log n) order management, lazy evaluation to defer storage writes, and Genesis Value accounting to roll all positions with one update. See the [Orderbook Deep Dive](advanced-topics/orderbook-deep-dive/).

</details>

<details>

<summary>Can I run a liquidation bot?</summary>

Yes. Liquidation is permissionless and pays a 5% fee to the liquidator. Start with the [Liquidator's Guide](core-concepts/liquidation/liquidators-guide.md).

</details>

## Still stuck?

* Guides: [Getting Started](getting-started/)
* Developers: [Developer Portal](../developer-portal/introduction.md)
* Community support: [Support & Contacts](../community/support-and-contacts.md)
